---
ms.openlocfilehash: 69d77c19cb2c589086df2b4bf19eeadf41aad58a
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274297"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="d9bb6-101">Dans cet exercice, vous allez activer l' [sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) de l’Application Office dans le add-in et étendre l’API web pour prendre en charge le flux « de la part [de](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)».</span><span class="sxs-lookup"><span data-stu-id="d9bb6-101">In this exercise you will enable [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) in the add-in, and extend the web API to support [on-behalf-of flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="d9bb6-102">Cette étape est nécessaire pour obtenir le jeton d’accès OAuth nécessaire pour appeler Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span>

## <a name="overview"></a><span data-ttu-id="d9bb6-103">Présentation</span><span class="sxs-lookup"><span data-stu-id="d9bb6-103">Overview</span></span>

<span data-ttu-id="d9bb6-104">L' ssO du add-in Office fournit un jeton d’accès, mais ce jeton permet uniquement au add-in d’appeler sa propre API web.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-104">Office Add-in SSO provides an access token, but that token is only enables the add-in to call it's own web API.</span></span> <span data-ttu-id="d9bb6-105">Il n’autorise pas l’accès direct à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-105">It does not enable direct access to the Microsoft Graph.</span></span> <span data-ttu-id="d9bb6-106">Le processus fonctionne comme suit.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-106">The process works as follows.</span></span>

1. <span data-ttu-id="d9bb6-107">Le add-in obtient un jeton en appelant [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-).</span><span class="sxs-lookup"><span data-stu-id="d9bb6-107">The add-in gets a token by calling [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-).</span></span> <span data-ttu-id="d9bb6-108">L’audience de ce jeton (la revendication) est `aud` l’ID d’application de l’inscription de l’application du module.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-108">This token's audience (the `aud` claim) is the application ID of the add-in's app registration.</span></span>
1. <span data-ttu-id="d9bb6-109">Le add-in envoie ce jeton dans l’en-tête lorsqu’il effectue un `Authorization` appel à l’API web.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-109">The add-in sends this token in the `Authorization` header when it makes a call to the web API.</span></span>
1. <span data-ttu-id="d9bb6-110">L’API web valide le jeton, puis utilise le flux « de la part de » pour échanger ce jeton contre un jeton Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-110">The web API validates the token, then uses the on-behalf-of flow to exchange this token for a Microsoft Graph token.</span></span> <span data-ttu-id="d9bb6-111">L’audience de ce nouveau jeton est `https://graph.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="d9bb6-111">This new token's audience is `https://graph.microsoft.com`.</span></span>
1. <span data-ttu-id="d9bb6-112">L’API web utilise le nouveau jeton pour appeler Microsoft Graph et renvoie les résultats au module.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-112">The web API uses the new token to make calls to the Microsoft Graph, and returns the results back to the add-in.</span></span>

## <a name="configure-the-solution"></a><span data-ttu-id="d9bb6-113">Configurer la solution</span><span class="sxs-lookup"><span data-stu-id="d9bb6-113">Configure the solution</span></span>

1. <span data-ttu-id="d9bb6-114">Ouvrez **./.env** et mettez à jour l’ID d’application et la `AZURE_APP_ID` secret client à partir de `AZURE_CLIENT_SECRET` l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-114">Open **./.env** and update the `AZURE_APP_ID` and `AZURE_CLIENT_SECRET` with the application ID and client secret from your app registration.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d9bb6-115">Si vous utilisez un contrôle source tel que Git, il est temps d’exclure le fichier **.env** du contrôle source afin d’éviter toute fuite accidentelle de votre ID d’application et de votre secret client.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-115">If you're using source control such as git, now would be a good time to exclude the **.env** file from source control to avoid inadvertently leaking your app ID and client secret.</span></span>

1. <span data-ttu-id="d9bb6-116">Ouvrez **./manifest/manifest.xml** et remplacez toutes les instances par l’ID de l’application à partir de `YOUR_APP_ID_HERE` l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-116">Open **./manifest/manifest.xml** and replace all instances of `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

1. <span data-ttu-id="d9bb6-117">Créez un fichier dans le répertoire **./src/addin** nommé **config.js** et ajoutez le code suivant, en remplaçant par l’ID d’application de l’inscription de `YOUR_APP_ID_HERE` votre application.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-117">Create a new file in the **./src/addin** directory named **config.js** and add the following code, replacing `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/config.example.js":::

## <a name="implement-sign-in"></a><span data-ttu-id="d9bb6-118">Implémentation de la connexion</span><span class="sxs-lookup"><span data-stu-id="d9bb6-118">Implement sign-in</span></span>

