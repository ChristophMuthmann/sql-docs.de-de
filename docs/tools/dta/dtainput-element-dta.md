---
title: DTAInput-Element (DTA) | Microsoft Docs
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
helpviewer_keywords: DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0ee58e6b5ec7215353296a1b17151b2354eb5e2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="dtainput-element-dta"></a>DTAInput-Element (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Enthält die Definition der XML-Eingabe für den Datenbankmodul-Optimierungsratgeber.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmale|Description|  
|---------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional einmalig pro **DTAXML** -Element.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[DTAXML-Element &#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)|  
|**Untergeordnete Elemente**|[Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md)<br /><br /> [Workload-Element &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)<br /><br /> [TuningOptions-Element &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)<br /><br /> [Configuration-Element &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
  
## <a name="remarks"></a>Hinweise  
 Dieses Element ist der Stamm der Eingabeschemahierarchie des Datenbankoptimierungsratgebers. Bei Eingaben in den Datenbankoptimierungsratgeber kann es sich um Argumente handeln, mit denen die Server angegeben werden, deren Datenbanken Sie optimieren möchten, oder auch Arbeitsauslastungen, Optimierungsoptionen bzw. eine benutzerspezifische Konfiguration.  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung des **DTAInput**-Elements finden Sie unter [Beispiel für eine einfache XML-Eingabedatei &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
