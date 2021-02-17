---
ms.openlocfilehash: facdbb5c42e60e5bb0ee98b06ef68939a6010a67
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274250"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez ajouter la possibilité de créer des événements sur le calendrier de l’utilisateur.

## <a name="implement-the-api"></a>Implémenter l’API

1. Ouvrez **./src/api/graph.ts** et ajoutez le code suivant pour implémenter une nouvelle API d’événement ( `POST /graph/newevent` ).

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="CreateEventSnippet":::

1. Ouvrez **./src/addin/taskpane.js** et ajoutez la fonction suivante pour appeler la nouvelle API d’événement.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="CreateEventSnippet":::

1. Enregistrez toutes vos modifications, redémarrez le serveur et actualisez le volet Des tâches dans Excel (fermez les volets Des tâches ouverts et ré-ouvrez- le).

    ![Capture d’écran du formulaire de création d’événement](images/create-event-ui.png)

1. Remplissez le formulaire et choisissez **Créer.** Vérifiez que l’événement est ajouté au calendrier de l’utilisateur.