1. <span data-ttu-id="d9bb6-119">Ouvrez **./src/api/auth.ts** et ajoutez les `import` instructions suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-119">Open **./src/api/auth.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import jwt, { SigningKeyCallback, JwtHeader } from 'jsonwebtoken';
    import jwksClient from 'jwks-rsa';
    import * as msal from '@azure/msal-node';
    ```

1. <span data-ttu-id="d9bb6-120">Ajoutez le code suivant après `import` les instructions.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-120">Add the following code after the `import` statements.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="TokenExchangeSnippet":::

    <span data-ttu-id="d9bb6-121">Ce code [initialise un client confidentiel MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)et exporte une fonction pour obtenir un jeton Graph à partir du jeton envoyé par le module.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-121">This code [initializes an MSAL confidential client](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md), and exports a function to get a Graph token from the token sent by the add-in.</span></span>

1. <span data-ttu-id="d9bb6-122">Ajoutez le code suivant avant la `export default authRouter;` ligne.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-122">Add the following code before the `export default authRouter;` line.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="GetAuthStatusSnippet":::

    <span data-ttu-id="d9bb6-123">Ce code implémente une API ( ) qui vérifie si le jeton de la application peut être échangé silencieusement `GET /auth/status` contre un jeton Graph.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-123">This code implements an API (`GET /auth/status`) that checks if the add-in token can be silently exchanged for a Graph token.</span></span> <span data-ttu-id="d9bb6-124">Le add-in utilise cette API pour déterminer s’il doit présenter une connexion interactive à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-124">The add-in will use this API to determine if it needs to present an interactive login to the user.</span></span>

1. <span data-ttu-id="d9bb6-125">Ouvrez **./src/addin/taskpane.js** et ajoutez le code suivant au fichier.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-125">Open **./src/addin/taskpane.js** and add the following code to the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="AuthUiSnippet":::

    <span data-ttu-id="d9bb6-126">Ce code ajoute des fonctions pour mettre à jour l’interface utilisateur et utiliser l’API de boîte de [dialogue Office](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) pour initier un flux d’authentification interactif.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-126">This code adds functions to update the UI, and to use the [Office Dialog API](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) to initiate an interactive authentication flow.</span></span>

1. <span data-ttu-id="d9bb6-127">Ajoutez la fonction suivante pour implémenter une interface utilisateur principale temporaire.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-127">Add the following function to implement a temporary main UI.</span></span>

    ```javascript
    function showMainUi() {
      $('.container').empty();
      $('<p/>', {
        class: 'ms-fontSize-24 ms-fontWeight-bold',
        text: 'Authenticated!'
      }).appendTo('.container');
    }
    ```

1. <span data-ttu-id="d9bb6-128">Remplacez `Office.onReady` l’appel existant par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-128">Replace the existing `Office.onReady` call with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="OfficeReadySnippet":::

    <span data-ttu-id="d9bb6-129">Considérez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-129">Consider what this code does.</span></span>

    - <span data-ttu-id="d9bb6-130">Lorsque le volet Des tâches se charge pour la première fois, il appelle pour obtenir un jeton pour `getAccessToken` l’API web du add-in.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-130">When the task pane first loads, it calls `getAccessToken` to get a token scoped for the add-in's web API.</span></span>
    - <span data-ttu-id="d9bb6-131">Il utilise ce jeton pour appeler l’API afin de vérifier si l’utilisateur a encore donné son consentement aux `/auth/status` étendues Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-131">It uses that token to call the `/auth/status` API to check if the user has given consent to the Microsoft Graph scopes yet.</span></span>
        - <span data-ttu-id="d9bb6-132">Si l’utilisateur n’a pas donné son consentement, il utilise une fenêtre pop-up pour obtenir son consentement par le biais d’une connexion interactive.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-132">If the user has not consented, it uses a pop-up window to get the user's consent through an interactive login.</span></span>
        - <span data-ttu-id="d9bb6-133">Si l’utilisateur a donné son consentement, il charge l’interface utilisateur principale.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-133">If the user has consented, it loads the main UI.</span></span>

### <a name="getting-user-consent"></a><span data-ttu-id="d9bb6-134">Obtention du consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d9bb6-134">Getting user consent</span></span>

<span data-ttu-id="d9bb6-135">Même si le add-in utilise l' luiso, l’utilisateur doit tout de même consentir à ce qu’il accède à ses données via Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-135">Even though the add-in is using SSO, the user still has to consent to the add-in accessing their data via Microsoft Graph.</span></span> <span data-ttu-id="d9bb6-136">L’obtention du consentement est un processus à durée seule.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-136">Getting consent is a one-time process.</span></span> <span data-ttu-id="d9bb6-137">Une fois que l’utilisateur a donné son consentement, le jeton DSO peut être échangé contre un jeton Graph sans aucune interaction de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-137">Once the user has granted consent, the SSO token can be exchanged for a Graph token without any user interaction.</span></span> <span data-ttu-id="d9bb6-138">Dans cette section, vous allez implémenter l’expérience de consentement dans le add-in à l’aide [de msal-browser](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser).</span><span class="sxs-lookup"><span data-stu-id="d9bb6-138">In this section you'll implement the consent experience in the add-in using [msal-browser](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser).</span></span>

1. <span data-ttu-id="d9bb6-139">Créez un fichier dans le répertoire **./src/addin** nommé **consent.js** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-139">Create a new file in the **./src/addin** directory named **consent.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/consent.js" id="ConsentJsSnippet":::

    <span data-ttu-id="d9bb6-140">Ce code se connecte pour l’utilisateur, demandant l’ensemble des autorisations Microsoft Graph configurées lors de l’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-140">This code does login for the user, requesting the set of Microsoft Graph permissions that are configured on the app registration.</span></span>

1. <span data-ttu-id="d9bb6-141">Créez un fichier dans le répertoire **./src/addin** nommé **consent.html** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-141">Create a new file in the **./src/addin** directory named **consent.html** and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/addin/consent.html" id="ConsentHtmlSnippet":::

    <span data-ttu-id="d9bb6-142">Ce code implémente une page HTML de base pour charger **consent.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-142">This code implements a basic HTML page to load the **consent.js** file.</span></span> <span data-ttu-id="d9bb6-143">Cette page sera chargée dans une boîte de dialogue de fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-143">This page will be loaded in a pop-up dialog.</span></span>

1. <span data-ttu-id="d9bb6-144">Enregistrez toutes vos modifications et redémarrez le serveur.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-144">Save all of your changes and restart the server.</span></span>

1. <span data-ttu-id="d9bb6-145">Re-chargez **votremanifest.xml** en utilisant les mêmes étapes de chargement de version latérale du [add-in dans Excel.](02-create-app.md#side-load-the-add-in-in-excel)</span><span class="sxs-lookup"><span data-stu-id="d9bb6-145">Re-upload your **manifest.xml** file using the same steps in [Side-load the add-in in Excel](02-create-app.md#side-load-the-add-in-in-excel).</span></span>

1. <span data-ttu-id="d9bb6-146">Sélectionnez le **bouton Importer** le calendrier sous **l’onglet Accueil** pour ouvrir le volet Des tâches.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-146">Select the **Import Calendar** button on the **Home** tab to open the task pane.</span></span>

1. <span data-ttu-id="d9bb6-147">Sélectionnez **le bouton** Accorder une autorisation dans le volet Des tâches pour lancer la boîte de dialogue de consentement dans une fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-147">Select the **Give permission** button in the task pane to launch the consent dialog in a pop-up window.</span></span> <span data-ttu-id="d9bb6-148">Connectez-vous et accordez le consentement.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-148">Sign in and grant consent.</span></span>

1. <span data-ttu-id="d9bb6-149">Le volet Des tâches est mis à jour avec un « Authentifié ! »</span><span class="sxs-lookup"><span data-stu-id="d9bb6-149">The task pane updates with an "Authenticated!"</span></span> <span data-ttu-id="d9bb6-150">Message.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-150">message.</span></span> <span data-ttu-id="d9bb6-151">Vous pouvez vérifier les jetons comme suit.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-151">You can check the tokens as follows.</span></span>

    - <span data-ttu-id="d9bb6-152">Dans les outils de développement de votre navigateur, le jeton d’API s’affiche dans la console.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-152">In your brower's developer tools, the API token is shown in the Console.</span></span>
    - <span data-ttu-id="d9bb6-153">Dans votre CLI où vous exécutez le serveur Node.js, le jeton Graph est imprimé.</span><span class="sxs-lookup"><span data-stu-id="d9bb6-153">In your CLI where you are running the Node.js server, the Graph token is printed.</span></span>

    <span data-ttu-id="d9bb6-154">Vous pouvez comparer ces jetons à [https://jwt.ms](https://jwt.ms) .</span><span class="sxs-lookup"><span data-stu-id="d9bb6-154">You can compare these token at [https://jwt.ms](https://jwt.ms).</span></span> <span data-ttu-id="d9bb6-155">Notez que l’audience du jeton d’API ( ) est définie sur l’ID d’application de l’inscription de votre application, et que `aud` l’étendue ( ) est `scp` `access_as_user` .</span><span class="sxs-lookup"><span data-stu-id="d9bb6-155">Notice that the API token's audience (`aud`) is set to the application ID of your app registration, and the scope (`scp`) is `access_as_user`.</span></span>
