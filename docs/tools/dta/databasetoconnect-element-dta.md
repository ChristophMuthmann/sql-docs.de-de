---
title: DatabaseToConnect-Element (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: "12"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e57133b7158ba1fae461f2d058f9cd8065226c8
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Gibt die erste Datenbank, die mit der Datenbankmodul-Optimierungsratgeber, beim Optimieren einer arbeitsauslastung verbunden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, unbegrenzte Länge.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Einmalige Verwendung pro **TuningOptions** -Element möglich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[TuningOptions-Element &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Untergeordnete Elemente**|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Mit **DatabaseToConnect** können Sie den Namen der ersten Datenbank angeben, mit der der Datenbankoptimierungsratgeber beim Starten der Optimierungssitzung eine Verbindung herstellen soll. Sie können mithilfe dieses Elements nur eine Datenbank angeben. Wenn mehrere Datenbanknamen angegeben werden, gibt der Datenbankoptimierungsratgeber einen Fehler zurück.  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung finden Sie unter [Beispiel für eine XML-Eingabedatei mit Inlinearbeitsauslastung &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
