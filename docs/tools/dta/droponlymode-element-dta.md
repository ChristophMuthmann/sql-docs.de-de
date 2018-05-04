---
title: DropOnlyMode-Element (DTA) | Microsoft Docs
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
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8e745bbafdf46451cf33628df2ab770b713bbe4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gibt an, dass der Datenbankoptimierungsratgeber während der Optimierungssitzung nur vorhandene Indizes, indizierte Sichten oder Partitionen löschen soll. Wenn diese Optimierungsoption angegeben ist, werden keine neuen physischen Entwurfsstrukturen berücksichtigt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
 **Datentyp und -länge**  
  
 **Standardwert**  
  
 **Vorkommen**: optional. Kann für jedes **TuningOptions** -Element nur einmal verwendet werden. Keine Verwendung möglich, wenn im **TuningOptions** -Element die folgenden Elemente angegeben sind:  
  
-   [FeatureSet-Element &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning-Element &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [KeepExisting-Element &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md) ist auf **ALL** festgelegt  
  
## <a name="element-relationships"></a>Elementbeziehungen  
 **Parent-Element**: [TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
 **Untergeordnete Elemente**  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht den **TuningOptions** -Abschnitt einer XML-Eingabedatei des Datenbankoptimierungsratgebers, wobei **DropOnlyMode** angegeben ist. In diesem Beispiel ist die Optimierungszeit auf 24 Stunden (1440 Minuten) begrenzt, und alle vorhandenen gruppierten und nicht gruppierten Indizes sollen gelöscht werden:  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
