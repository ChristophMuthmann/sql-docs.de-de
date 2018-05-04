---
title: Namespaces | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93a3aca2aee11ed1f78fb33ca286b171a28f62d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="namespaces"></a>Namespaces
Die XML-Format die Persistenz in ADO verwendet die folgenden vier Namespaces.  
  
## <a name="remarks"></a>Hinweise  
 Die XML-Format die Persistenz in ADO verwendet die folgenden vier Namespaces.  
  
|Präfix|Description|  
|------------|-----------------|  
|s|Bezieht sich auf den "XML-Data"-Namespace enthält die Elemente und Attribute, die das Schema von den aktuellen Recordset zu definieren.|  
|DT|Bezieht sich auf die Definitionen der Datentypspezifikation.|  
|rs|Bezieht sich auf die enthaltenden Namespace-Elementen und Attributen, die spezifisch für ADO-Recordset-Eigenschaften und Attribute.|  
|z|Bezieht sich auf das Schema des aktuellen Rowsets.|  
  
 Ein Client sollte nicht auf diese Namespaces einen eigenen Tags hinzufügen, gemäß der Spezifikation. Angenommen, ein Client sollte nicht definieren Sie einen Namespace als "Urn: Schemas-Microsoft-Com:rowset" und dann ausgeschrieben etwas wie z. B. "Rs: MyOwnTag." Weitere Informationen zu Namespaces finden Sie unter der [W3C-Namespaces in XML-Empfehlung](http://www.w3.org/TR/REC-xml-names/).  
  
> [!IMPORTANT]
>  Die ID für das Schema-Tag muss "RowsetSchema lauten", und der Namespace, der zum Verweisen auf das Schema des aktuellen Rowsets muss zeigen Sie auf "#RowsetSchema."  
  
 Beachten Sie, dass das Präfix des Namespace, der Teil zwischen dem Doppelpunkt und dem Gleichheitszeichen – ist willkürlich.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 Der Benutzer können diese Option, um einen beliebigen Namen werden, solange dieser Name in der XML-Dokument einheitlich verwendet wird. ADO schreibt immer "s", "Rs,", "dt" und "Z", doch diese Präfixnamen sind nicht hartcodiert Komponente laden.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
