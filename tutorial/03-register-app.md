---
ms.openlocfilehash: a336095a238eefeae22dac86d29e3140e8d94bf1
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274262"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="32c15-101">Dans cet exercice, vous allez créer une inscription d’application web Azure AD à l’aide du Centre d’administration Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32c15-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="32c15-102">Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32c15-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="32c15-103">Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="32c15-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="32c15-104">Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="32c15-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="32c15-105">Une capture d’écran des inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="32c15-105">A screenshot of the App registrations</span></span> ](images/app-registrations.png)

1. <span data-ttu-id="32c15-106">Sélectionnez **Nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="32c15-106">Select **New registration**.</span></span> <span data-ttu-id="32c15-107">Sur la page **Inscrire une application**, définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="32c15-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="32c15-108">Définissez le **Nom** sur `Office Add-in Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="32c15-108">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="32c15-109">Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="32c15-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="32c15-110">Sous **URI de redirection**, définissez la première flèche déroulante sur `Single-page application (SPA)`, et la valeur sur `https://localhost:3000/consent.html`.</span><span class="sxs-lookup"><span data-stu-id="32c15-110">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Capture d’écran de la page Inscrire une application](images/register-an-app.png)

1. <span data-ttu-id="32c15-112">Sélectionner **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="32c15-112">Select **Register**.</span></span> <span data-ttu-id="32c15-113">Dans la page Didacticiel Graph du **add-in Office,** copiez la valeur de l’ID de l’application **(client)** et enregistrez-la. Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="32c15-113">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](images/application-id.png)

1. <span data-ttu-id="32c15-115">Sélectionnez **Certificats et secrets** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="32c15-115">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="32c15-116">Sélectionnez le bouton **Nouveau secret client**.</span><span class="sxs-lookup"><span data-stu-id="32c15-116">Select the **New client secret** button.</span></span> <span data-ttu-id="32c15-117">Entrez une valeur dans **Description**, sélectionnez une des options pour **Expire le**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="32c15-117">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="32c15-118">Copiez la valeur du secret client avant de quitter cette page.</span><span class="sxs-lookup"><span data-stu-id="32c15-118">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="32c15-119">Vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="32c15-119">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="32c15-120">Ce secret client n’apparaîtra plus jamais, aussi veillez à le copier maintenant.</span><span class="sxs-lookup"><span data-stu-id="32c15-120">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="32c15-121">Sélectionnez **les autorisations d’API** sous **Gérer,** puis **sélectionnez Ajouter une autorisation.**</span><span class="sxs-lookup"><span data-stu-id="32c15-121">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="32c15-122">Sélectionnez **Microsoft Graph,** puis **Autorisations déléguées.**</span><span class="sxs-lookup"><span data-stu-id="32c15-122">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="32c15-123">Sélectionnez les autorisations suivantes, puis **sélectionnez Ajouter des autorisations.**</span><span class="sxs-lookup"><span data-stu-id="32c15-123">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="32c15-124">**offline_access** - cela permet à l’application d’actualiser les jetons d’accès lorsqu’ils expirent.</span><span class="sxs-lookup"><span data-stu-id="32c15-124">**offline_access** - this will allow the app to refresh access tokens when they expire.</span></span>
    - <span data-ttu-id="32c15-125">**Calendars.ReadWrite** : cela permettra à l’application de lire et d’écrire dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32c15-125">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="32c15-126">**MailboxSettings.Read** : cela permettra à l’application d’obtenir le fuseau horaire de l’utilisateur à partir de ses paramètres de boîte aux lettres.</span><span class="sxs-lookup"><span data-stu-id="32c15-126">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Capture d’écran des autorisations configurées](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="32c15-128">Configuration de l' sign-on unique du add-in Office</span><span class="sxs-lookup"><span data-stu-id="32c15-128">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="32c15-129">Dans cette section, vous allez mettre à jour l’inscription de l’application pour prendre en charge l' [sign-in unique (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)Office.</span><span class="sxs-lookup"><span data-stu-id="32c15-129">In this section you'll update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="32c15-130">Sélectionnez **Exposer une API.**</span><span class="sxs-lookup"><span data-stu-id="32c15-130">Select **Expose an API**.</span></span> <span data-ttu-id="32c15-131">Dans les **étendues définies par cette** section API, **sélectionnez Ajouter une étendue.**</span><span class="sxs-lookup"><span data-stu-id="32c15-131">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="32c15-132">Lorsque vous y sont invités pour définir un **URI d’ID** d’application, définissez la valeur sur , en remplaçant `api://localhost:3000/YOUR_APP_ID_HERE` par `YOUR_APP_ID_HERE` l’ID d’application.</span><span class="sxs-lookup"><span data-stu-id="32c15-132">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="32c15-133">Choose **Save and continue**.</span><span class="sxs-lookup"><span data-stu-id="32c15-133">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="32c15-134">Remplissez les champs comme suit et sélectionnez **Ajouter une étendue.**</span><span class="sxs-lookup"><span data-stu-id="32c15-134">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="32c15-135">**Nom de l’étendue :**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="32c15-135">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="32c15-136">**Qui peut donner son consentement ? : Administrateurs et utilisateurs**</span><span class="sxs-lookup"><span data-stu-id="32c15-136">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="32c15-137">**Nom complet du consentement de l’administrateur :**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="32c15-137">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="32c15-138">**Description du consentement de l’administrateur :**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="32c15-138">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="32c15-139">**Nom complet du consentement de l’utilisateur :**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="32c15-139">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="32c15-140">**Description du consentement de l’utilisateur :**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="32c15-140">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="32c15-141">**État : activé**</span><span class="sxs-lookup"><span data-stu-id="32c15-141">**State: Enabled**</span></span>

    ![Capture d’écran du formulaire Ajouter une étendue](images/add-scope.png)

1. <span data-ttu-id="32c15-143">Dans la section **Applications clientes autorisées,** **sélectionnez Ajouter une application cliente.**</span><span class="sxs-lookup"><span data-stu-id="32c15-143">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="32c15-144">Entrez un ID client dans la liste suivante, activez l’étendue sous **Étendues autorisées,** puis **sélectionnez Ajouter une application.**</span><span class="sxs-lookup"><span data-stu-id="32c15-144">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="32c15-145">Répétez ce processus pour chacun des ID clients de la liste.</span><span class="sxs-lookup"><span data-stu-id="32c15-145">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="32c15-146">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="32c15-146">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="32c15-147">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="32c15-147">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="32c15-148">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office sur le web)</span><span class="sxs-lookup"><span data-stu-id="32c15-148">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="32c15-149">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office sur le web)</span><span class="sxs-lookup"><span data-stu-id="32c15-149">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>
