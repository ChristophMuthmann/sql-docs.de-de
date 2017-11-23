---
title: Partitioning-Element (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c84705492db53c29b2f430d6e105a239e4393de
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="partitioning-element-dta"></a>Partitioning-Element (DTA)
  Enthält das Partitionierungsschema, das der Datenbankoptimierungsratgeber bei der Analyse verwenden soll.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, keine maximale Länge.|  
|**Zulässige Werte**|**NONE**<br /> Keine Partitionierung.<br /><br /> **FULL**<br /> Vollständige Partitionierung. (Erhöht die Leistung.)<br /><br /> **ALIGNED**<br /> Nur ausgerichtete Partitionierung. (Erleichtert die Verwaltbarkeit.)<br /><br /> Verwenden Sie nur einen dieser Werte mit diesem Element.<br /><br /> **ALIGNED** bedeutet, dass in der vom Datenbankoptimierungsratgeber generierten Empfehlung jeder vorgeschlagene Index auf exakt dieselbe Weise partitioniert wird wie die zugrunde liegende Tabelle, für die der Index definiert ist. Nicht gruppierte Indizes für eine indizierte Sicht werden mit der indizierten Sicht ausgerichtet.|  
|**Standardwert**|**NONE**|  
|**Vorkommen**|Einmalig erforderlich für das **TuningOptions** -Element, es sei denn, das **DropOnlyMode** -Element wird verwendet. Wird das **DropOnlyMode** -Element verwendet, kann das **Partitioning**-Element nicht verwendet werden. Diese Elemente schließen sich gegenseitig aus.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Untergeordnete Elemente**|Keine.|  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine einfache XML-Eingabedatei &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
