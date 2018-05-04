---
title: Move-Methode (ADO) | Microsoft Docs
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
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a64cfae0055f3052a75886556b7493fb096105a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="move-method-ado"></a>Move-Methode (ADO)
Verschiebt die Position des aktuellen Datensatzes in einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parameter  
 *NumRecords*  
 Eine signierte **lange** Ausdruck, der die Anzahl der Datensätze angibt, das die Position des aktuellen Datensatzes bewegt.  
  
 *Start*  
 Optional. Ein **Zeichenfolge** Wert oder **Variant** , die ein Lesezeichen ergibt. Sie können auch eine [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) Wert.  
  
## <a name="remarks"></a>Hinweise  
 Die **verschieben** Methode wird für alle unterstützt **Recordset** Objekte.  
  
 Wenn die *NumRecords* Argument ist größer als 0 (null), die Position des aktuellen Datensatzes rückt vor (gegen Ende der **Recordset**). Wenn *NumRecords* ist kleiner als 0 (null), die Position des aktuellen Datensatzes verschiebt diesen rückwärts (bis zum Anfang der **Recordset**).  
  
 Wenn die **verschieben** aufrufen würde die Position des aktuellen Datensatzes zu einem Zeitpunkt vor dem ersten Datensatz verschoben wird, ADO wird des aktuellen Datensatzes auf die Position vor dem ersten Datensatz des Recordsets ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) ist **"true"** ). Der Versuch, When rückwärts Verschieben der **BOF** Eigenschaft ist bereits **"true"** wird ein Fehler generiert.  
  
 Wenn die **verschieben** Aufruf würde die Position des aktuellen Datensatzes zu einem Zeitpunkt nach dem letzten Datensatz verschieben, ADO setzt den aktuellen Datensatz auf die Position hinter dem letzten Datensatz im Recordset ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) ist **"true"** ). Der Versuch, forward When Verschieben der **EOF** Eigenschaft ist bereits **"true"** wird ein Fehler generiert.  
  
 Aufrufen der **verschieben** Methode aus einer leeren **Recordset** Objekt wird ein Fehler generiert.  
  
 Wenn Sie übergeben die *starten* Argument der Verschiebevorgang ist relativ zu dem Datensatz mit diesem Lesezeichen, vorausgesetzt die **Recordset** Objekt Lesezeichen unterstützt. Wenn nicht angegeben, ist die Verschiebung relativ zum aktuellen Datensatz.  
  
 Bei Verwendung der [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) Eigenschaft lokal Datensätze aus den Anbieter übergeben Zwischenspeichern ein *NumRecords* Argument, das die Position des aktuellen Datensatzes außerhalb der aktuellen Gruppe der zwischengespeicherten Datensätze verschiebt Erzwingt, dass ADO, um eine neue Gruppe von Datensätzen, beginnend mit dem Zieldatensatz abzurufen. Die **CacheSize** Eigenschaft bestimmt die Größe der neu abgerufenen Gruppe, und der Zieldatensatz ist der erste Datensatz abgerufen.  
  
 Wenn die **Recordset** Objekt ist eine vorwärtsenumeration, ein Benutzer kann weiterhin übergeben, eine *NumRecords* Argument kleiner als 0 (null), zur Verfügung gestellt, das Ziel ist in den aktuellen Satz von zwischengespeicherten Einträge. Wenn die **verschieben** Aufruf würde verschieben Sie die Position des aktuellen Datensatzes zu einem Datensatz vor dem ersten zwischengespeicherten Datensatz wird eine Fehlermeldung angezeigt. Daher können Sie einen Datensatzcache verwenden, der über einen Anbieter, der Bildlauf ausschließlich vorwärts ausgeführt unterstützt vollständige Bildlauf unterstützt. Da zwischengespeicherte Datensätze in den Arbeitsspeicher geladen werden, sollten Sie vermeiden, Zwischenspeichern mehr Datensätze als erforderlich sind. Auch wenn ein Vorwärtscursor **Recordset** aufrufen Objekt unterstützt das rückwärts bewegt wird, auf diese Weise die [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) Methode für ein beliebiges Vorwärtscursor **Recordset** Objekt weiterhin ein Fehler generiert.  
  
> [!NOTE]
>  Unterstützung für in einem Vorwärtscursor rückwärts verschieben **Recordset** ist nicht vorhersagbar, abhängig von Ihren Anbieter. Wenn der aktuelle Datensatz nach dem letzten Datensatz in positioniert wurde hat die **Recordset**, **verschieben** Abwärtskompatibilität führt möglicherweise nicht die richtige aktuelle Position zu.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Move-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move-Methode (Beispiel) (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move-Methode (VC++-Beispiel)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord-Methode (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
