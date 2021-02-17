---
ms.openlocfilehash: fed56663591ac36e4defcae3a8d0a222f86e3026
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274285"
---
# <a name="how-to-run-the-completed-project"></a>Comment exécuter le projet terminé

## <a name="prerequisites"></a>Configuration requise

Pour exécuter le projet terminé dans ce dossier, vous devez :

- [Node.js](https://nodejs.org) [et Sons installés](https://yarnpkg.com/) sur votre ordinateur de développement. (**Remarque : ce** didacticiel a été écrit avec Node version 14.15.0 et La version 1.22.0 de Ce didacticiel. Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.)
- Soit un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com, soit un compte scolaire ou scolaire Microsoft.

Si vous n’avez pas de compte Microsoft, deux options s’offrent à vous pour obtenir un compte gratuit :

- Vous pouvez [vous inscrire à un nouveau compte Microsoft personnel.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Vous pouvez vous inscrire au programme pour les développeurs [Office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement Office 365 gratuit.

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a>Inscrire une application web auprès du Centre d’administration Azure Active Directory

1. Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com). Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.

1. Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.

    ![Une capture d’écran des inscriptions d’applications ](/tutorial/images/app-registrations.png)

1. Sélectionnez **Nouvelle inscription**. Sur la page **Inscrire une application**, définissez les valeurs comme suit.

    - Définissez le **Nom** sur `Office Add-in Graph Tutorial`.
    - Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.
    - Sous **URI de redirection**, définissez la première flèche déroulante sur `Single-page application (SPA)`, et la valeur sur `https://localhost:3000/consent.html`.

    ![Capture d’écran de la page Inscrire une application](/tutorial/images/register-an-app.png)

1. Sélectionner **Inscription**. Dans la page Didacticiel Graph du **add-in Office,** copiez la valeur de l’ID de l’application **(client)** et enregistrez-la. Vous en aurez besoin à l’étape suivante.

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](/tutorial/images/application-id.png)

1. Sélectionnez **Certificats et secrets** sous **Gérer**. Sélectionnez le bouton **Nouveau secret client**. Entrez une valeur dans **Description**, sélectionnez une des options pour **Expire le**, puis sélectionnez **Ajouter**.

1. Copiez la valeur du secret client avant de quitter cette page. Vous en aurez besoin à l’étape suivante.

    > [!IMPORTANT]
    > Ce secret client n’apparaîtra plus jamais, aussi veillez à le copier maintenant.

1. Sélectionnez **les autorisations d’API** sous **Gérer,** puis **sélectionnez Ajouter une autorisation.**

1. Sélectionnez **Microsoft Graph,** puis **Autorisations déléguées.**

1. Sélectionnez les autorisations suivantes, puis **sélectionnez Ajouter des autorisations.**

    - **Calendars.ReadWrite** : cela permettra à l’application de lire et d’écrire dans le calendrier de l’utilisateur.
    - **MailboxSettings.Read** : cela permettra à l’application d’obtenir le fuseau horaire de l’utilisateur à partir de ses paramètres de boîte aux lettres.

    ![Capture d’écran des autorisations configurées](/tutorial/images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a>Configuration de l' sign-on unique du add-in Office

Mettez à jour l’inscription de l’application pour prendre en charge [l' sign-in unique (SSO) Office.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)

1. Sélectionnez **Exposer une API.** Dans les **étendues définies par cette** section API, **sélectionnez Ajouter une étendue.** Lorsque vous y sont invités pour définir un **URI d’ID** d’application, définissez la valeur sur , en remplaçant `api://localhost:3000/YOUR_APP_ID_HERE` par `YOUR_APP_ID_HERE` l’ID d’application. Choose **Save and continue**.

1. Remplissez les champs comme suit et sélectionnez **Ajouter une étendue.**

    - **Nom de l’étendue :**`access_as_user`
    - **Qui peut donner son consentement ? : Administrateurs et utilisateurs**
    - **Nom complet du consentement de l’administrateur :**`Access the app as the user`
    - **Description du consentement de l’administrateur :**`Allows Office Add-ins to call the app's web APIs as the current user.`
    - **Nom complet du consentement de l’utilisateur :**`Access the app as you`
    - **Description du consentement de l’utilisateur :**`Allows Office Add-ins to call the app's web APIs as you.`
    - **État : activé**

    ![Capture d’écran du formulaire Ajouter une étendue](/tutorial/images/add-scope.png)

1. Dans la section **Applications clientes autorisées,** **sélectionnez Ajouter une application cliente.** Entrez un ID client dans la liste suivante, activez l’étendue sous **Étendues autorisées,** puis **sélectionnez Ajouter une application.** Répétez ce processus pour chacun des ID clients de la liste.

    - `d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)
    - `ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)
    - `57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office sur le web)
    - `08e18876-6177-487e-b8b5-cf950c1e598c` (Office sur le web)

## <a name="install-development-certificates"></a>Installer des certificats de développement

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

1. Copiez les chemins d’accès vers localhost.crt et localhost.key. Vous en aurez besoin à l’étape suivante.

## <a name="update-the-manifest"></a>Mise à jour du manifeste

1. Ouvrez **lemanifest.xml** et a apporté les modifications suivantes.
    1. Remplacez `NEW_GUID_HERE` par un nouveau GUID, comme `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .
    1. Remplacez toutes les instances `YOUR_APP_ID_HERE` par l’ID d’application de l’inscription de votre application.

## <a name="configure-the-sample"></a>Configurer l’exemple

1. Renommons `example.env` le fichier `.env` .
1. Modifiez `.env` le fichier et a apporté les modifications suivantes.
    1. Remplacez `YOUR_APP_ID_HERE` par **l’ID d’application** que vous avez obtenu à partir du portail d’inscription des applications.
    1. `YOUR_CLIENT_SECRET_HERE`Remplacez-la par la secret client que vous avez obtenu à partir du portail d’inscription des applications.
    1. Remplacez `PATH_TO_LOCALHOST.CRT` par le chemin d’accès à votre fichier localhost.crt à partir de la sortie de la `npx office-addin-dev-certs install` commande.
    1. Remplacez `PATH_TO_LOCALHOST.KEY` par le chemin d’accès à votre fichier localhost.key à partir de la sortie de la `npx office-addin-dev-certs install` commande.

1. Renommons `config.example.js` le fichier `config.js` .
1. Modifiez `config.js` le fichier et a apporter les modifications suivantes.
    1. Remplacez `YOUR_APP_ID_HERE` par **l’ID d’application** que vous avez obtenu à partir du portail d’inscription des applications.
1. Dans votre interface de ligne de commande, accédez à ce répertoire et exécutez la commande suivante pour installer les conditions requises.

    ```Shell
    yarn install
    ```

## <a name="run-the-sample"></a>Exécution de l’exemple

1. Exécutez la commande suivante dans votre CLI pour démarrer l’application.

    ```Shell
    yarn start
    ```

1. Dans votre navigateur, Office.com [et](https://www.office.com/) connectez-vous. Sélectionnez **Créer** dans la barre d’outils de gauche, puis sélectionnez **Feuille de calcul.**

    ![Capture d’écran du menu Créer sur Office.com](/tutorial/images/office-select-excel.png)

1. Sélectionnez **l’onglet** Insérer, puis **sélectionnez Les add-ins Office.**

1. Select **Upload My Add-in,** then select **Browse**. Téléchargez **votremanifest.xml** de données.

1. Sélectionnez **le bouton Importer** le calendrier sous **l’onglet Accueil** pour ouvrir lepane des tâches.

    ![Capture d’écran du bouton Importer le calendrier sous l’onglet Accueil](/tutorial/images/get-started.png)
