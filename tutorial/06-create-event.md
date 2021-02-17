---
ms.openlocfilehash: facdbb5c42e60e5bb0ee98b06ef68939a6010a67
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274250"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e883c-101">Dans cette section, vous allez ajouter la possibilité de créer des événements sur le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e883c-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="implement-the-api"></a><span data-ttu-id="e883c-102">Implémenter l’API</span><span class="sxs-lookup"><span data-stu-id="e883c-102">Implement the API</span></span>

1. <span data-ttu-id="e883c-103">Ouvrez **./src/api/graph.ts** et ajoutez le code suivant pour implémenter une nouvelle API d’événement ( `POST /graph/newevent` ).</span><span class="sxs-lookup"><span data-stu-id="e883c-103">Open **./src/api/graph.ts** and add the following code to implement a new event API (`POST /graph/newevent`).</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="CreateEventSnippet":::

1. <span data-ttu-id="e883c-104">Ouvrez **./src/addin/taskpane.js** et ajoutez la fonction suivante pour appeler la nouvelle API d’événement.</span><span class="sxs-lookup"><span data-stu-id="e883c-104">Open **./src/addin/taskpane.js** and add the following function to call the new event API.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="CreateEventSnippet":::

1. <span data-ttu-id="e883c-105">Enregistrez toutes vos modifications, redémarrez le serveur et actualisez le volet Des tâches dans Excel (fermez les volets Des tâches ouverts et ré-ouvrez- le).</span><span class="sxs-lookup"><span data-stu-id="e883c-105">Save all of your changes, restart the server, and refresh the task pane in Excel (close any open task panes and re-open).</span></span>

    ![Capture d’écran du formulaire de création d’événement](images/create-event-ui.png)

1. <span data-ttu-id="e883c-107">Remplissez le formulaire et choisissez **Créer.**</span><span class="sxs-lookup"><span data-stu-id="e883c-107">Fill in the form and choose **Create**.</span></span> <span data-ttu-id="e883c-108">Vérifiez que l’événement est ajouté au calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e883c-108">Verify that the event is added to the user's calendar.</span></span>
