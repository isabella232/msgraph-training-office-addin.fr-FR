---
ms.openlocfilehash: fed56663591ac36e4defcae3a8d0a222f86e3026
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274285"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="16349-101">Comment exécuter le projet terminé</span><span class="sxs-lookup"><span data-stu-id="16349-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16349-102">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="16349-102">Prerequisites</span></span>

<span data-ttu-id="16349-103">Pour exécuter le projet terminé dans ce dossier, vous devez :</span><span class="sxs-lookup"><span data-stu-id="16349-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="16349-104">[Node.js](https://nodejs.org) [et Sons installés](https://yarnpkg.com/) sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="16349-104">[Node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com/) installed on your development machine.</span></span> <span data-ttu-id="16349-105">(**Remarque : ce** didacticiel a été écrit avec Node version 14.15.0 et La version 1.22.0 de Ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="16349-105">(**Note:** This tutorial was written with Node version 14.15.0 and Yarn version 1.22.0.</span></span> <span data-ttu-id="16349-106">Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.)</span><span class="sxs-lookup"><span data-stu-id="16349-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="16349-107">Soit un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com, soit un compte scolaire ou scolaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16349-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="16349-108">Si vous n’avez pas de compte Microsoft, deux options s’offrent à vous pour obtenir un compte gratuit :</span><span class="sxs-lookup"><span data-stu-id="16349-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="16349-109">Vous pouvez [vous inscrire à un nouveau compte Microsoft personnel.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)</span><span class="sxs-lookup"><span data-stu-id="16349-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="16349-110">Vous pouvez vous inscrire au programme pour les développeurs [Office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement Office 365 gratuit.</span><span class="sxs-lookup"><span data-stu-id="16349-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="16349-111">Inscrire une application web auprès du Centre d’administration Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16349-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="16349-112">Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16349-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="16349-113">Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="16349-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="16349-114">Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="16349-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="16349-115">Une capture d’écran des inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="16349-115">A screenshot of the App registrations</span></span> ](/tutorial/images/app-registrations.png)

1. <span data-ttu-id="16349-116">Sélectionnez **Nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="16349-116">Select **New registration**.</span></span> <span data-ttu-id="16349-117">Sur la page **Inscrire une application**, définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="16349-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="16349-118">Définissez le **Nom** sur `Office Add-in Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="16349-118">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="16349-119">Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="16349-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="16349-120">Sous **URI de redirection**, définissez la première flèche déroulante sur `Single-page application (SPA)`, et la valeur sur `https://localhost:3000/consent.html`.</span><span class="sxs-lookup"><span data-stu-id="16349-120">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Capture d’écran de la page Inscrire une application](/tutorial/images/register-an-app.png)

1. <span data-ttu-id="16349-122">Sélectionner **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="16349-122">Select **Register**.</span></span> <span data-ttu-id="16349-123">Dans la page Didacticiel Graph du **add-in Office,** copiez la valeur de l’ID de l’application **(client)** et enregistrez-la. Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="16349-123">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](/tutorial/images/application-id.png)

