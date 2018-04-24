---
title: CursorLocation-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ef22aa0aa82071367e9912c31f747cacf7e5075
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="cursorlocation-property-ado"></a>CursorLocation-Eigenschaft (ADO)
Gibt den Speicherort des Cursordiensts.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** -Wert, der auf eine der festgelegt werden kann die [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) Werte.  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaft können Sie zur Wahl zwischen verschiedenen Cursorbibliotheken, die an den Anbieter zugegriffen werden kann. Sie können in der Regel zwischen der Verwendung einer clientseitigen Cursor-Bibliothek oder die befindet sich auf dem Server.  
  
 Die Einstellung dieser Eigenschaft wirkt sich auf Verbindungen nur, nachdem die Eigenschaft festgelegt wurde. Ändern der **CursorLocation** Eigenschaft hat keine Auswirkung auf vorhandene Verbindungen.  
  
 Zurückgegebene Cursor der [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) Methode erben diese Einstellung. **Recordset** Objekte erben diese Einstellung automatisch aus ihren zugeordneten Verbindungen.  
  
 Diese Eigenschaft ist Lese-/Schreibzugriff auf eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) oder geschlossene [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), und auf ein offenes schreibgeschützt **Recordset**.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Recordset** oder **Verbindung** -Objekt, das **CursorLocation** Eigenschaft kann nur festgelegt werden, um **AdUseClient**.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
