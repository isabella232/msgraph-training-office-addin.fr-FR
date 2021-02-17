---
ms.openlocfilehash: 2c323d61632c62c82af0561536656f1d68fe8938
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274289"
---
<!-- markdownlint-disable MD002 MD041 -->

Ce didacticiel vous apprend à créer un add-in Office pour Excel qui utilise l’API Microsoft Graph pour récupérer les informations de calendrier d’un utilisateur.

> [!TIP]
> Si vous préférez simplement télécharger le didacticiel terminé, vous pouvez télécharger ou cloner le référentiel [GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)

## <a name="prerequisites"></a>Configuration requise

Avant de commencer cette démonstration, vous devez avoir [ installéNode.js](https://nodejs.org) [et Sons](https://yarnpkg.com/) sur votre ordinateur de développement. Si vous n’avez pas de Node.js ou Der, consultez le lien précédent pour obtenir les options de téléchargement.

> [!NOTE]
> Les utilisateurs Windows devront peut-être installer Python et Visual Studio créer des outils pour prendre en charge les modules NPM qui doivent être compilés à partir de C/C++. Le programme Node.js installer sur Windows permet d’installer automatiquement ces outils. Vous pouvez également suivre les instructions sur [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows) .

Vous devez également avoir un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com ou un compte scolaire ou scolaire Microsoft. Si vous n’avez pas de compte Microsoft, deux options s’offrent à vous pour obtenir un compte gratuit :

- Vous pouvez [vous inscrire à un nouveau compte Microsoft personnel.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Vous pouvez vous inscrire au programme pour les développeurs [Office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement Office 365 gratuit.

> [!NOTE]
> Ce didacticiel a été écrit avec Node version 14.15.0 et La version 1.22.0. Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais elles n’ont pas été testées.

## <a name="feedback"></a>Commentaires

Veuillez nous faire part de vos commentaires sur ce didacticiel dans [le référentiel GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)
