---
title: CursorOptionEnum | Microsoft Docs
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
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4acc97166d85e5c55b96405505f4267ee9c8386e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Gibt an, welche Funktionen die [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode sollte für testen.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Unterstützt die [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) Methode, um neue Datensätze hinzufügen.|  
|**adApproxPosition**|0x4000|Unterstützt die [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) und [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) Eigenschaften.|  
|**adBookmark**|0x2000|Unterstützt die [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md) Eigenschaft für den Zugriff auf bestimmte Datensätze.|  
|**adDelete**|0x1000800|Unterstützt die [löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md) Methode zum Löschen von Datensätzen.|  
|**adFind**|0x80000|Unterstützt die [suchen](../../../ado/reference/ado-api/find-method-ado.md) Methode, um eine Zeile in einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Ruft weitere Datensätze ab, oder die nächste Position ändert, ohne dass alle ausstehende Änderungen.|  
|**adIndex**|0x100000|Unterstützt die [Index](../../../ado/reference/ado-api/index-property.md) Eigenschaft um einen Index zu benennen.|  
|**adMovePrevious**|0x200|Unterstützt die [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) und [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) Methoden und [verschieben](../../../ado/reference/ado-api/move-method-ado.md) oder [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) Methoden zum Verschieben des aktuellen Datensatzes rückwärts positionieren. ohne Lesezeichen.|  
|**adNotify**|0x40000|Gibt an, dass der zugrunde liegenden Datenanbieter Benachrichtigungen unterstützt (die bestimmt, ob **Recordset** Ereignisse werden unterstützt).|  
|**adResync**|0x20000|Unterstützt die [Resync](../../../ado/reference/ado-api/resync-method.md) Methode, um den Cursor mit den Daten zu aktualisieren, die in der zugrunde liegenden Datenbank sichtbar ist.|  
|**adSeek**|0x200000|Unterstützt die [Seek](../../../ado/reference/ado-api/seek-method.md) Methode, um eine Zeile in einer **Recordset**.|  
|**adUpdate**|0x1008000|Unterstützt die [Update](../../../ado/reference/ado-api/update-method.md) Methode, um vorhandene Daten zu ändern.|  
|**adUpdateBatch**|0x10000|BatchUpdates unterstützt ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) und [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methoden), Gruppen von Änderungen an den Anbieter zu übertragen.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>Gilt für  
 [Supports-Methode](../../../ado/reference/ado-api/supports-method.md)
