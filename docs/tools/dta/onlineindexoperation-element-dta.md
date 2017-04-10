---
title: "OnlineIndexOperation-Element (DTA) | Microsoft Docs"
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
  - "OnlineIndexOperation-Element"
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# OnlineIndexOperation-Element (DTA)
  Gibt an, ob die vom Datenbankoptimierungsratgeber empfohlenen Indizes, indizierten Sichten oder Partitionen online erstellt werden können.  
  
## Syntax  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, keine maximale Länge.|  
|**Zulässige Werte**|**OFF**<br /> Es können keine empfohlenen physischen Entwurfsstrukturen online erstellt werden.<br /><br /> **ON**<br /> Alle empfohlenen physischen Entwurfsstrukturen können online erstellt werden.<br /><br /> **MIXED**<br /> Der Datenbankoptimierungsratgeber versucht, sofern möglich physische Entwurfsstrukturen zu empfehlen, die online erstellt werden können.<br /><br /> Verwenden Sie einen dieser Werte mit diesem Element. Wenn Indizes online erstellt werden, wird das Schlüsselwort **ONLINE = ON** an die Objektdefinition angehängt.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Kann bei Verwendung nur einmalig pro **TuningOptions** -Element verwendet werden.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Untergeordnete Elemente**|Keine.|  
  
## Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine einfache XML-Eingabedatei &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  