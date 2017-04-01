---
title: "Server-Element f&#252;r Konfiguration (DTA) | Microsoft Docs"
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
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Server-Element f&#252;r Konfiguration (DTA)
  Enthält die Identifikationsinformationen für den Server, auf dem der Datenbankoptimierungsratgeber die hypothetische Konfiguration auswerten soll (wird durch das **Configuration**-Element angegeben).  
  
## Syntax  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmal pro **Configuration** -Element erforderlich.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Configuration-Element &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Database-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## Hinweise  
 Sie können nur ein **Server** -Element für das **Configuration** -Element angeben. Dieses Element hat den Namen **ServerTypecomplexType** im [XML-Schema des Datenbankoptimierungsratgebers](http://go.microsoft.com/fwlink/?linkid=43100). Dieses **Server** -Element ist nicht mit dem untergeordneten Element für das **DTAInput** -Element identisch. Weitere Informationen finden Sie unter [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## Beispiel  
 Ein Beispiel für die Syntax finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  