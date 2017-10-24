---
title: RowPosition-Eigenschaft (ADO) | Microsoft Docs
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
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 00206531bf8154d509f79e7229b1a2da319fa5fa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rowposition-property-ado"></a>RowPosition-Eigenschaft (ADO)
Ruft ab oder legt einen OLE DB- **RowPosition** Objekt vom bzw. auf eine **ADORecordsetConstruction** Objekt. Bei Verwendung von **Put_RowPosition** festzulegende der **RowPosition** -Objekt, das resultierende **Recordset** -Objekt verwendet die **RowPosition** -Objekt hinzu Bestimmen der aktuellen Zeile.  
  
 Lese-/Schreibzugriff.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parameter  
 *ppRowPos*  
 Zeiger auf einen OLE DB- **RowPosition** Objekt.  
  
 *PRowPos*  
 OLE DB- **RowPosition** Objekt.  
  
## <a name="return-values"></a>Rückgabewerte  
 Diese Eigenschaftsmethode gibt die standardmäßige HRESULT-Werte, einschließlich S_OK und E_FAIL zurück.  
  
## <a name="remarks"></a>Hinweise  
 Wenn diese Eigenschaft festgelegt wird, wenn die **Rowset** -Objekt, auf die **RowPosition** Objekt unterscheidet sich von der **Rowset** -Objekt, auf die **Recordset**-Objekt, das Erstere überschreibt der zweite Wert. Das gleiche Verhalten trifft auf den aktuellen **Kapitel** von der **RowPosition** ebenfalls.  
  
## <a name="applies-to"></a>Gilt für  
 [ADORecordsetConstruction-Schnittstelle](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)