1. <span data-ttu-id="16349-125">Sélectionnez **Certificats et secrets** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="16349-125">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="16349-126">Sélectionnez le bouton **Nouveau secret client**.</span><span class="sxs-lookup"><span data-stu-id="16349-126">Select the **New client secret** button.</span></span> <span data-ttu-id="16349-127">Entrez une valeur dans **Description**, sélectionnez une des options pour **Expire le**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="16349-127">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="16349-128">Copiez la valeur du secret client avant de quitter cette page.</span><span class="sxs-lookup"><span data-stu-id="16349-128">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="16349-129">Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="16349-129">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="16349-130">Ce secret client n’apparaîtra plus jamais, aussi veillez à le copier maintenant.</span><span class="sxs-lookup"><span data-stu-id="16349-130">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="16349-131">Sélectionnez **les autorisations d’API** sous **Gérer,** puis **sélectionnez Ajouter une autorisation.**</span><span class="sxs-lookup"><span data-stu-id="16349-131">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="16349-132">Sélectionnez **Microsoft Graph,** puis **Autorisations déléguées.**</span><span class="sxs-lookup"><span data-stu-id="16349-132">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="16349-133">Sélectionnez les autorisations suivantes, puis **sélectionnez Ajouter des autorisations.**</span><span class="sxs-lookup"><span data-stu-id="16349-133">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="16349-134">**Calendars.ReadWrite** : cela permettra à l’application de lire et d’écrire dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="16349-134">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="16349-135">**MailboxSettings.Read** : cela permettra à l’application d’obtenir le fuseau horaire de l’utilisateur à partir de ses paramètres de boîte aux lettres.</span><span class="sxs-lookup"><span data-stu-id="16349-135">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Capture d’écran des autorisations configurées](/tutorial/images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="16349-137">Configuration de l' sign-on unique du add-in Office</span><span class="sxs-lookup"><span data-stu-id="16349-137">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="16349-138">Mettez à jour l’inscription de l’application pour prendre en charge [l' sign-in unique (SSO) Office.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)</span><span class="sxs-lookup"><span data-stu-id="16349-138">Update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="16349-139">Sélectionnez **Exposer une API.**</span><span class="sxs-lookup"><span data-stu-id="16349-139">Select **Expose an API**.</span></span> <span data-ttu-id="16349-140">Dans les **étendues définies par cette** section API, **sélectionnez Ajouter une étendue.**</span><span class="sxs-lookup"><span data-stu-id="16349-140">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="16349-141">Lorsque vous y sont invités pour définir un **URI d’ID** d’application, définissez la valeur sur , en remplaçant `api://localhost:3000/YOUR_APP_ID_HERE` par `YOUR_APP_ID_HERE` l’ID d’application.</span><span class="sxs-lookup"><span data-stu-id="16349-141">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="16349-142">Choose **Save and continue**.</span><span class="sxs-lookup"><span data-stu-id="16349-142">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="16349-143">Remplissez les champs comme suit et sélectionnez **Ajouter une étendue.**</span><span class="sxs-lookup"><span data-stu-id="16349-143">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="16349-144">**Nom de l’étendue :**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="16349-144">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="16349-145">**Qui peut donner son consentement ? : Administrateurs et utilisateurs**</span><span class="sxs-lookup"><span data-stu-id="16349-145">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="16349-146">**Nom complet du consentement de l’administrateur :**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="16349-146">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="16349-147">**Description du consentement de l’administrateur :**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="16349-147">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="16349-148">**Nom complet du consentement de l’utilisateur :**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="16349-148">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="16349-149">**Description du consentement de l’utilisateur :**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="16349-149">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="16349-150">**État : activé**</span><span class="sxs-lookup"><span data-stu-id="16349-150">**State: Enabled**</span></span>

    ![Capture d’écran du formulaire Ajouter une étendue](/tutorial/images/add-scope.png)

1. <span data-ttu-id="16349-152">Dans la section **Applications clientes autorisées,** **sélectionnez Ajouter une application cliente.**</span><span class="sxs-lookup"><span data-stu-id="16349-152">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="16349-153">Entrez un ID client dans la liste suivante, activez l’étendue sous **Étendues autorisées,** puis **sélectionnez Ajouter une application.**</span><span class="sxs-lookup"><span data-stu-id="16349-153">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="16349-154">Répétez ce processus pour chacun des ID clients de la liste.</span><span class="sxs-lookup"><span data-stu-id="16349-154">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="16349-155">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="16349-155">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="16349-156">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="16349-156">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="16349-157">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office sur le web)</span><span class="sxs-lookup"><span data-stu-id="16349-157">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="16349-158">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office sur le web)</span><span class="sxs-lookup"><span data-stu-id="16349-158">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>

## <a name="install-development-certificates"></a><span data-ttu-id="16349-159">Installer des certificats de développement</span><span class="sxs-lookup"><span data-stu-id="16349-159">Install development certificates</span></span>

1. <span data-ttu-id="16349-160">Exécutez la commande suivante pour générer et installer des certificats de développement pour votre add-in.</span><span class="sxs-lookup"><span data-stu-id="16349-160">Run the following command to generate and install development certificates for your add-in.</span></span>

    ```Shell
    npx office-addin-dev-certs install
    ```

    <span data-ttu-id="16349-161">Si vous êtes invité à confirmer, confirmez les actions.</span><span class="sxs-lookup"><span data-stu-id="16349-161">If prompted for confirmation, confirm the actions.</span></span> <span data-ttu-id="16349-162">Une fois la commande terminée, vous verrez une sortie semblable à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="16349-162">Once the command completes, you will see output similar to the following.</span></span>

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. <span data-ttu-id="16349-163">Copiez les chemins d’accès vers localhost.crt et localhost.key. Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="16349-163">Copy the paths to localhost.crt and localhost.key, you'll need them in the next step.</span></span>

## <a name="update-the-manifest"></a><span data-ttu-id="16349-164">Mise à jour du manifeste</span><span class="sxs-lookup"><span data-stu-id="16349-164">Update the manifest</span></span>

1. <span data-ttu-id="16349-165">Ouvrez **lemanifest.xml** et a apporté les modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="16349-165">Open the **manifest.xml** file and make the following changes.</span></span>
    1. <span data-ttu-id="16349-166">Remplacez `NEW_GUID_HERE` par un nouveau GUID, comme `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .</span><span class="sxs-lookup"><span data-stu-id="16349-166">Replace `NEW_GUID_HERE` with a new GUID, like `b4fa03b8-1eb6-4e8b-a380-e0476be9e019`.</span></span>
    1. <span data-ttu-id="16349-167">Remplacez toutes les instances `YOUR_APP_ID_HERE` par l’ID d’application de l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="16349-167">Replace all instances of `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="16349-168">Configurer l’exemple</span><span class="sxs-lookup"><span data-stu-id="16349-168">Configure the sample</span></span>

