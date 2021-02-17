---
ms.openlocfilehash: 70df2dfceb1d2df527acfecab894b28019c6febb
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274293"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="31469-101">Dans cet exercice, vous allez créer une solution de add-in Office à l’aide [d’Express](http://expressjs.com/).</span><span class="sxs-lookup"><span data-stu-id="31469-101">In this exercise you will create an Office Add-in solution using [Express](http://expressjs.com/).</span></span> <span data-ttu-id="31469-102">La solution se compose de deux parties.</span><span class="sxs-lookup"><span data-stu-id="31469-102">The solution will consist of two parts.</span></span>

- <span data-ttu-id="31469-103">Le add-in, implémenté en tant que fichiers HTML et JavaScript statiques.</span><span class="sxs-lookup"><span data-stu-id="31469-103">The add-in, implemented as static HTML and JavaScript files.</span></span>
- <span data-ttu-id="31469-104">Un Node.js/Express qui sert le add-in et implémente une API web pour récupérer des données pour le add-in.</span><span class="sxs-lookup"><span data-stu-id="31469-104">A Node.js/Express server that serves the add-in and implements a web API to retrieve data for the add-in.</span></span>

## <a name="create-the-server"></a><span data-ttu-id="31469-105">Créer le serveur</span><span class="sxs-lookup"><span data-stu-id="31469-105">Create the server</span></span>

1. <span data-ttu-id="31469-106">Ouvrez votre interface de ligne de commande (CLI), accédez à un répertoire dans lequel vous souhaitez créer votre projet et exécutez la commande suivante pour générer une package.jssur le fichier.</span><span class="sxs-lookup"><span data-stu-id="31469-106">Open your command-line interface (CLI), navigate to a directory where you want to create your project, and run the following command to generate a package.json file.</span></span>

    ```Shell
    yarn init
    ```

    <span data-ttu-id="31469-107">Entrez des valeurs pour les invites selon le cas.</span><span class="sxs-lookup"><span data-stu-id="31469-107">Enter values for the prompts as appropriate.</span></span> <span data-ttu-id="31469-108">Si vous n’êtes pas sûr, les valeurs par défaut sont bonnes.</span><span class="sxs-lookup"><span data-stu-id="31469-108">If you're unsure, the default values are fine.</span></span>

1. <span data-ttu-id="31469-109">Exécutez les commandes suivantes pour installer les dépendances.</span><span class="sxs-lookup"><span data-stu-id="31469-109">Run the following commands to install dependencies.</span></span>

    ```Shell
    yarn add express@4.17.1 express-promise-router@4.0.1 dotenv@8.2.0 node-fetch@2.6.1 jsonwebtoken@8.5.1@
    yarn add jwks-rsa@1.11.0 @azure/msal-node@1.0.0-beta.1 @microsoft/microsoft-graph-client@2.1.1
    yarn add date-fns@2.16.1 date-fns-tz@1.0.12 isomorphic-fetch@3.0.0 windows-iana@4.2.1
    yarn add -D typescript@4.0.5 ts-node@9.0.0 nodemon@2.0.6 @types/node@14.14.7 @types/express@4.17.9
    yarn add -D @types/node-fetch@2.5.7 @types/jsonwebtoken@8.5.0 @types/microsoft-graph@1.26.0
    yarn add -D @types/office-js@1.0.147 @types/jquery@3.5.4 @types/isomorphic-fetch@0.0.35
    ```

1. <span data-ttu-id="31469-110">Exécutez la commande suivante pour générer une tsconfig.jsfichier.</span><span class="sxs-lookup"><span data-stu-id="31469-110">Run the following command to generate a tsconfig.json file.</span></span>

    ```Shell
    tsc --init
    ```

1. <span data-ttu-id="31469-111">Ouvrez **./tsconfig.jsdans** un éditeur de texte et a apporter les modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="31469-111">Open **./tsconfig.json** in a text editor and make the following changes.</span></span>

    - <span data-ttu-id="31469-112">Changez `target` la valeur en `es6` .</span><span class="sxs-lookup"><span data-stu-id="31469-112">Change the `target` value to `es6`.</span></span>
    - <span data-ttu-id="31469-113">Désécommant la `outDir` valeur et définissez-la sur `./dist` .</span><span class="sxs-lookup"><span data-stu-id="31469-113">Uncomment the `outDir` value and set it to `./dist`.</span></span>
    - <span data-ttu-id="31469-114">Désécommant la `rootDir` valeur et définissez-la sur `./src` .</span><span class="sxs-lookup"><span data-stu-id="31469-114">Uncomment the `rootDir` value and set it to `./src`.</span></span>

1. <span data-ttu-id="31469-115">Ouvrez **./package.jset** ajoutez la propriété suivante au JSON.</span><span class="sxs-lookup"><span data-stu-id="31469-115">Open **./package.json** and add the following property to the JSON.</span></span>

    ```json
    "scripts": {
      "start": "nodemon ./src/server.ts",
      "build": "tsc --project ./"
    },
    ```

