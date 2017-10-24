---
title: Optimieren Sie die Eigenschaft dynamisch (ADO) | Microsoft Docs
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
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4aeae41d865e585c4c8b93c86bd6f8e9753eaea1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="optimize-property-dynamic-ado"></a>Optimieren Sie die Eigenschaft dynamisch (ADO)
Gibt an, ob ein Index erstellt werden soll, auf eine [Feld](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **booleschen** Wert, der angibt, ob ein Index erstellt werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Ein Index kann steigern der Leistung von Vorgängen zum Suchen und Sortieren der Werte in einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Der Index ist für ADO intern; Sie können nicht explizit Zugriff auf oder in Ihrer Anwendung verwenden.  
  
 Um einen Index für ein Feld erstellen, legen die **optimieren** Eigenschaft **"true"**. Um den Index zu löschen, legen Sie diese Eigenschaft auf **"false"**.  
  
 **Optimieren** wird an eine dynamische Eigenschaft angefügt der [Feld](../../../ado/reference/ado-api/field-object.md) Objekt [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung bei der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaftensatz zu **AdUseClient**.  
  
## <a name="usage"></a>Verwendung  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>Gilt für  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Optimieren Sie die Beispiel-Eigenschaft (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Optimieren Sie die Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Filter-Eigenschaft](../../../ado/reference/ado-api/filter-property.md)   
 [Find-Methode (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort-Eigenschaft](../../../ado/reference/ado-api/sort-property.md)

