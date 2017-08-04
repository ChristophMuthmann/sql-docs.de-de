---
title: "Bestätigen oder übermitteln ein Changesets (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd91aef621a480510896500070bd36e55d778d66
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>Ein Changeset bestätigen oder übermitteln (Master Data Services)
  Ein Changeset ist eine Auflistung der ausstehenden Änderungen an den Masterdaten. Wenn für die Entitätsänderungen keine Genehmigung durch den Administrator erforderlich ist, können Sie das Changeset bestätigen. Wenn die Entitätsänderungen vom Administrator genehmigt werden müssen, können Sie das Changeset zur Genehmigung übermitteln.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
  
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
  
## <a name="next-steps"></a>Nächste Schritte  
 [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Wenden Sie an und aktualisieren Sie ein Changeset &#40; Master Data Services &#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
