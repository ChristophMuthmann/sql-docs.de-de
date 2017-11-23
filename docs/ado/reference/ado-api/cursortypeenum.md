---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CursorTypeEnum
helpviewer_keywords: CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5adf070387078902d7d21a68cc0f89af2de8194a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Gibt den Typ der Cursor, mit dem einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Verwendet einen dynamischen Cursor. Hinzufügen, ändern oder Löschen von anderen Benutzern sind sichtbar, und alle Typen der Bewegung durch die **Recordset** sind zulässig, mit Ausnahme von Lesezeichen, wenn der Anbieter diese nicht unterstützt.|  
|**adOpenForwardOnly**|0|Standard. Verwendet einen Vorwärtscursor. Identisch mit einem statischen Cursor, mit dem Unterschied, dass Sie nur vorwärts durch die Datensätze gescrollt werden können. Dies verbessert die Leistung, wenn Sie nur eine pass-through vornehmen müssen eine **Recordset**.|  
|**adOpenKeyset**|1|Verwendet einen Keysetcursor. Wie Sie einen dynamischen Cursor, mit dem Unterschied, dass Sie Einträge, die andere Benutzer hinzufügen möchten, sehen können, obwohl die von anderen Benutzern gelöschten Datensätze aus zugegriffen werden Ihre **Recordset**. Datenänderungen von anderen Benutzern sind weiterhin sichtbar.|  
|**adOpenStatic**|3|Verwendet einen statischen Cursor, also eine statische Kopie einer Gruppe von Datensätzen, die Sie zum Suchen von Daten oder zum Generieren von Berichten verwenden können. Hinzufügungen, Änderungen oder löschungen von anderen Benutzern sind nicht sichtbar.|  
|**adOpenUnspecified**|-1|Gibt nicht den Typ des Cursors an.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Gilt für  
 [CursorType-Eigenschaft (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