1. <span data-ttu-id="31469-116">Exécutez la commande suivante pour générer et installer des certificats de développement pour votre add-in.</span><span class="sxs-lookup"><span data-stu-id="31469-116">Run the following command to generate and install development certificates for your add-in.</span></span>

    ```Shell
    npx office-addin-dev-certs install
    ```

    <span data-ttu-id="31469-117">Si vous êtes invité à confirmer, confirmez les actions.</span><span class="sxs-lookup"><span data-stu-id="31469-117">If prompted for confirmation, confirm the actions.</span></span> <span data-ttu-id="31469-118">Une fois la commande terminée, vous verrez une sortie semblable à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="31469-118">Once the command completes, you will see output similar to the following.</span></span>

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. <span data-ttu-id="31469-119">Créez un fichier nommé **.env** à la racine de votre projet et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-119">Create a new file named **.env** in the root of your project and add the following code.</span></span>

    :::code language="ini" source="../demo/graph-tutorial/example.env":::

    <span data-ttu-id="31469-120">Remplacez par le chemin d’accès à localhost.crt et par le chemin d’accès à la sortie `PATH_TO_LOCALHOST.CRT` `PATH_TO_LOCALHOST.KEY` localhost.key par la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="31469-120">Replace `PATH_TO_LOCALHOST.CRT` with the path to localhost.crt and `PATH_TO_LOCALHOST.KEY` with the path to localhost.key output by the previous command.</span></span>

1. <span data-ttu-id="31469-121">Créez un répertoire à la racine de votre projet nommé **src**.</span><span class="sxs-lookup"><span data-stu-id="31469-121">Create a new directory in the root of your project named **src**.</span></span>

1. <span data-ttu-id="31469-122">Créez deux répertoires dans le répertoire **./src** : **le addin** et **l’api.**</span><span class="sxs-lookup"><span data-stu-id="31469-122">Create two directories in the **./src** directory: **addin** and **api**.</span></span>

1. <span data-ttu-id="31469-123">Créez un fichier nommé **auth.ts** dans le répertoire **./src/api** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-123">Create a new file named **auth.ts** in the **./src/api** directory and add the following code.</span></span>

    ```typescript
    import Router from 'express-promise-router';

    const authRouter = Router();

    // TODO: Implement this router

    export default authRouter;
    ```

1. <span data-ttu-id="31469-124">Créez un fichier nommé **graph.ts** dans le répertoire **./src/api** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-124">Create a new file named **graph.ts** in the **./src/api** directory and add the following code.</span></span>

    ```typescript
    import Router from 'express-promise-router';

    const graphRouter = Router();

    // TODO: Implement this router

    export default graphRouter;
    ```

1. <span data-ttu-id="31469-125">Créez un fichier nommé **server.ts dans** le répertoire **./src** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-125">Create a new file named **server.ts** in the **./src** directory and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/server.ts" id="ServerSnippet":::

## <a name="create-the-add-in"></a><span data-ttu-id="31469-126">Créer le complément</span><span class="sxs-lookup"><span data-stu-id="31469-126">Create the add-in</span></span>

1. <span data-ttu-id="31469-127">Créez un fichier nommé **taskpane.html** dans le répertoire **./src/addin** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-127">Create a new file named **taskpane.html** in the **./src/addin** directory and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/addin/taskpane.html" id="TaskPaneHtmlSnippet":::

1. <span data-ttu-id="31469-128">Créez un fichier nommé **taskpane.css** dans le répertoire **./src/addin** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-128">Create a new file named **taskpane.css** in the **./src/addin** directory and add the following code.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/addin/taskpane.css":::

1. <span data-ttu-id="31469-129">Créez un fichier nommé **taskpane.js** dans le répertoire **./src/addin** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-129">Create a new file named **taskpane.js** in the **./src/addin** directory and add the following code.</span></span>

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

1. <span data-ttu-id="31469-130">Créez un répertoire dans le répertoire **.src/addin** nommé **assets**.</span><span class="sxs-lookup"><span data-stu-id="31469-130">Create a new directory in the **.src/addin** directory named **assets**.</span></span>

