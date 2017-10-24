---
title: Seek (Methode) | Microsoft Docs
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
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d401bca51d735b2d0d633716cee732ad2ab9a086
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="seek-method"></a>Seek-Methode
Sucht den Index des eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) schnell die Zeile finden, die mit den angegebenen Werten übereinstimmt, und ändert die aktuelle Zeilenposition Zeile.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parameter  
 *KeyValues*  
 Ein Array von **Variant** Werte. Ein Index besteht aus einer oder mehreren Spalten und das Array enthält einen Wert, für jede einzelne Spalte verglichen werden soll.  
  
 *SeekOption*  
 Ein [SeekEnum](../../../ado/reference/ado-api/seekenum.md) Wert, der angibt, den Typ des Vergleichs zwischen den Spalten des Indexes und das entsprechende erfolgen *KeyValues*.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Seek** Methode in Verbindung mit der [Index](../../../ado/reference/ado-api/index-property.md) Eigenschaft, wenn der zugrunde liegende Anbieter Indizes unterstützt die **Recordset** Objekt. Verwenden der [unterstützt](../../../ado/reference/ado-api/supports-method.md)**(AdSeek)** Methode, um zu bestimmen, ob der zugrunde liegende Anbieter unterstützt **Seek**, und die **Supports(adIndex)** Methode, um zu bestimmen, ob der Anbieter Indizes unterstützt. (Z. B. die [OLE DB-Anbieter für Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) unterstützt **Seek** und **Index**.)  
  
 Wenn **Seek** befindet sich nicht Suchen der gewünschten Zeile, kein Fehler auftritt, und für die Zeile am Ende der **Recordset**. Legen Sie die **Index** Eigenschaft auf den gewünschten Index vor dem Ausführen dieser Methode.  
  
 Diese Methode ist nur mit serverseitiger Cursor unterstützt. Seek nicht unterstützt, wenn die **Recordset** des Objekts [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaftswert ist **AdUseClient**.  
  
 Diese Methode kann nur verwendet werden, wenn die **Recordset** Objekt mit geöffnet wurde eine [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) Wert **AdCmdTableDirect**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Seek-Methode und Eigenschaft Beispiel eines Indexes (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Seek-Methode und Index-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find-Methode (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Index-Eigenschaft](../../../ado/reference/ado-api/index-property.md)