1. <span data-ttu-id="16349-169">Renommons `example.env` le fichier `.env` .</span><span class="sxs-lookup"><span data-stu-id="16349-169">Rename the `example.env` file to `.env`.</span></span>
1. <span data-ttu-id="16349-170">Modifiez `.env` le fichier et a apporté les modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="16349-170">Edit the `.env` file and make the following changes.</span></span>
    1. <span data-ttu-id="16349-171">Remplacez `YOUR_APP_ID_HERE` par **l’ID d’application** que vous avez obtenu à partir du portail d’inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="16349-171">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
    1. <span data-ttu-id="16349-172">`YOUR_CLIENT_SECRET_HERE`Remplacez-la par la secret client que vous avez obtenu à partir du portail d’inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="16349-172">Replace `YOUR_CLIENT_SECRET_HERE` with the client secret you got from the App Registration Portal.</span></span>
    1. <span data-ttu-id="16349-173">Remplacez `PATH_TO_LOCALHOST.CRT` par le chemin d’accès à votre fichier localhost.crt à partir de la sortie de la `npx office-addin-dev-certs install` commande.</span><span class="sxs-lookup"><span data-stu-id="16349-173">Replace `PATH_TO_LOCALHOST.CRT` with the path to your localhost.crt file from the output of the `npx office-addin-dev-certs install` command.</span></span>
    1. <span data-ttu-id="16349-174">Remplacez `PATH_TO_LOCALHOST.KEY` par le chemin d’accès à votre fichier localhost.key à partir de la sortie de la `npx office-addin-dev-certs install` commande.</span><span class="sxs-lookup"><span data-stu-id="16349-174">Replace `PATH_TO_LOCALHOST.KEY` with the path to your localhost.key file from the output of the `npx office-addin-dev-certs install` command.</span></span>

1. <span data-ttu-id="16349-175">Renommons `config.example.js` le fichier `config.js` .</span><span class="sxs-lookup"><span data-stu-id="16349-175">Rename the `config.example.js` file to `config.js`.</span></span>
1. <span data-ttu-id="16349-176">Modifiez `config.js` le fichier et a apporter les modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="16349-176">Edit the `config.js` file and make the following changes.</span></span>
    1. <span data-ttu-id="16349-177">Remplacez `YOUR_APP_ID_HERE` par **l’ID d’application** que vous avez obtenu à partir du portail d’inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="16349-177">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="16349-178">Dans votre interface de ligne de commande, accédez à ce répertoire et exécutez la commande suivante pour installer les conditions requises.</span><span class="sxs-lookup"><span data-stu-id="16349-178">In your command-line interface (CLI), navigate to this directory and run the following command to install requirements.</span></span>

    ```Shell
    yarn install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="16349-179">Exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="16349-179">Run the sample</span></span>

1. <span data-ttu-id="16349-180">Exécutez la commande suivante dans votre CLI pour démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="16349-180">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    yarn start
    ```

1. <span data-ttu-id="16349-181">Dans votre navigateur, Office.com [et](https://www.office.com/) connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="16349-181">In your browser, go to [Office.com](https://www.office.com/) and sign in.</span></span> <span data-ttu-id="16349-182">Sélectionnez **Créer** dans la barre d’outils de gauche, puis sélectionnez **Feuille de calcul.**</span><span class="sxs-lookup"><span data-stu-id="16349-182">Select **Create** in the left-hand toolbar, then select **Spreadsheet**.</span></span>

    ![Capture d’écran du menu Créer sur Office.com](/tutorial/images/office-select-excel.png)

1. <span data-ttu-id="16349-184">Sélectionnez **l’onglet** Insérer, puis **sélectionnez Les add-ins Office.**</span><span class="sxs-lookup"><span data-stu-id="16349-184">Select the **Insert** tab, then select **Office Add-ins**.</span></span>

1. <span data-ttu-id="16349-185">Select **Upload My Add-in,** then select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="16349-185">Select **Upload My Add-in**, then select **Browse**.</span></span> <span data-ttu-id="16349-186">Téléchargez **votremanifest.xml** de données.</span><span class="sxs-lookup"><span data-stu-id="16349-186">Upload your **manifest.xml** file.</span></span>

1. <span data-ttu-id="16349-187">Sélectionnez **le bouton Importer** le calendrier sous **l’onglet Accueil** pour ouvrir lepane des tâches.</span><span class="sxs-lookup"><span data-stu-id="16349-187">Select the **Import Calendar** button on the **Home** tab to open the taskpane.</span></span>

    ![Capture d’écran du bouton Importer le calendrier sous l’onglet Accueil](/tutorial/images/get-started.png)
