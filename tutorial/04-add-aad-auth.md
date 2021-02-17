---
ms.openlocfilehash: 69d77c19cb2c589086df2b4bf19eeadf41aad58a
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274297"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cet exercice, vous allez activer l' [sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) de l’Application Office dans le add-in et étendre l’API web pour prendre en charge le flux « de la part [de](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)». Cette étape est nécessaire pour obtenir le jeton d’accès OAuth nécessaire pour appeler Microsoft Graph.

## <a name="overview"></a>Présentation

L' ssO du add-in Office fournit un jeton d’accès, mais ce jeton permet uniquement au add-in d’appeler sa propre API web. Il n’autorise pas l’accès direct à Microsoft Graph. Le processus fonctionne comme suit.

1. Le add-in obtient un jeton en appelant [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-). L’audience de ce jeton (la revendication) est `aud` l’ID d’application de l’inscription de l’application du module.
1. Le add-in envoie ce jeton dans l’en-tête lorsqu’il effectue un `Authorization` appel à l’API web.
1. L’API web valide le jeton, puis utilise le flux « de la part de » pour échanger ce jeton contre un jeton Microsoft Graph. L’audience de ce nouveau jeton est `https://graph.microsoft.com` .
1. L’API web utilise le nouveau jeton pour appeler Microsoft Graph et renvoie les résultats au module.

## <a name="configure-the-solution"></a>Configurer la solution

1. Ouvrez **./.env** et mettez à jour l’ID d’application et la `AZURE_APP_ID` secret client à partir de `AZURE_CLIENT_SECRET` l’inscription de votre application.

    > [!IMPORTANT]
    > Si vous utilisez un contrôle source tel que Git, il est temps d’exclure le fichier **.env** du contrôle source afin d’éviter toute fuite accidentelle de votre ID d’application et de votre secret client.

1. Ouvrez **./manifest/manifest.xml** et remplacez toutes les instances par l’ID de l’application à partir de `YOUR_APP_ID_HERE` l’inscription de votre application.

1. Créez un fichier dans le répertoire **./src/addin** nommé **config.js** et ajoutez le code suivant, en remplaçant par l’ID d’application de l’inscription de `YOUR_APP_ID_HERE` votre application.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/config.example.js":::

## <a name="implement-sign-in"></a>Implémentation de la connexion

1. Ouvrez **./src/api/auth.ts** et ajoutez les `import` instructions suivantes en haut du fichier.

    ```typescript
    import jwt, { SigningKeyCallback, JwtHeader } from 'jsonwebtoken';
    import jwksClient from 'jwks-rsa';
    import * as msal from '@azure/msal-node';
    ```

1. Ajoutez le code suivant après `import` les instructions.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="TokenExchangeSnippet":::

    Ce code [initialise un client confidentiel MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)et exporte une fonction pour obtenir un jeton Graph à partir du jeton envoyé par le module.

1. Ajoutez le code suivant avant la `export default authRouter;` ligne.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="GetAuthStatusSnippet":::

    Ce code implémente une API ( ) qui vérifie si le jeton de la application peut être échangé silencieusement `GET /auth/status` contre un jeton Graph. Le add-in utilise cette API pour déterminer s’il doit présenter une connexion interactive à l’utilisateur.

1. Ouvrez **./src/addin/taskpane.js** et ajoutez le code suivant au fichier.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="AuthUiSnippet":::

    Ce code ajoute des fonctions pour mettre à jour l’interface utilisateur et utiliser l’API de boîte de [dialogue Office](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) pour initier un flux d’authentification interactif.

1. Ajoutez la fonction suivante pour implémenter une interface utilisateur principale temporaire.

    ```javascript
    function showMainUi() {
      $('.container').empty();
      $('<p/>', {
        class: 'ms-fontSize-24 ms-fontWeight-bold',
        text: 'Authenticated!'
      }).appendTo('.container');
    }
    ```

1. Remplacez `Office.onReady` l’appel existant par ce qui suit.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="OfficeReadySnippet":::

    Considérez ce que fait ce code.

    - Lorsque le volet Des tâches se charge pour la première fois, il appelle pour obtenir un jeton pour `getAccessToken` l’API web du add-in.
    - Il utilise ce jeton pour appeler l’API afin de vérifier si l’utilisateur a encore donné son consentement aux `/auth/status` étendues Microsoft Graph.
        - Si l’utilisateur n’a pas donné son consentement, il utilise une fenêtre pop-up pour obtenir son consentement par le biais d’une connexion interactive.
        - Si l’utilisateur a donné son consentement, il charge l’interface utilisateur principale.

### <a name="getting-user-consent"></a>Obtention du consentement de l’utilisateur

Même si le add-in utilise l' luiso, l’utilisateur doit tout de même consentir à ce qu’il accède à ses données via Microsoft Graph. L’obtention du consentement est un processus à durée seule. Une fois que l’utilisateur a donné son consentement, le jeton DSO peut être échangé contre un jeton Graph sans aucune interaction de l’utilisateur. Dans cette section, vous allez implémenter l’expérience de consentement dans le add-in à l’aide [de msal-browser](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser).

1. Créez un fichier dans le répertoire **./src/addin** nommé **consent.js** et ajoutez le code suivant.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/consent.js" id="ConsentJsSnippet":::

    Ce code se connecte pour l’utilisateur, demandant l’ensemble des autorisations Microsoft Graph configurées lors de l’inscription de l’application.

1. Créez un fichier dans le répertoire **./src/addin** nommé **consent.html** et ajoutez le code suivant.

    :::code language="html" source="../demo/graph-tutorial/src/addin/consent.html" id="ConsentHtmlSnippet":::

    Ce code implémente une page HTML de base pour charger **consent.js** fichier. Cette page sera chargée dans une boîte de dialogue de fenêtre.

1. Enregistrez toutes vos modifications et redémarrez le serveur.

1. Re-chargez **votremanifest.xml** en utilisant les mêmes étapes de chargement de version latérale du [add-in dans Excel.](02-create-app.md#side-load-the-add-in-in-excel)

1. Sélectionnez le **bouton Importer** le calendrier sous **l’onglet Accueil** pour ouvrir le volet Des tâches.

1. Sélectionnez **le bouton** Accorder une autorisation dans le volet Des tâches pour lancer la boîte de dialogue de consentement dans une fenêtre pop-up. Connectez-vous et accordez le consentement.

1. Le volet Des tâches est mis à jour avec un « Authentifié ! » Message. Vous pouvez vérifier les jetons comme suit.

    - Dans les outils de développement de votre navigateur, le jeton d’API s’affiche dans la console.
    - Dans votre CLI où vous exécutez le serveur Node.js, le jeton Graph est imprimé.

    Vous pouvez comparer ces jetons à [https://jwt.ms](https://jwt.ms) . Notez que l’audience du jeton d’API ( ) est définie sur l’ID d’application de l’inscription de votre application, et que `aud` l’étendue ( ) est `scp` `access_as_user` .
