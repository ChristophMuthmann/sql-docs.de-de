---
title: CursorType-Eigenschaft (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83302f195c18aee51f0f7fb4c5bfe2d59ae4e882
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cursortype-property-ado"></a>CursorType-Eigenschaft (ADO)
Gibt den Typ der Cursor, mit dem einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) Wert. Der Standardwert ist **AdOpenForwardOnly**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CursorType** Eigenschaft, um den Typ des Cursors anzugeben, die verwendet werden soll, beim Öffnen der **Recordset** Objekt.  
  
 Nur eine Einstellung der **AdOpenStatic** wird unterstützt, wenn die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) -Eigenschaftensatz auf **AdUseClient**. Wenn ein nicht unterstützter Wert festgelegt ist, wird kein Fehler gemeldet. unterstützt die nächstgelegene **CursorType** wird stattdessen verwendet.  
  
 Wenn ein Anbieter den angeforderten Cursortyp nicht unterstützt, wird möglicherweise ein anderer Cursortyp zurückgegeben. Die **CursorType** Eigenschaft ändert sich entsprechend den tatsächlichen Cursortyp verwenden, wenn in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt geöffnet ist. Um bestimmte Funktionen des zurückgegebenen Cursors zu überprüfen, verwenden die [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode. Nach dem Schließen der **Recordset**, **CursorType** Eigenschaft auf die ursprüngliche Einstellung zurückgesetzt.  
  
 Das folgende Diagramm zeigt die Anbieterfunktionalität (identifiziert durch **unterstützt** Methode Konstanten) für jeden Cursortyp erforderlich sind.  
  
|Für ein Recordset mit diesem CursorType|Die Methode unterstützt muss für alle diese Konstanten "true" zurückgeben.|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**zulässt**, **AdHoldRecords**, **AdMovePrevious**, **AdResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**zulässt**, **AdHoldRecords**, **AdMovePrevious**, **AdResync**|  
  
> [!NOTE]
>  Obwohl **unterstützt**(**AdUpdateBatch**) gilt möglicherweise für dynamische "und" Forward-only-Cursor, Batch, die Sie Softwareupdates sollten entweder einen Keyset- oder static-Cursor verwenden. Festlegen der [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) Eigenschaft **AdLockBatchOptimistic** und die **CursorLocation** Eigenschaft **AdUseClient** So aktivieren Sie den Cursor Dienst für OLE DB, die für BatchUpdates erforderlich ist.  
  
 Die **CursorType** Eigenschaft gilt Lese-/Schreibzugriff bei der **Recordset** geschlossen ist, und schreibgeschützt, wenn er geöffnet ist.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Recordset** -Objekt, das **CursorType** Eigenschaft kann nur festgelegt werden **AdOpenStatic**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CursorType LockType und EditMode Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType LockType und EditMode Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports-Methode](../../../ado/reference/ado-api/supports-method.md)
