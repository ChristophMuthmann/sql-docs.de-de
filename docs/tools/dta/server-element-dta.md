---
title: "Server-Element (DTA) | Microsoft Docs"
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
  - "Server-Element"
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# Server-Element (DTA)
  Enthält die Identifikationsinformationen für den Server, auf dem sich die zu optimierenden Datenbanken befinden.  
  
## Syntax  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmal pro **DTAInput** -Element erforderlich.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[DTAInput-Element &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Database-Element für Server &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)|  
  
## Hinweise  
 Sie können nur ein **Server** -Element für das **DTAInput** -Element angeben. Dieses Element hat im DTA-XML-Schema den Namen **ServerDetailsTypecomplexType**. Dieses **Server** -Element ist nicht mit dem untergeordneten Element für das **Configuration** -Element identisch. Weitere Informationen finden Sie unter [Server-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md).  
  
## Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die **Sales.SalesPerson** -Tabelle in der **AdventureWorks** -Datenbank auf SERVER001 angegeben wird:  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  