---
title: Position-Eigenschaft (ADO) | Microsoft Docs
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
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: adb889b4f1741160aa16a6d0866bfbb45c9942fa
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="position-property-ado"></a>Positionseigenschaft (ADO)
Gibt die aktuelle Position innerhalb einer [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** Wert, der den Offset in Anzahl von Bytes, die von der aktuellen Position vom Anfang des Streams angibt. Der Standardwert ist 0, d. h. das erste Byte im Stream darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Die aktuelle Position kann bis zu einem Zeitpunkt nach dem Ende des Streams verschoben werden. Bei Angabe von der aktuellen Position hinter dem Ende des Streams, der [Größe](../../../ado/reference/ado-api/size-property-ado-stream.md) von der **Stream** Objekt wird entsprechend erhöht werden. Auf diese Weise hinzugefügten neuen Bytes werden als null sein.  
  
> [!NOTE]
>  **Position** immer misst Bytes. Multiplizieren Sie für Textstreams mit Mehrbyte-Zeichensätzen die Position mit Zeichengröße zur Bestimmung der Anzahl von Zeichen ein. Für einen Doppelbyte-Zeichensatz ist das erste Zeichen an Position 0, das zweite Zeichen an Position 2, das dritte Zeichen an Position 4 und So weiter.  
  
> [!NOTE]
>  Negative Werte können nicht verwendet werden, so ändern Sie die aktuelle Position in einer **Stream**. Nur positive Zahlen verwendet werden können, für die **Position**.  
  
> [!NOTE]
>  Für nur-Lese **Stream** Objekte aufweist, ADO wird kein Fehler zurückgegeben, wenn **Position** wird festgelegt auf einen Wert größer als die **Größe** von der **Stream**. Dies ändert nicht die Größe des der **Stream**, oder Ändern der **Stream** Inhalt in keiner Weise. Allerdings auf diese Weise sollte vermieden werden, da dies zu einem bedeutungslos führt **Position**Wert.  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Charset-Eigenschaft (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
