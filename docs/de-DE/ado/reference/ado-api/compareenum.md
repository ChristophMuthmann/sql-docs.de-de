---
title: CompareEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareEnum
helpviewer_keywords:
- CompareEnum enumeration [ADO]
ms.assetid: bc8f710d-0621-4673-8d8e-0361e44abed0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db29f164e3329044f0d4ed12d2353e206bb87172
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="compareenum"></a>CompareEnum
Gibt die relative Position von zwei Datensätzen, die durch ihre Lesezeichen dargestellt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adCompareEqual**|1|Gibt an, dass die Textmarken gleich sind.|  
|**adCompareGreaterThan**|2|Gibt an, dass das erste Lesezeichen nach der zweiten ist.|  
|**adCompareLessThan**|0|Gibt an, dass das erste Lesezeichen vor dem zweiten ist.|  
|**adCompareNotComparable**|4|Gibt an, dass die Textmarken nicht verglichen werden können.|  
|**adCompareNotEqual**|3|Gibt an, dass die Textmarken nicht gleich und nicht sortiert sind.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.Compare.EQUAL|  
|AdoEnums.Compare.GREATERTHAN|  
|AdoEnums.Compare.LESSTHAN|  
|AdoEnums.Compare.NOTCOMPARABLE|  
|AdoEnums.Compare.NOTEQUAL|  
  
## <a name="applies-to"></a>Gilt für  
 [CompareBookmarks-Methode (ADO)](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CompareBookmarks-Methode (ADO)](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)
