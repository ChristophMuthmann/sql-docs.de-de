---
title: "Benutzer und Gruppen (Master Data Services) | Microsoft Docs"
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
  - "Benutzer [Master Data Services]"
  - "Gruppen [Master Data Services]"
  - "Benutzer [Master Data Services], Informationen zu Benutzern"
  - "Gruppen [Master Data Services], Informationen zu Gruppen"
ms.assetid: ed08dd2d-248e-4b68-91d4-e9961cb50eed
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# Benutzer und Gruppen (Master Data Services)
  Um auf die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung zuzugreifen, muss der Benutzer über ein Windows-Domänenkonto oder ein Konto auf dem Servercomputer verfügen, auf dem [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] installiert ist. Sie können wie folgt Zugriff auf [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] gewähren:  
  
-   Fügen Sie das Benutzerkonto einer Domänengruppe oder lokalen Gruppe hinzu und fügen Sie die Gruppe dann zur Liste der Gruppen in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]hinzu.  
  
-   Fügen Sie das Benutzerkonto zur Liste der Benutzer in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]hinzu.  
  
    > [!NOTE]  
    >  Wenn ein Benutzer zu einer Gruppe gehört, die Zugriff auf [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] hat, wird der Name des Benutzers beim ersten Zugriff auf [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] oder MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] automatisch zur Liste der Benutzer hinzugefügt.  
  
 Um innerhalb des Funktionsbereichs **Explorer** der Benutzeroberfläche Aktionen ausführen zu können, müssen der Gruppe bzw. dem Benutzer Zugriff auf den Funktionsbereich **Explorer** gewährt und Berechtigungen für Modellobjekte zugewiesen werden.  
  
 Wenn ein Benutzer oder eine Gruppe Zugriff auf andere Funktionsbereiche benötigt, muss dem Benutzer bzw. der Gruppe ein Zugriff auf die spezifischen Funktionsbereiche zugewiesen werden.  
  
## Bewährte Methoden  
 Um die Verwaltung zu vereinfachen, erstellen Sie Gruppen und weisen den Funktionsbereichen und Modellobjekten die einzelnen Gruppenberechtigungen zu. Sie können anschließend der Gruppe Benutzer hinzufügen und diese daraus entfernen, ohne auf die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Benutzeroberfläche zuzugreifen.  
  
 Weisen Sie einem einzelnen Benutzer keine zusätzlichen Berechtigungen zu und nehmen Sie einen Benutzer nicht in mehrere Gruppen auf, die Zugriff auf [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]haben. Verwenden Sie außerdem keine Hierarchieelementberechtigungen, es sei denn, eine Gruppe soll beschränkten Zugriff auf bestimmte Elemente haben.  
  
## Siehe auch  
 [Hinzufügen eines Benutzers &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)   
 [Hinzufügen einer Gruppe &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)   
 [Löschen von Benutzern oder Gruppen &#40;Master Data Services&#41;](../master-data-services/delete-users-or-groups-master-data-services.md)   
 [Testen der Berechtigungen eines Benutzers &#40;Master Data Services&#41;](../master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  