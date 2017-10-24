---
title: "Auflistungen (ADO für Visual C++-Syntax) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d16122393fb3a81f90b6e8d708377745a2ef1236
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
-   [Delete-Methode (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
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
  
-   [Delete-Methode (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
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
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

