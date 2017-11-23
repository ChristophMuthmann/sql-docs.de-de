---
title: Configuration-Element (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20e3d53c5e7825af7a018d0a42b2361f1fe2e5d1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configuration-element-dta"></a>Configuration-Element (DTA)
  Gibt eine benutzerdefinierte Konfiguration an, die aus vorhandenen und hypothetischen physischen Entwurfsstrukturen besteht, die der Datenbankoptimierungsratgeber beim Optimieren einer Arbeitsauslastung analysiert.  
  
## <a name="syntax"></a>Syntax  
  
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
  
## <a name="element-attributes"></a>Elementattribute  
  
|Konfigurationsattribut|Beschreibung|  
|-----------------------------|-----------------|  
|**SpecificationMode**|Optional. Gibt an, ob der Datenbankoptimierungsratgeber die angegebene Konfiguration im Vergleich zur aktuellen vorhandenen Konfiguration oder als vollständig neue eigenständige Konfiguration analysieren soll. Mit einem **string** -Datentyp können Sie dieses Attribut mit einem der folgenden zulässigen Werte angeben:<br /><br /> **Relative**:<br />                  Wertet die angegebene Konfiguration im Vergleich zur aktuellen vorhandenen Konfiguration physischer Entwurfsstrukturen (Indizes, indizierte Sichten, Partitionierung) in der Datenbank aus, die optimiert wird. Beispiel:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Wertet die angegebene Konfiguration als eigenständige Konfiguration aus. Wenn der Absolute-Wert angegeben ist, wird die vorhandene Konfiguration nicht vom Datenbankoptimierungsratgeber berücksichtigt. Beispiel:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Einmalige Verwendung pro **DTAInput** -Element möglich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[DTAInput-Element &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Untergeordnete Elemente**|[Server-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
