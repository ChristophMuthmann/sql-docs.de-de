---
title: "Sofortiges Anwenden von Elementberechtigungen (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Elemente [Master Data Services], sofortiges Anwenden von Berechtigungen"
  - "Berechtigungen [Master Data Services], sofortiges Anwenden von Elementberechtigungen"
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Sofortiges Anwenden von Elementberechtigungen (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie sofort Elementberechtigungen anwenden, statt zu warten, bis die Elementsicherheit in regelmäßigen Abständen angewendet wird.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, die gespeicherte Prozedur mdm.udpSecurityMemberProcessRebuildModel in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank auszuführen. Weitere Informationen finden Sie unter [Sicherheit von Datenbankobjekten &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md).  
  
### So wenden Sie Hierarchieelementberechtigungen sofort an  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung mit der [!INCLUDE[ssDE](../includes/ssde-md.md)] -Instanz für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank her.  
  
2.  Erstellen Sie eine neue Abfrage.  
  
3.  Geben Sie den folgenden Text ein, und ersetzen Sie *Datenbank* durch den Namen Ihrer Datenbank und *Name des Modells* durch den Namen des Modells.  
  
    ```  
    USE [database];  
    GO  
  
    DECLARE @Model_ID INT;  
    SELECT @Model_ID = ID FROM mdm.tblModel WHERE [Name] = N'Model_Name';  
    EXEC [mdm].[udpSecurityMemberProcessRebuildModel] @Model_ID=@Model_ID, @ProcessNow=1;  
    GO  
    ```  
  
4.  Führen Sie die Abfrage aus.  
  
## Siehe auch  
 [Zuweisen von Hierarchieelementberechtigungen &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Berechtigungen für Hierarchieelemente &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  