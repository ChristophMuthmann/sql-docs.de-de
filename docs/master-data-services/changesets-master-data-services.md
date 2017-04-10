---
title: "Changesets (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
caps.latest.revision: 13
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 13
---
# Changesets (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] unterstützt nun die Möglichkeit, ausstehende Änderungen in einer Entität als Changesets zu speichern. Es gibt zwei Verwendungsszenarios für diese Funktion.  
  
-   **Ändert sich, wenn „Genehmigung erforderlich“ von Entitätsadministrator aktiviert wird**  
  
     Wenn ein Entitätsadministrator angibt, dass für die Änderungen an einer bestimmten Entität eine Genehmigung erforderlich ist, bevor für diese ein Commit ausgeführt wird, so müssen alle Änderungen an der Entität in einem neuen oder vorhandenen Changeset gespeichert werden, bevor sie zur Genehmigung übermittelt werden.  Weitere Informationen finden Sie unter [Genehmigung erforderlich &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md).  
  
     Befolgen Sie diesen Workflow.  
  
    1.  Erstellen Sie ein Changeset. Das Changeset befindet sich im Status „Offen“. Weitere Informationen finden Sie unter [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md).  
  
    2.  Wenden Sie das Changeset an, und führen Sie einige Änderungen am Changeset durch. Weitere Informationen finden Sie unter [Anwenden und Aktualisieren eines Changesets &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Übermitteln Sie das Changeset zur Genehmigung an den Entitätsadministrator. Das Changeset befindet sich im Status „Ausstehend“. Weitere Informationen finden Sie unter [Ein Changeset bestätigen oder übermitteln &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md).  
  
    4.  Der Entitätsadministrator erhält eine E-Mail-Benachrichtigung, dass ein Changeset auf Genehmigung wartet. Wenn der Entitätsadministrator das Changeset genehmigt, befindet sich das Changeset im Status „Genehmigt“. Weitere Informationen finden Sie unter [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  Für das genehmigte Changeset wird automatisch ein Commit ausgeführt. Wenn für die Änderung erfolgreich ein Commit ausgeführt wurde, befindet sich das Changeset im Status „Commit wurde ausgeführt“.  
  
-   **Änderungen des lokalen Benutzers**  
  
     Wenn Sie lediglich Ihre lokalen Änderungen speichern möchten, sodass Sie diese später verwenden oder abrufen können, können Sie dafür Changesets verwenden.  
  
     Befolgen Sie diesen Workflow.  
  
    1.  Erstellen Sie ein Changeset. Das Changeset befindet sich im Status „Offen“. Weitere Informationen finden Sie unter [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md).  
  
    2.  Wenden Sie das Changeset an, und führen Sie einige Änderungen am Changeset durch. Weitere Informationen finden Sie unter [Anwenden und Aktualisieren eines Changesets &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Wenn Sie bereit sind, führen Sie ein Commit auf das Changeset aus. Weitere Informationen finden Sie unter [Ein Changeset bestätigen oder übermitteln &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md).  
  
## Siehe auch  
 [Erstellen eines Changesets &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Anwenden und Aktualisieren eines Changesets &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Ein Changeset bestätigen oder übermitteln &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Genehmigen oder Ablehnen eines Changesets &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [Verwalten von Changesets &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  