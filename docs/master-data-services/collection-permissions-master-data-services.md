---
title: "Auflistungsberechtigungen (Master Data Services) | Microsoft Docs"
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
  - "Auflistungen [Master Data Services], Berechtigungen"
  - "Berechtigungen [Master Data Services], Auflistungen"
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Auflistungsberechtigungen (Master Data Services)
  Auflistungsberechtigungen gelten für alle Auflistungen in einer Entität. Es kann keine Berechtigung für eine bestimmte Auflistung erteilt werden; Berechtigungen gelten für alle Auflistungen.  
  
> [!NOTE]  
>  Diese Berechtigungen gelten nur für den Funktionsbereich **Explorer** der Benutzeroberfläche.  
  
|Berechtigung|Description|  
|----------------|-----------------|  
|**Lesen**|Der Benutzer kann Elemente der Auflistung und die Elementattribute lesen.|  
|**Erstellen**|Der Benutzer kann Auflistungselemente erstellen und Attributwerte zuweisen.|  
|**Update**|Der Benutzer kann Auflistungselemente, Attribute und Beziehungen aktualisieren.|  
|**Delete**|Der Benutzer kann Elemente der Auflistung löschen.|  
|**Verweigern**|Jeglicher Zugriff auf die Elemente der Auflistung wird verweigert.|  
  
 Die Berechtigungen Lesen, Erstellen, Aktualisieren und Löschen können kombiniert werden. Wenn Erstellen, Aktualisieren und Löschen zugewiesen werden, wird die Leseberechtigung automatisch zugewiesen.  
  
## Siehe auch  
 [Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)   
 [Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  