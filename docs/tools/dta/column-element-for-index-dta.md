---
title: "Column-Element f&#252;r Index (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/09/2017"
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
  - "Column-Element"
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Column-Element f&#252;r Index (DTA)
  Gibt die Spalten an, für die der Index für eine benutzerspezifische Konfiguration erstellt wird.  
  
## Syntax  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## Elementattribute  
  
 **Type**: Optional. Gibt den Indexspaltentyp an. Mit einem **string** -Datentyp können Sie dieses Attribut mit einem der folgenden zulässigen Werte angeben:  
  
-   **KeyColumn**  
  
     Gibt an, dass durch einen Indexschlüssel auf die Spalte verwiesen wird. Verwenden Sie die folgende Syntax, um dieses Attribut festzulegen:  
  
    ```  
    <Column Type="KeyColumn">  
    ```  
  
     Weitere Informationen zu Schlüsselspalten finden Sie unter [Beschreibung von gruppierten und nicht gruppierten Indizes](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md).  
  
-   **IncludedColumn**  
  
     Gibt an, dass die Spalte eine eingeschlossene Spalte ist (statt einer Schlüsselspalte). Verwenden Sie die folgende Syntax, um dieses Attribut festzulegen:  
  
    ```  
    <Column Type="IncludedColumn">  
    ```  
  
     Weitere Informationen zu eingeschlossenen Spalten finden Sie unter [Erstellen von Indizes mit eingeschlossenen Spalten](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
 **SortOrder**: Optional. Gibt die Sortierreihenfolge der Spalte an. Mit einem **string** -Datentyp können Sie die Sortierreihenfolge wie folgt als **Aufsteigend** oder **Absteigend** angeben:  
  
```  
<Column SortOrder="Ascending">  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Angabe von bis zu 1024 Spalten für das **Index** -Element möglich.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Index-Element &#40;DTA&#41;](../../tools/dta/index-element-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Spalte &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)|  
  
## Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  