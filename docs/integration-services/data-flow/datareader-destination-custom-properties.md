---
title: "Benutzerdefinierte Eigenschaften des DataReader-Ziels | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Benutzerdefinierte Eigenschaften des DataReader-Ziels
  Das DataReader-Ziel verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften des DataReader-Ziels. Alle Eigenschaften außer **DataReader** weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|DataReader|String|Der Klassenname des DataReader-Ziels.|  
|FailOnTimeout|Boolean|Gibt an, ob ein Fehler ausgegeben wird, wenn ein **ReadTimeout** auftritt. Der Standardwert dieser Eigenschaft ist **False**.|  
|ReadTimeout|Integer|Die Anzahl von Millisekunden, bevor ein Timeout auftritt. Der Standardwert dieser Eigenschaft beträgt 30000 (30 Sekunden).|  
  
 Die Eingabe und die Eingabespalten des DataReader-Ziels verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [DataReader Destination](../../integration-services/data-flow/datareader-destination.md).  
  
## Siehe auch  
 [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
  