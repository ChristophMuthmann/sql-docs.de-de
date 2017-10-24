---
title: "\"PageCount\"-Eigenschaft (ADO) | Microsoft Docs"
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
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 44759f9316e46be72120febd022f9a47554eb6bd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pagecount-property-ado"></a>"PageCount"-Eigenschaft (ADO)
Gibt an, wie viele Seiten mit Daten der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **lange** -Wert, der die Anzahl der Seiten in der **Recordset**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **"PageCount"** -Eigenschaft können Sie bestimmen, wie viele Seiten der Daten werden die **Recordset** Objekt. *Seiten* sind Gruppen von Datensätzen, dessen Größe gleich, der [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) Einstellung der Eigenschaft. Auch wenn die letzte Seite unvollständig ist, da weniger als Datensätze die **PageSize** Wert, zählt als eine zusätzliche Seite in der **"PageCount"** Wert. Wenn die **Recordset** Objekt unterstützt diese Eigenschaft nicht, ist des Werts-1 gibt an, dass die **"PageCount"** Maskierungsstufe ist.  
  
 Finden Sie unter der **PageSize** und [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) Eigenschaften für weitere auf Funktionen der Seite.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePage "PageCount" und PageSize Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage "PageCount" und PageSize Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Die Eigenschaft PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)

