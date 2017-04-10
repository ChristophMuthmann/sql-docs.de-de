---
title: "Database-Element f&#252;r Server (DTA) | Microsoft Docs"
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
  - "Database-Element"
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# Database-Element f&#252;r Server (DTA)
  Gibt die Datenbank an, die Sie auf einem bestimmten Server optimieren möchten.  
  
## Syntax  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine.|  
|Standardwert|Keine.|  
|Vorkommen|Einmal oder mehrfach pro **Server** -Element erforderlich.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|Übergeordnetes Element|[Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|Untergeordnete Elemente|[Name-Element für Datenbank &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Schema-Element für Datenbank &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## Hinweise  
 Dieses Element hat den Namen **DatabaseDetailsTypecomplexType** im XML-Schema des Datenbankoptimierungsratgebers. Dieses **Database** -Element ist nicht mit dem identisch, dessen übergeordnetes Stammelement das **Configuration** -Element ist. Weitere Informationen finden Sie unter [Database-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md).  
  
## Beispiel  
 Ein Beispiel für die Verwendung des **Database**-Elements finden Sie unter [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  