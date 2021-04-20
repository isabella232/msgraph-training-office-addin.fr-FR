---
ms.openlocfilehash: 89bc4baff47ae895c7c0dfd34a8f8d4d0da091f5
ms.sourcegitcommit: 8a65c826f6b229c287a782d784b6d9629aa5a3d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2021
ms.locfileid: "51899431"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="fad3b-101">Dans cet exercice, vous allez créer une inscription d'application web Azure AD à l'aide du Centre d'administration Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fad3b-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="fad3b-102">Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fad3b-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="fad3b-103">Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="fad3b-104">Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="fad3b-105">Une capture d’écran des inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="fad3b-105">A screenshot of the App registrations</span></span> ](images/app-registrations.png)

1. <span data-ttu-id="fad3b-106">Sélectionnez **Nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-106">Select **New registration**.</span></span> <span data-ttu-id="fad3b-107">Sur la page **Inscrire une application**, définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="fad3b-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="fad3b-108">Définissez le **Nom** sur `Office Add-in Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="fad3b-108">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="fad3b-109">Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="fad3b-110">Sous **URI de redirection**, définissez la première flèche déroulante sur `Single-page application (SPA)`, et la valeur sur `https://localhost:3000/consent.html`.</span><span class="sxs-lookup"><span data-stu-id="fad3b-110">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Capture d’écran de la page Inscrire une application](images/register-an-app.png)

1. <span data-ttu-id="fad3b-112">Sélectionner **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-112">Select **Register**.</span></span> <span data-ttu-id="fad3b-113">Dans la page Didacticiel Graph du **add-in Office,** copiez la valeur de **l'ID d'application (client)** et enregistrez-la. Vous en aurez besoin à l'étape suivante.</span><span class="sxs-lookup"><span data-stu-id="fad3b-113">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](images/application-id.png)

1. <span data-ttu-id="fad3b-115">Sous **Gérer**, sélectionnez **Authentification**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-115">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="fad3b-116">Recherchez la section **d'octroi** implicite et activez **les jetons d'accès** et **les jetons d'ID.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-116">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="fad3b-117">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-117">Select **Save**.</span></span>

    ![Une capture d’écran de la rubrique octroi implicite](./images/aad-implicit-grant.png)

1. <span data-ttu-id="fad3b-119">Sélectionnez **Certificats et secrets** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-119">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="fad3b-120">Sélectionnez le bouton **Nouveau secret client**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-120">Select the **New client secret** button.</span></span> <span data-ttu-id="fad3b-121">Entrez une valeur dans **Description**, sélectionnez une des options pour **Expire le**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fad3b-121">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="fad3b-122">Copiez la valeur du secret client avant de quitter cette page.</span><span class="sxs-lookup"><span data-stu-id="fad3b-122">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="fad3b-123">Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="fad3b-123">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fad3b-124">Ce secret client n’apparaîtra plus jamais, aussi veillez à le copier maintenant.</span><span class="sxs-lookup"><span data-stu-id="fad3b-124">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="fad3b-125">Sélectionnez **les autorisations d'API** sous **Gérer,** puis **sélectionnez Ajouter une autorisation.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-125">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="fad3b-126">Sélectionnez **Microsoft Graph,** puis **Autorisations déléguées.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-126">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="fad3b-127">Sélectionnez les autorisations suivantes, puis **sélectionnez Ajouter des autorisations.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-127">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="fad3b-128">**offline_access** - cela permet à l'application d'actualiser les jetons d'accès lorsqu'ils expirent.</span><span class="sxs-lookup"><span data-stu-id="fad3b-128">**offline_access** - this will allow the app to refresh access tokens when they expire.</span></span>
    - <span data-ttu-id="fad3b-129">**Calendars.ReadWrite** : cela permettra à l'application de lire et d'écrire dans le calendrier de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fad3b-129">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="fad3b-130">**MailboxSettings.Read** : cela permettra à l'application d'obtenir le fuseau horaire de l'utilisateur à partir de ses paramètres de boîte aux lettres.</span><span class="sxs-lookup"><span data-stu-id="fad3b-130">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Capture d'écran des autorisations configurées](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="fad3b-132">Configuration de l' sign-on unique du add-in Office</span><span class="sxs-lookup"><span data-stu-id="fad3b-132">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="fad3b-133">Dans cette section, vous allez mettre à jour l'inscription de l'application pour prendre en charge l' [sign-on unique (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)pour office.</span><span class="sxs-lookup"><span data-stu-id="fad3b-133">In this section you'll update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="fad3b-134">Sélectionnez **Exposer une API.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-134">Select **Expose an API**.</span></span> <span data-ttu-id="fad3b-135">Dans les **étendues définies par cette** section API, **sélectionnez Ajouter une étendue.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-135">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="fad3b-136">Lorsque vous y sont invités pour définir un **URI d'ID** d'application, définissez la valeur sur , en remplaçant `api://localhost:3000/YOUR_APP_ID_HERE` par `YOUR_APP_ID_HERE` l'ID d'application.</span><span class="sxs-lookup"><span data-stu-id="fad3b-136">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="fad3b-137">Sélectionnez **Enregistrer et continuer.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-137">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="fad3b-138">Remplissez les champs comme suit et sélectionnez **Ajouter une étendue.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-138">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="fad3b-139">**Nom de l'étendue :**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="fad3b-139">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="fad3b-140">**Qui peut donner son consentement ? : Administrateurs et utilisateurs**</span><span class="sxs-lookup"><span data-stu-id="fad3b-140">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="fad3b-141">**Nom complet du consentement de l'administrateur :**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="fad3b-141">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="fad3b-142">**Description du consentement de l'administrateur :**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="fad3b-142">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="fad3b-143">**Nom complet du consentement de l'utilisateur :**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="fad3b-143">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="fad3b-144">**Description du consentement de l'utilisateur :**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="fad3b-144">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="fad3b-145">**État : activé**</span><span class="sxs-lookup"><span data-stu-id="fad3b-145">**State: Enabled**</span></span>

    ![Capture d'écran du formulaire Ajouter une étendue](images/add-scope.png)

1. <span data-ttu-id="fad3b-147">Dans la section **Applications clientes autorisées,** **sélectionnez Ajouter une application cliente.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-147">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="fad3b-148">Entrez un ID client dans la liste suivante, activez l'étendue sous **Étendues autorisées,** puis **sélectionnez Ajouter une application.**</span><span class="sxs-lookup"><span data-stu-id="fad3b-148">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="fad3b-149">Répétez ce processus pour chacun des ID clients de la liste.</span><span class="sxs-lookup"><span data-stu-id="fad3b-149">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="fad3b-150">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="fad3b-150">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="fad3b-151">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="fad3b-151">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="fad3b-152">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office sur le web)</span><span class="sxs-lookup"><span data-stu-id="fad3b-152">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="fad3b-153">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office sur le web)</span><span class="sxs-lookup"><span data-stu-id="fad3b-153">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>
