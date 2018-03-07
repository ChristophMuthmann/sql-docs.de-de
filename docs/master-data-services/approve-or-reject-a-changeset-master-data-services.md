---
title: Genehmigen oder Ablehnen eines Changesets (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae28abadd1114bf5944502337289170061f39e1c
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>Genehmigen oder Ablehnen eines Changesets (Master Data Services)
  Ein Changeset ist eine Auflistung der ausstehenden Änderungen an den Masterdaten. Wenn die Entitätsänderungen die Genehmigung durch den Administrator erfordern und ein Changeset zur Genehmigung übermittelt wird, können Sie das Changeset überprüfen und dann genehmigen oder ablehnen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie benötigen Administratorberechtigungen für die Entität.  
  
-   Die Entitätsänderungen müssen die Genehmigung durch den Administrator erfordern.  
  
-   Wenn der Changesetstatus ausstehend ist, können Sie das Changeset überprüfen und dann genehmigen oder ablehnen.  
  
-   Benutzer dürfen nicht ihre eigenen Änderungen genehmigen. Wenn Sie der Entitätsadministrator sind, müssen Sie einen sekundären Administrator zuweisen, um Ihr eigenes Changeset zu genehmigen.  
  
## <a name="to-approve-or-reject-a-changeset"></a>So können Sie ein Changeset genehmigen oder ablehnen  
  
1.  Wählen Sie auf der Startseite von [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] das Modell und die Version aus, und klicken Sie anschließend auf **Explorer**.  
  
2.  Klicken Sie im Menü **Entitäten** auf eine Entität.  
  
3.  Wählen Sie im rechten Bereich **Changesets** aus, und doppelklicken Sie auf das Changeset, das Sie genehmigen oder ablehnen möchten.  
  
4.  Klicken Sie auf **Anwenden** , um das Changeset zu übernehmen und die ausstehenden Änderungen zu überprüfen.  
  
5.  Klicken Sie auf **Ablehnen** , um das Changeset abzulehnen und zurück an den Besitzer zu senden.  
  
6.  Klicken Sie auf **Genehmigen** , um das Changeset zu genehmigen. Für das Changeset wird automatisch ein Commit ausgeführt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Anwenden und Aktualisieren eines Changesets &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Ein Changeset bestätigen oder übermitteln &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
