---
ms.openlocfilehash: 2c323d61632c62c82af0561536656f1d68fe8938
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274289"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="dd0ac-101">Ce didacticiel vous apprend à créer un add-in Office pour Excel qui utilise l’API Microsoft Graph pour récupérer les informations de calendrier d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-101">This tutorial teaches you how to build an Office Add-in for Excel that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="dd0ac-102">Si vous préférez simplement télécharger le didacticiel terminé, vous pouvez télécharger ou cloner le référentiel [GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)</span><span class="sxs-lookup"><span data-stu-id="dd0ac-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-office-addin).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd0ac-103">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="dd0ac-103">Prerequisites</span></span>

<span data-ttu-id="dd0ac-104">Avant de commencer cette démonstration, vous devez avoir [ installéNode.js](https://nodejs.org) [et Sons](https://yarnpkg.com/) sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-104">Before you start this demo, you should have [Node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com/) installed on your development machine.</span></span> <span data-ttu-id="dd0ac-105">Si vous n’avez pas de Node.js ou Der, consultez le lien précédent pour obtenir les options de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-105">If you do not have Node.js or Yarn, visit the previous link for download options.</span></span>

> [!NOTE]
> <span data-ttu-id="dd0ac-106">Les utilisateurs Windows devront peut-être installer Python et Visual Studio créer des outils pour prendre en charge les modules NPM qui doivent être compilés à partir de C/C++.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-106">Windows users may need to install Python and Visual Studio Build Tools to support NPM modules that need to be compiled from C/C++.</span></span> <span data-ttu-id="dd0ac-107">Le programme Node.js installer sur Windows permet d’installer automatiquement ces outils.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-107">The Node.js installer on Windows gives an option to automatically install these tools.</span></span> <span data-ttu-id="dd0ac-108">Vous pouvez également suivre les instructions sur [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows) .</span><span class="sxs-lookup"><span data-stu-id="dd0ac-108">Alternatively, you can follow instructions at [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows).</span></span>

<span data-ttu-id="dd0ac-109">Vous devez également avoir un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com ou un compte scolaire ou scolaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="dd0ac-110">Si vous n’avez pas de compte Microsoft, deux options s’offrent à vous pour obtenir un compte gratuit :</span><span class="sxs-lookup"><span data-stu-id="dd0ac-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="dd0ac-111">Vous pouvez [vous inscrire à un nouveau compte Microsoft personnel.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)</span><span class="sxs-lookup"><span data-stu-id="dd0ac-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="dd0ac-112">Vous pouvez vous inscrire au programme pour les développeurs [Office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement Office 365 gratuit.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="dd0ac-113">Ce didacticiel a été écrit avec Node version 14.15.0 et La version 1.22.0.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-113">This tutorial was written with Node version 14.15.0 and Yarn version 1.22.0.</span></span> <span data-ttu-id="dd0ac-114">Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais elles n’ont pas été testées.</span><span class="sxs-lookup"><span data-stu-id="dd0ac-114">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="dd0ac-115">Commentaires</span><span class="sxs-lookup"><span data-stu-id="dd0ac-115">Feedback</span></span>

<span data-ttu-id="dd0ac-116">Veuillez nous faire part de vos commentaires sur ce didacticiel dans [le référentiel GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)</span><span class="sxs-lookup"><span data-stu-id="dd0ac-116">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-office-addin).</span></span>
