---
title: DTAXML-Element (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
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
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4eeed88249de7d3d04bee44262d72e113a8e04ec
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="dtaxml-element-dta"></a>DTAXML-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Als Stammelement einer XML-Eingabe- oder -Ausgabedatei des Datenbankoptimierungsratgebers enthält **DTAXML** alle Elemente, die die vom Datenbankoptimierungsratgeber generierte Optimierungseingabe und -ausgabe beschreiben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>Elementattribute  
  
|attribute|Description|  
|---------------|-----------------|  
|**xmlns:xsi**|Erforderlich. Identifiziert den XML-Schemainstanzennamespace. Attribute aus diesem Namespace dienen zum Verweisen auf das Schema, das zum Überprüfen der XML-Datei des Datenbankoptimierungsratgebers verwendet wird.<br /><br /> Erforderlicher Wert: [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|**xmlns**|Erforderlich. Identifiziert den Namespace des Datenbankoptimierungsratgebers.<br /><br /> Wenn Sie die XML-Datei des Datenbankoptimierungsratgebers mit dem XML-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bearbeiten, wird dieser Wert von der F1-Hilfe und der dynamischen Hilfe verwendet, um mögliche Referenzthemen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation zu ermitteln.<br /><br /> Erforderlicher Wert:<br /><br /> für das[XML-Schema des Datenbankoptimierungsratgebers](http://go.microsoft.com/fwlink/?LinkId=43100) |  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmal pro DTA XML-Datei erforderlich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|InclusionThresholdSetting|  
|**Untergeordnete Elemente**|[DTAInput-Element &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)<br /><br /> **DTAOutput**-Element (weitere Informationen finden Sie im Thema zum [XML-Schema für den Datenbankoptimierungsratgeber](http://schemas.microsoft.com/sqlserver/))|  
  
## <a name="remarks"></a>Remarks  
 Weitere Informationen zu XML-Namespaces finden Sie unter [Namespaces in an XML Document](http://go.microsoft.com/fwlink/?LinkId=7341) (in Englisch) in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN Library.  
  
## <a name="example"></a>Beispiel  
 Beispiele für typische **DTAXML**-Elemente finden Sie unter [Beispiele für XML-Eingabedateien &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)   
 [Starten und Verwenden des Datenbankoptimierungsratgebers](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  
