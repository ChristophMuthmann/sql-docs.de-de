---
title: FeatureSet-Element (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61253d4641b008b1cb48213962a2cbc992e4c7b8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="featureset-element-dta"></a>FeatureSet-Element (DTA)
  Enthält die physischen Entwurfsstrukturen (Indizes oder indizierte Sichten), die der Datenbankoptimierungsratgeber bei der Analyse verwenden soll.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, keine maximale Länge.|  
|**Zulässige Werte**|**IDX_IV**<br /> Indizes und indizierte Sichten.<br /><br /> **IDX**<br /> Nur Indizes.<br /><br /> **IV**<br /> Nur indizierte Sichten.<br /><br /> **NCL_IDX**<br /> Nur nicht gruppierte Indizes.<br /><br /> Verwenden Sie einen dieser Werte mit diesem Element.|  
|**Standardwert**|**IDX**|  
|**Vorkommen**|Einmalig erforderlich für jedes **TuningOptions** -Element, es sei denn, das **DropOnlyMode** -Element wird verwendet. Wird das **DropOnlyMode** -Element verwendet, kann das **FeatureSet**-Element nicht verwendet werden. Diese Elemente schließen sich gegenseitig aus.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Untergeordnete Elemente**|Keine.|  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine einfache XML-Eingabedatei &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
