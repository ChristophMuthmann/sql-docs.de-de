---
title: Anwenden und Aktualisieren eines Changesets (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a6a3cf2-1e77-43d3-a64a-855ae51258e7
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdb8c98f1a20d6639bb5d5c981645fc2c7023398
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="apply-and-update-a-changeset-master-data-services"></a>Anwenden und Aktualisieren eines Changeset (Master Data Services)
  Ein Changeset ist eine Auflistung der ausstehenden Änderungen an den Masterdaten. Sie können ein Changeset lokal anwenden, um die ausstehenden Änderungen anzuzeigen, hinzuzufügen, zu aktualisieren bzw. zu löschen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie benötigen mindestens die Berechtigung zum Aktualisieren der Entität oder einer ihrer Attribute.  
  
-   Als Administrator einer Entität können Sie nur das Changeset anzeigen, dessen Eigentümer Sie sind, bzw. das zur Genehmigung vorgelegte Changeset.  
  
-   Sie können nur Ihr eigenes Changeset ändern, und das auch nur, wenn der Status des Changeset "Offen" oder "Abgelehnt" lautet.  
  
## <a name="to-apply-and-update-a-changeset"></a>So wenden Sie ein Changeset an und aktualisieren es  
  
1.  Wählen Sie auf der Startseite von [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ein Modell und eine Version aus, und klicken Sie anschließend auf **Explorer**.  
  
2.  Klicken Sie im Menü **Entitäten** auf eine Entität.  
  
3.  Wählen Sie im rechten Bereich **Changesets** aus, und doppelklicken Sie auf das Changeset, das Sie anzeigen und ändern möchten.  
  
4.  Klicken Sie auf **Anwenden**.  
  
     Die ausstehenden Änderungen werden auf das Entitätselement im Raster angewendet. Die ausstehenden Änderungen werden hervorgehoben.  
  
     Durch Erstellen, Löschen und Aktualisieren von Elementen werden die Änderungen des Changeset angewendet.  
  
5.  Um ausstehende Änderungen wieder zurückzusetzen, klicken Sie im Bereich **Changesets** mit der rechten Maustaste in das Raster, und klicken Sie anschließend auf **Wiederherstellen**.  
  
## <a name="next-steps"></a>Next Steps  
 [Ein Changeset bestätigen oder übermitteln &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
