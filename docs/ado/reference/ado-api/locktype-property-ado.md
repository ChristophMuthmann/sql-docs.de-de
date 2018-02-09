---
title: LockType-Eigenschaft (ADO) | Microsoft Docs
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
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 231ca93c71468fc46ed7729170b2c58e224b1d6f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="locktype-property-ado"></a>LockType Property (ADO)
Gibt den Typ der Sperren auf Datensätze während der Bearbeitung.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) Wert. Der Standardwert ist **AdLockReadOnly**.  
  
## <a name="remarks"></a>Hinweise  
 Legen Sie die **LockType** Eigenschaft vor dem Öffnen einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) angeben, welche Art von Sperren des Anbieters verwenden soll, beim Öffnen. Lesen die Eigenschaft, um die Sperren auf ein offenes Rückgabetyp **Recordset** Objekt.  
  
 Anbieter unterstützen möglicherweise nicht alle Typen von Sperren. Wenn ein Anbieter nicht die angeforderte unterstützt **LockType** festlegen, ersetzen sie einen anderen Typ von Sperren. Um zu bestimmen, die eigentliche Sperre Funktionen, die in einem **Recordset** -Objekts die [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode mit **AdUpdate** und **AdUpdateBatch**.  
  
 Die **AdLockPessimistic** Einstellung wird nicht unterstützt, wenn die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) -Eigenschaftensatz auf **AdUseClient**. Wenn ein nicht unterstützter Wert festgelegt ist, wird kein Fehler gemeldet. unterstützt die nächstgelegene **LockType** wird stattdessen verwendet.  
  
 Die **LockType** Eigenschaft gilt Lese-/Schreibzugriff bei der **Recordset** geschlossen ist, und schreibgeschützt, wenn er geöffnet ist.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Recordset** -Objekt, das **LockType** Eigenschaft kann nur festgelegt werden, um **AdLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CursorType LockType und EditMode Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType LockType und EditMode Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch-Methode (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
