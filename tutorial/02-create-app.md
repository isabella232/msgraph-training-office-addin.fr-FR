---
ms.openlocfilehash: 70df2dfceb1d2df527acfecab894b28019c6febb
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274293"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cet exercice, vous allez créer une solution de add-in Office à l’aide [d’Express](http://expressjs.com/). La solution se compose de deux parties.

- Le add-in, implémenté en tant que fichiers HTML et JavaScript statiques.
- Un Node.js/Express qui sert le add-in et implémente une API web pour récupérer des données pour le add-in.

## <a name="create-the-server"></a>Créer le serveur

1. Ouvrez votre interface de ligne de commande (CLI), accédez à un répertoire dans lequel vous souhaitez créer votre projet et exécutez la commande suivante pour générer une package.jssur le fichier.

    ```Shell
    yarn init
    ```

    Entrez des valeurs pour les invites selon le cas. Si vous n’êtes pas sûr, les valeurs par défaut sont bonnes.

1. Exécutez les commandes suivantes pour installer les dépendances.

    ```Shell
    yarn add express@4.17.1 express-promise-router@4.0.1 dotenv@8.2.0 node-fetch@2.6.1 jsonwebtoken@8.5.1@
    yarn add jwks-rsa@1.11.0 @azure/msal-node@1.0.0-beta.1 @microsoft/microsoft-graph-client@2.1.1
    yarn add date-fns@2.16.1 date-fns-tz@1.0.12 isomorphic-fetch@3.0.0 windows-iana@4.2.1
    yarn add -D typescript@4.0.5 ts-node@9.0.0 nodemon@2.0.6 @types/node@14.14.7 @types/express@4.17.9
    yarn add -D @types/node-fetch@2.5.7 @types/jsonwebtoken@8.5.0 @types/microsoft-graph@1.26.0
    yarn add -D @types/office-js@1.0.147 @types/jquery@3.5.4 @types/isomorphic-fetch@0.0.35
    ```

1. Exécutez la commande suivante pour générer une tsconfig.jsfichier.

    ```Shell
    tsc --init
    ```

1. Ouvrez **./tsconfig.jsdans** un éditeur de texte et a apporter les modifications suivantes.

    - Changez `target` la valeur en `es6` .
    - Désécommant la `outDir` valeur et définissez-la sur `./dist` .
    - Désécommant la `rootDir` valeur et définissez-la sur `./src` .

1. Ouvrez **./package.jset** ajoutez la propriété suivante au JSON.

    ```json
    "scripts": {
      "start": "nodemon ./src/server.ts",
      "build": "tsc --project ./"
    },
    ```

1. Exécutez la commande suivante pour générer et installer des certificats de développement pour votre add-in.

    ```Shell
    npx office-addin-dev-certs install
    ```

    Si vous êtes invité à confirmer, confirmez les actions. Une fois la commande terminée, vous verrez une sortie semblable à celle-ci.

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. Créez un fichier nommé **.env** à la racine de votre projet et ajoutez le code suivant.

    :::code language="ini" source="../demo/graph-tutorial/example.env":::

    Remplacez par le chemin d’accès à localhost.crt et par le chemin d’accès à la sortie `PATH_TO_LOCALHOST.CRT` `PATH_TO_LOCALHOST.KEY` localhost.key par la commande précédente.

1. Créez un répertoire à la racine de votre projet nommé **src**.

1. Créez deux répertoires dans le répertoire **./src** : **le addin** et **l’api.**

1. Créez un fichier nommé **auth.ts** dans le répertoire **./src/api** et ajoutez le code suivant.

    ```typescript
    import Router from 'express-promise-router';

    const authRouter = Router();

    // TODO: Implement this router

    export default authRouter;
    ```

1. Créez un fichier nommé **graph.ts** dans le répertoire **./src/api** et ajoutez le code suivant.

    ```typescript
    import Router from 'express-promise-router';

    const graphRouter = Router();

    // TODO: Implement this router

    export default graphRouter;
    ```

1. Créez un fichier nommé **server.ts dans** le répertoire **./src** et ajoutez le code suivant.

    :::code language="typescript" source="../demo/graph-tutorial/src/server.ts" id="ServerSnippet":::

## <a name="create-the-add-in"></a>Créer le complément

1. Créez un fichier nommé **taskpane.html** dans le répertoire **./src/addin** et ajoutez le code suivant.

    :::code language="html" source="../demo/graph-tutorial/src/addin/taskpane.html" id="TaskPaneHtmlSnippet":::

1. Créez un fichier nommé **taskpane.css** dans le répertoire **./src/addin** et ajoutez le code suivant.

    :::code language="css" source="../demo/graph-tutorial/src/addin/taskpane.css":::

1. Créez un fichier nommé **taskpane.js** dans le répertoire **./src/addin** et ajoutez le code suivant.

    ```javascript
    // TEMPORARY CODE TO VERIFY ADD-IN LOADS
    'use strict';

    Office.onReady(info => {
      if (info.host === Office.HostType.Excel) {
        $(function() {
          $('p').text('Hello World!!');
        });
      }
    });
    ```

1. Créez un répertoire dans le répertoire **.src/addin** nommé **assets**.

1. Ajoutez trois fichiers PNG dans ce répertoire, conformément au tableau suivant.

    | Nom de fichier   | Taille en pixels |
    |-------------|----------------|
    | icon-80.png | 80x80          |
    | icon-32.png | 32x32          |
    | icon-16.png | 16x16          |

    > [!NOTE]
    > Vous pouvez utiliser n’importe quelle image que vous souhaitez pour cette étape. Vous pouvez également télécharger les images utilisées dans cet exemple directement à partir [de GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets)

1. Créez un répertoire à la racine du projet nommé **manifeste**.

1. Créez un fichier nommé **manifest.xml** dans le **dossier ./manifest** et ajoutez le code suivant. Remplacez `NEW_GUID_HERE` par un nouveau GUID, comme `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .

    :::code language="xml" source="../demo/graph-tutorial/manifest/manifest.xml":::

## <a name="side-load-the-add-in-in-excel"></a>Chargement d’une version de version latéral du module dans Excel

1. Démarrez le serveur en exécutant la commande suivante.

    ```Shell
    yarn start
    ```

1. Ouvrez votre navigateur et accédez à `https://localhost:3000/taskpane.html` . Vous devriez voir un `Not loaded` message.

1. Dans votre navigateur, Office.com [et](https://www.office.com/) connectez-vous. Sélectionnez **Créer** dans la barre d’outils de gauche, puis sélectionnez **Feuille de calcul.**

    ![Capture d’écran du menu Créer sur Office.com](images/office-select-excel.png)

1. Sélectionnez **l’onglet** Insérer, puis **sélectionnez Les add-ins Office.**

1. Select **Upload My Add-in,** then select **Browse**. Téléchargez **votre fichier ./manifest/manifest.xml.**

1. Sélectionnez **le bouton Importer** le calendrier sous **l’onglet Accueil** pour ouvrir lepane des tâches.

    ![Capture d’écran du bouton Importer le calendrier sous l’onglet Accueil](images/get-started.png)

1. Une fois lepane des tâches ouvert, vous devez voir un `Hello World!` message.

    ![Capture d’écran du message Hello World](images/hello-world.png)
