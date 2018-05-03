---
title: Clone-Methode (ADO) | Microsoft Docs
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
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eccbb6bea59ff2b99712479bb90cdfb0f0c963a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="clone-method-ado"></a>Clone-Methode (ADO)
Erstellt ein Duplikat [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt aus einer vorhandenen **Recordset** Objekt. Optional gibt an, dass der Klon schreibgeschützt ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Recordset** -Objektverweis.  
  
#### <a name="parameters"></a>Parameter  
 *rstDuplicate*  
 Ein Object-Variablen, die das Duplikat identifiziert **Recordset** zu erstellendes Objekt wäre.  
  
 *rstOriginal*  
 Ein Object-Variablen, die identifiziert die **Recordset** Objekt dupliziert werden.  
  
 *LockType*  
 Optional. Ein [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) Wert, der angibt, die Sperrtyp des ursprünglichen **Recordset**, oder ein schreibgeschütztes **Recordset**. Gültige Werte sind **AdLockUnspecified** oder **AdLockReadOnly**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Klon** Methode zum Erstellen mehrerer dupliziert **Recordset** Objekten, insbesondere, wenn Sie mehr als ein aktuellen Datensatz in einem angegebenen Satz von Datensätzen beibehalten möchten. Mithilfe der **Klon** Methode ist effizienter als das Erstellen und öffnen ein neues **Recordset** -Objekt, wie der ursprüngliche derselben Definition verwendet.  
  
 Die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft des ursprünglichen **Recordset**, sofern vorhanden, werden nicht an den Klon angewendet. Legen Sie die **Filter** -Eigenschaft der neuen **Recordset** zum Filtern der Ergebnisse. Die einfachste Möglichkeit, kopieren Sie alle vorhandenen **Filter** wird der Wert direkt, wie folgt zugewiesen.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 Der aktuelle Datensatz eines neu erstellten Klons wird auf den ersten Eintrag festgelegt.  
  
 Änderungen an einer **Recordset** Objekt aller seiner Klone unabhängig von der Cursortyp sichtbar sind. Allerdings nach dem Ausführen [Requery](../../../ado/reference/ado-api/requery-method.md) am ursprünglichen **Recordset**, Klone werden nicht mehr mit dem ursprünglichen synchronisiert werden.  
  
 Schließen die ursprüngliche **Recordset** seine Datenbankkopien wird nicht geschlossen, ebenso wie nicht schließen schließen eine Kopie der ursprünglichen oder keines der anderen Kopien.  
  
 Sie können nur Klonen eine **Recordset** -Objekt, das Lesezeichen unterstützt. Lesezeichenwerte sind austauschbar. d. h. ein Lesezeichenverweis von einem **Recordset** Objekt bezieht sich auf den gleichen Datensatz in einer seiner Klone.  
  
 Einige **Recordset** Ereignisse, die ausgelöst werden, erfolgt auch in allen **Recordset** klont. Da der aktuelle Datensatz unterscheiden kann allerdings geklont **Recordsets**, die Ereignisse möglicherweise nicht gültig für den Klon. Z. B., wenn Sie einen Wert eines Felds ändern einer [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) -Ereignis tritt in der geänderten **Recordset** und in allen klonen. Die *Felder* Parameter von der **WillChangeField** Ereignis eines geklonten **Recordset** (wobei die Änderung nicht vorgenommen wurde) auf die Felder des aktuellen Datensatzes des Klons verweist Das ist möglicherweise einem anderen Datensatz als den aktuellen Datensatz des ursprünglichen **Recordset** , in dem die Änderung aufgetreten ist.  
  
 Die folgende Tabelle enthält eine vollständige Liste aller **Recordset** Ereignisse. Es gibt an, ob sie gültig ist und für alle Recordsetklone mit generiert ausgelöste sind die **Klon** Methode.  
  
|Ereignis|Im Klone ausgelöst?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|nein|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|nein|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|nein|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|ja|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|nein|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|ja|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|nein|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|ja|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|ja|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|nein|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|nein|  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Clone-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Clone-Methode (Beispiel) (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone-Methode – Beispiel (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
