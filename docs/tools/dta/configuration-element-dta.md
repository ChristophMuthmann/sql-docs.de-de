---
title: "Configuration-Element (DTA) | Microsoft Docs"
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
  - "Configuration-Element"
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# Configuration-Element (DTA)
  Gibt eine benutzerdefinierte Konfiguration an, die aus vorhandenen und hypothetischen physischen Entwurfsstrukturen besteht, die der Datenbankoptimierungsratgeber beim Optimieren einer Arbeitsauslastung analysiert.  
  
## Syntax  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## Elementattribute  
  
|Konfigurationsattribut|Beschreibung|  
|-----------------------------|-----------------|  
|**SpecificationMode**|Optional. Gibt an, ob der Datenbankoptimierungsratgeber die angegebene Konfiguration im Vergleich zur aktuellen vorhandenen Konfiguration oder als vollständig neue eigenständige Konfiguration analysieren soll. Mit einem **string** -Datentyp können Sie dieses Attribut mit einem der folgenden zulässigen Werte angeben:<br /><br /> **Relative**:<br />                  Wertet die angegebene Konfiguration im Vergleich zur aktuellen vorhandenen Konfiguration physischer Entwurfsstrukturen (Indizes, indizierte Sichten, Partitionierung) in der Datenbank aus, die optimiert wird. Beispiel:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Wertet die angegebene Konfiguration als eigenständige Konfiguration aus. Wenn der Absolute-Wert angegeben ist, wird die vorhandene Konfiguration nicht vom Datenbankoptimierungsratgeber berücksichtigt. Beispiel:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Einmalige Verwendung pro **DTAInput** -Element möglich.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[DTAInput-Element &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Untergeordnete Elemente**|[Server-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter der [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  