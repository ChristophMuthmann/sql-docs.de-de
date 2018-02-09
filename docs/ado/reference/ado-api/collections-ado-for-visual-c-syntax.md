---
title: "Auflistungen (ADO für Visual C++-Syntax) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65f6f9875705fee8ea5bcb6adf045ea51ebb7ca7
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="collections-ado-for-visual-c-syntax"></a>Auflistungen (ADO für Visual C++-Syntax)
## <a name="parameters"></a>Parameter  
  
### <a name="methods"></a>Methoden  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Append-Methode (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete-Methode (Parameters-Collection – ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh-Methode (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Eigenschaften  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Count-Eigenschaft (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item-Eigenschaft (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>Felder  
  
### <a name="methods"></a>Methoden  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Append-Methode (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete-Methode (Parameters-Collection – ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh-Methode (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Eigenschaften  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Count-Eigenschaft (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item-Eigenschaft (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>Fehler  
  
### <a name="methods"></a>Methoden  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Refresh-Methode (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Eigenschaften  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Count-Eigenschaft (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item-Eigenschaft (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>Eigenschaften  
  
### <a name="methods"></a>Methoden  
  
```  
Refresh(void);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Refresh-Methode (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Eigenschaften  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 Weitere Informationen finden Sie unter  
  
-   [Count-Eigenschaft (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item-Eigenschaft (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Errors-Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters-Auflistung (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
