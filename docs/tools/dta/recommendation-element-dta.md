---
title: Recommendation-Element (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 88ee6ad381638147b1b19a515fb3c55cdf0a7447
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="recommendation-element-dta"></a>Recommendation-Element (DTA)
  Enthält Informationen zu den hypothetischen Indizes, die Teil einer benutzerspezifischen Konfiguration sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Optional. Einmalige Verwendung pro **Table** -Element möglich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Table-Element für Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**Untergeordnete Elemente**|[Create Element &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** -Element. Weitere Informationen finden Sie im [XML-Schema des Datenbankoptimierungsratgebers](http://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Hinweise  
 Dieses Element hat den Namen **CreateTypecomplexType** im XML-Schema des Datenbankoptimierungsratgebers. Es wird zur Angabe von Indizes für eine hypothetische Konfiguration verwendet. Dieses **Recommendation** -Element ist nicht mit den anderen Typen identisch, die zum Angeben von Partitionierungen (**RecommendationPType**) oder Sichten (**RecommendationViewType**) verwendet werden können. Unter **XML-Schema des Datenbankoptimierungsratgebers** finden Sie Informationen zu diesen anderen [Recommendation](http://go.microsoft.com/fwlink/?linkid=43100)-Elementtypen.  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