1. <span data-ttu-id="31469-131">Ajoutez trois fichiers PNG dans ce répertoire, conformément au tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-131">Add three PNG files in this directory according to the following table.</span></span>

    | <span data-ttu-id="31469-132">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="31469-132">File name</span></span>   | <span data-ttu-id="31469-133">Taille en pixels</span><span class="sxs-lookup"><span data-stu-id="31469-133">Size in pixels</span></span> |
    |-------------|----------------|
    | <span data-ttu-id="31469-134">icon-80.png</span><span class="sxs-lookup"><span data-stu-id="31469-134">icon-80.png</span></span> | <span data-ttu-id="31469-135">80x80</span><span class="sxs-lookup"><span data-stu-id="31469-135">80x80</span></span>          |
    | <span data-ttu-id="31469-136">icon-32.png</span><span class="sxs-lookup"><span data-stu-id="31469-136">icon-32.png</span></span> | <span data-ttu-id="31469-137">32x32</span><span class="sxs-lookup"><span data-stu-id="31469-137">32x32</span></span>          |
    | <span data-ttu-id="31469-138">icon-16.png</span><span class="sxs-lookup"><span data-stu-id="31469-138">icon-16.png</span></span> | <span data-ttu-id="31469-139">16x16</span><span class="sxs-lookup"><span data-stu-id="31469-139">16x16</span></span>          |

    > [!NOTE]
    > <span data-ttu-id="31469-140">Vous pouvez utiliser n’importe quelle image que vous souhaitez pour cette étape.</span><span class="sxs-lookup"><span data-stu-id="31469-140">You can use any image you want for this step.</span></span> <span data-ttu-id="31469-141">Vous pouvez également télécharger les images utilisées dans cet exemple directement à partir [de GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets)</span><span class="sxs-lookup"><span data-stu-id="31469-141">You can also download the images used in this sample directly from [GitHub](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets).</span></span>

1. <span data-ttu-id="31469-142">Créez un répertoire à la racine du projet nommé **manifeste**.</span><span class="sxs-lookup"><span data-stu-id="31469-142">Create a new directory in the root of the project named **manifest**.</span></span>

1. <span data-ttu-id="31469-143">Créez un fichier nommé **manifest.xml** dans le **dossier ./manifest** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="31469-143">Create a new file named **manifest.xml** in the **./manifest** folder and add the following code.</span></span> <span data-ttu-id="31469-144">Remplacez `NEW_GUID_HERE` par un nouveau GUID, comme `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .</span><span class="sxs-lookup"><span data-stu-id="31469-144">Replace `NEW_GUID_HERE` with a new GUID, like `b4fa03b8-1eb6-4e8b-a380-e0476be9e019`.</span></span>

    :::code language="xml" source="../demo/graph-tutorial/manifest/manifest.xml":::

## <a name="side-load-the-add-in-in-excel"></a><span data-ttu-id="31469-145">Chargement d’une version de version latéral du module dans Excel</span><span class="sxs-lookup"><span data-stu-id="31469-145">Side-load the add-in in Excel</span></span>

1. <span data-ttu-id="31469-146">Démarrez le serveur en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="31469-146">Start the server by running the following command.</span></span>

    ```Shell
    yarn start
    ```

1. <span data-ttu-id="31469-147">Ouvrez votre navigateur et accédez à `https://localhost:3000/taskpane.html` .</span><span class="sxs-lookup"><span data-stu-id="31469-147">Open your browser and browse to `https://localhost:3000/taskpane.html`.</span></span> <span data-ttu-id="31469-148">Vous devriez voir un `Not loaded` message.</span><span class="sxs-lookup"><span data-stu-id="31469-148">You should see a `Not loaded` message.</span></span>

1. <span data-ttu-id="31469-149">Dans votre navigateur, Office.com [et](https://www.office.com/) connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="31469-149">In your browser, go to [Office.com](https://www.office.com/) and sign in.</span></span> <span data-ttu-id="31469-150">Sélectionnez **Créer** dans la barre d’outils de gauche, puis sélectionnez **Feuille de calcul.**</span><span class="sxs-lookup"><span data-stu-id="31469-150">Select **Create** in the left-hand toolbar, then select **Spreadsheet**.</span></span>

    ![Capture d’écran du menu Créer sur Office.com](images/office-select-excel.png)

1. <span data-ttu-id="31469-152">Sélectionnez **l’onglet** Insérer, puis **sélectionnez Les add-ins Office.**</span><span class="sxs-lookup"><span data-stu-id="31469-152">Select the **Insert** tab, then select **Office Add-ins**.</span></span>

1. <span data-ttu-id="31469-153">Select **Upload My Add-in,** then select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="31469-153">Select **Upload My Add-in**, then select **Browse**.</span></span> <span data-ttu-id="31469-154">Téléchargez **votre fichier ./manifest/manifest.xml.**</span><span class="sxs-lookup"><span data-stu-id="31469-154">Upload your **./manifest/manifest.xml** file.</span></span>

1. <span data-ttu-id="31469-155">Sélectionnez **le bouton Importer** le calendrier sous **l’onglet Accueil** pour ouvrir lepane des tâches.</span><span class="sxs-lookup"><span data-stu-id="31469-155">Select the **Import Calendar** button on the **Home** tab to open the taskpane.</span></span>

    ![Capture d’écran du bouton Importer le calendrier sous l’onglet Accueil](images/get-started.png)

1. <span data-ttu-id="31469-157">Une fois lepane des tâches ouvert, vous devez voir un `Hello World!` message.</span><span class="sxs-lookup"><span data-stu-id="31469-157">After the taskpane opens, you should see a `Hello World!` message.</span></span>

    ![Capture d’écran du message Hello World](images/hello-world.png)
