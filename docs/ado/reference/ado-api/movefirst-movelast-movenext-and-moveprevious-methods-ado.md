---
title: MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (ADO) | Microsoft Docs
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
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b127303e4b74a60e6ef839922bc911c31b360914
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (ADO)
Wechselt zum ersten, letzten, nächsten oder vorherigen Datensatz in einem angegebenen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt und macht, die zum aktuellen Datensatz.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **MoveFirst** -Methode verschieben die Position des aktuellen Datensatzes auf den ersten Eintrag in der **Recordset**.  
  
 Verwenden der **MoveLast** -Methode verschieben die Position des aktuellen Datensatzes bis zum letzten zeichnen Sie in der **Recordset**. Die **Recordset** Objekt muss Lesezeichen oder Bewegung des Cursors nach hinten unterstützen; andernfalls wird der Methodenaufruf ein Fehler generiert.  
  
 Ein Aufruf von **MoveFirst** oder **MoveLast** bei der **Recordset** ist leer (beide **BOF** und **EOF** Gibt "true") wird ein Fehler generiert.  
  
 Verwenden der **MoveNext** -Methode des aktuellen Datensatzes verschieben einen Datensatz vorwärts positionieren (im unteren Teil der **Recordset**). Wenn der letzte Datensatz der aktuelle Datensatz ist ein, und Sie rufen die **MoveNext** -Methode, ADO setzt den aktuellen Datensatz auf die Position hinter dem letzten Datensatz in der **Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) ist **"True"**). Der Versuch, forward When Verschieben der **EOF** Eigenschaft ist bereits **"true"** wird ein Fehler generiert.  
  
 In ADO 2.5 und höher, bei der **Recordset** gefiltert wurde oder sortiert und die Daten des aktuellen Datensatzes geändert werden, Aufrufen der **MoveNext** Methode verschiebt den Cursor zwei Datensätze aus dem aktuellen Datensatz weitergeleitet . Dies liegt daran, wenn der aktuelle Datensatz geändert wird, der nächste Datensatz der aktuelle Datensatz wechselt. Aufrufen von **MoveNext** , nachdem die Änderung aus der neuen aktuellen Datensatz wird der Cursor um einen Datensatz nach vorn verschoben. Dies ist das sich vom Verhalten in ADO 2.1 und früher. Ändern Sie bei diesen älteren Versionen der Daten von einer aktuellen Datensatz in der sortierten oder gefilterten **Recordset** ändert sich nicht auf die Position des aktuellen Datensatzes und **MoveNext** Bewegen des Cursors an den nächsten Datensatz unmittelbar nach der aktuellen Datensatz.  
  
 Verwenden der **MovePrevious** -Methode des aktuellen Datensatzes verschieben positionieren, einen Datensatz nach hinten (weiter oben in der die **Recordset**). Die **Recordset** Objekt muss Lesezeichen oder Bewegung des Cursors nach hinten unterstützen; andernfalls wird der Methodenaufruf ein Fehler generiert. Wenn der erste Datensatz zum aktuellen Datensatz und Sie rufen die **MovePrevious** -Methode ADO legt den aktuellen Datensatz auf die Position vor dem ersten Datensatz in der **Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)ist **"true"**). Der Versuch, When rückwärts Verschieben der **BOF** Eigenschaft ist bereits **"true"** wird ein Fehler generiert. Wenn die **Recordset** Objekt unterstützt keine Lesezeichen oder rückwärtsgerichtete Verschiebung des Cursors, der **MovePrevious** Methode wird ein Fehler generiert.  
  
 Wenn die **Recordset** ist nur vorwärts und unterstützen sowohl vorwärts und rückwärts werden sollen können Sie die [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) Eigenschaft, um einen Datensatzcache zu erstellen, die Bewegung des Cursors nach hinten unterstützt über die [verschieben](../../../ado/reference/ado-api/move-method-ado.md) Methode. Da zwischengespeicherte Datensätze in den Arbeitsspeicher geladen werden, sollten Sie vermeiden, mehrere Datensätze als notwendig Zwischenspeichern. Sie erreichen die **MoveFirst** Methode in einem Vorwärtscursor **Recordset** Objekt; dadurch kann dazu führen, dass den Anbieter den Befehl erneut ausführen, die generiert die **Recordset** Objekt .  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious Methoden Beispiel (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move-Methode (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord-Methode (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
