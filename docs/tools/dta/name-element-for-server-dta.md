---
title: "Name-Element f&#252;r Server (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "Name-Element"
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Name-Element f&#252;r Server (DTA)
  Enthält den Namen des Servers, auf dem sich die zu optimierenden Datenbanken befinden.  
  
## Syntax  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, 1 bis 255 Zeichen.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmalig pro **Server** -Element erforderlich.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|**Untergeordnete Elemente**|Keine.|  
  
## Beispiel  
 Ein Beispiel für die Verwendung dieses **Name**-Elements finden Sie unter [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  