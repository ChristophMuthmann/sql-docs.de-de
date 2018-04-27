---
title: Bestätigen oder Übermitteln eines Changesets (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 149519f8072dc783747edb26ce449e4ade290685
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>Ein Changeset bestätigen oder übermitteln (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Ein Changeset ist eine Auflistung der ausstehenden Änderungen an den Masterdaten. Wenn für die Entitätsänderungen keine Genehmigung durch den Administrator erforderlich ist, können Sie das Changeset bestätigen. Wenn die Entitätsänderungen vom Administrator genehmigt werden müssen, können Sie das Changeset zur Genehmigung übermitteln.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Wenn für die Entitätsänderungen keine Genehmigung durch den Administrator erforderlich ist, können Sie das Changeset nur bestätigen, wenn Sie das Changeset besitzen und der Changeset-Status "offen" ist.  
  
-   Wenn die Entitätsänderungen vom Administrator genehmigt werden müssen, können Sie das Changeset nur zur Genehmigung übermitteln, wenn Sie der Besitzer des Changesets sind und der Changeset-Status "offen" oder "abgelehnt" ist.  
  
## <a name="to-commit-a-local-changeset"></a>So führen Sie einen Commit für ein lokales Changeset aus  
 Die Commitoption ist nur für lokale Changesets in Entitäten verfügbar, für die der Entitätsadministrator nicht die Notwendigkeit zur Genehmigung aktiviert hat.  
  
1.  Wählen Sie auf der Startseite von [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] das Modell und die Version aus, und klicken Sie anschließend auf **Explorer**.  
  
2.  Klicken Sie im Menü **Entitäten** auf eine Entität.  
  
3.  Wählen Sie im rechten Bereich **Changesets** aus, und doppelklicken Sie auf das Changeset, das Sie bestätigen möchten.  
  
4.  Klicken Sie auf **Commit**.  
  
## <a name="to-submit-a-changeset"></a>So senden Sie ein Changeset  
 Die Sendeoption ist nur für Changesets in Entitäten verfügbar, für die der Entitätsadministrator die Notwendigkeit zur Genehmigung aktiviert hat.  
  
1.  Wählen Sie auf der Startseite von [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] das Modell und die Version aus, und klicken Sie anschließend auf **Explorer**.  
  
2.  Klicken Sie im Menü **Entitäten** auf eine Entität.  
  
3.  Wählen Sie im rechten Bereich **Changesets** aus, und doppelklicken Sie auf das Changeset, das Sie senden möchten.  
  
4.  Klicken Sie auf **Submit**(Senden).  
  
## <a name="next-steps"></a>Next Steps  
 [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Anwenden und Aktualisieren eines Changesets &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
