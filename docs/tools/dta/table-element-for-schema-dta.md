---
title: "Table-Element f&#252;r Schema (DTA) | Microsoft Docs"
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
  - "Table-Element [DTA]"
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Table-Element f&#252;r Schema (DTA)
  Gibt die Tabelle zum Optimieren an.  
  
## Syntax  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## Elementattribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|**NumberOfRows**|Optional. Eine ganze Zahl, mit der Sie Tabellen unterschiedlicher Größe simulieren können.|  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, 1 bis 255 Zeichen.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Sie können beliebig viele Tabellen für die Arbeitsauslastung auflisten.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Schema-Element für Datenbank &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Tabelle &#40;DTA&#41;](../../tools/dta/name-element-for-table-dta.md)|  
  
## Hinweise  
 Wenn Sie kein **Table** -Element angeben, geht der Datenbankoptimierungsratgeber davon aus, dass sich alle Tabellen in der angegebenen Datenbank optimieren lassen.  
  
## Beispiel  
 Ein Beispiel für die Verwendung finden Sie unter [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  