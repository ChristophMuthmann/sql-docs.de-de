---
title: TuningTimeInMin-Element (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TuningTimeInMin element
ms.assetid: 4973d9ac-20fd-4ac3-bc9f-5d60e39fdb7d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 534f7868de00a0e102ba6f80c8663f0aaa7bf279
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="tuningtimeinmin-element-dta"></a>TuningTimeInMin-Element (DTA)
  Gibt die maximale Dauer einer Optimierungssitzung in Minuten an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <TuningTimeInMin>...</TuningTimeInMin>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**unsignedInt**, unbegrenzte Länge.|  
|**Standardwert**|480 Minuten (8 Stunden).|  
|**Vorkommen**|Erforderlich, sofern kein Wert für das **NumberOfEvents** -Element festgelegt wurde.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[TuningOptions-Element &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Untergeordnete Elemente**|Keine|  
  
## <a name="example"></a>Beispiel  
  
## <a name="description"></a>Beschreibung  
 Im folgenden Codebeispiel wird gezeigt, wie 12 Stunden als maximale Optimierungszeit festgelegt werden:  
  
## <a name="code"></a>Code  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <TuningTimeInMin>720</TuningTimeInMin>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

