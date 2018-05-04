---
title: KeepExisting-Element (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b426c32b4573ed0b30ae4180b3b782de9f553dae
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="keepexisting-element-dta"></a>KeepExisting-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gibt die physischen Entwurfsstrukturen (Indizes, indizierte Sichten oder Partitionierung) an, die der Datenbankoptimierungsratgeber beim Generieren der Empfehlung beibehalten muss.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, Grenzwert für die Länge wird vom Server erzwungen.|  
|**Zulässige Werte**|**NONE**<br /> Keine vorhandenen Strukturen.<br /><br /> **ALL**<br /> Alle vorhandenen Strukturen.<br /><br /> **ALIGNED**<br /> Alle Strukturen mit ausgerichteten Partitionen.<br /><br /> **CL_IDX**<br /> Alle gruppierten Indizes für Tabellen.<br /><br /> **IDX**<br /> Alle gruppierten und nicht gruppierten Indizes für Tabellen.<br /><br /> Verwenden Sie nur einen dieser Werte mit diesem Element.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Nur einmalige Verwendung pro **TuningOptions** -Element möglich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Untergeordnete Elemente**|Keine.|  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine einfache XML-Eingabedatei &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
