---
title: Configuration-Element (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 50e3fc0edbc43eff14fa9cfec5e4bf5d8326b0e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configuration-element-dta"></a>Configuration-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
|Konfigurationsattribut|Description|  
|-----------------------------|-----------------|  
|**SpecificationMode**|Optional. Gibt an, ob der Datenbankoptimierungsratgeber die angegebene Konfiguration im Vergleich zur aktuellen vorhandenen Konfiguration oder als vollständig neue eigenständige Konfiguration analysieren soll. Mit einem **string** -Datentyp können Sie dieses Attribut mit einem der folgenden zulässigen Werte angeben:<br /><br /> **Relative**:<br />                  Wertet die angegebene Konfiguration im Vergleich zur aktuellen vorhandenen Konfiguration physischer Entwurfsstrukturen (Indizes, indizierte Sichten, Partitionierung) in der Datenbank aus, die optimiert wird. Zum Beispiel:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Wertet die angegebene Konfiguration als eigenständige Konfiguration aus. Wenn der Absolute-Wert angegeben ist, wird die vorhandene Konfiguration nicht vom Datenbankoptimierungsratgeber berücksichtigt. Zum Beispiel:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
