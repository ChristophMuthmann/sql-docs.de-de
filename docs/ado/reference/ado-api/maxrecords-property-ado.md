---
title: MaxRecords-Eigenschaft (ADO) | Microsoft Docs
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
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 232f515c2250e1ec40fbb28bdff767baf9cf81c5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="maxrecords-property-ado"></a>MaxRecords-Eigenschaft (ADO)
Gibt die maximale Anzahl von Datensätzen, die zum Zurückgeben einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aus einer Abfrage.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** Wert, der die maximale Anzahl der zurückzugebenden Datensätze angibt. Standard ist 0 (null) (**0**), was bedeutet keine Beschränkung.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **MaxRecords** -Eigenschaft können Sie die Anzahl der Datensätze zu begrenzen, die aus der Datenquelle des Anbieters zurückgibt. Die Standardeinstellung dieser Eigenschaft ist 0 (null), was bedeutet, dass der Anbieter gibt alle angeforderten Datensätze zurück.  
  
 Die **MaxRecords** Eigenschaft gilt Lese-/Schreibzugriff bei der **Recordset** geschlossen ist, und schreibgeschützt, wenn er geöffnet ist.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für MaxRecords-Eigenschaft (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   

