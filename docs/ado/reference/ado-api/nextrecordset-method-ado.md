---
title: NextRecordset-Methode (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fa92f2d14f270f31a44e3512b78b905debbc90c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="nextrecordset-method-ado"></a>NextRecordset-Methode (ADO)
Löscht die aktuelle [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt und gibt die nächste **Recordset** durch eine Reihe von Befehlen gelangt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Recordset** Objekt. Im Syntaxmodell *recordset1* und *recordset2* kann derselbe Pfad werden **Recordset** -Objekt, oder Sie können separate Objekte verwenden. Verwendung von separaten **Recordset** Objekte, die Zurücksetzen der **ActiveConnection** Eigenschaft auf die ursprüngliche **Recordset** (*recordset1*) nach dem **NextRecordset** wird aufgerufen wurde ein Fehler generiert.  
  
#### <a name="parameters"></a>Parameter  
 *RecordsAffected*  
 Optional. Ein **lange** Variablen, zu dem der Anbieter gibt die Anzahl der Datensätze, die der aktuelle Vorgang betroffen.  
  
> [!NOTE]
>  Dieser Parameter gibt nur die Anzahl der von einem Vorgang betroffenen Datensätze zurück. Anzahl der Datensätze werden nicht von einer select-Anweisung verwendet, um generieren zurückgegeben der **Recordset**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **NextRecordset** Methode zum Zurückgeben der Ergebnisse von den nächsten Befehl in einer zusammengesetzten Command-Anweisung oder einer gespeicherten Prozedur, die mehrere Ergebnisse zurückgibt. Wenn Sie öffnen ein **Recordset** -Objekt auf Grundlage einer zusammengesetzten Command-Anweisung (z. B. "wählen \* von table1; SELECT \* von table2 ") mit der [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode auf eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) oder [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode auf eine **Recordset**, ADO führt nur den ersten Befehl aus und gibt die Ergebnisse in *Recordset*. Um die Ergebnisse der nachfolgenden Befehle in der Anweisung zuzugreifen, rufen die **NextRecordset** Methode.  
  
 Als zusätzliche Ergebnisse vorhanden sind und die **Recordset** nicht getrennt oder über Prozessgrenzen hinweg, gemarshallt wird, enthält die verbundanweisungen der **NextRecordset** Methode weiterhin zurückgeben **Recordset** Objekte. Wenn ein Zeile zurückgeben-Befehl erfolgreich ausgeführt wird, aber keine Datensätze, die den zurückgegebenen gibt **Recordset** Objekt wird geöffnet, aber leer sein. Tests für diesen Fall, indem Sie überprüfen, ob die [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) und [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) Eigenschaften sind beide **"true"**. Wenn ein Befehl nicht Zeile zurückgeben erfolgreich, das zurückgegebene ausgeführt wird **Recordset** Objekt wird geschlossen, die können Sie Tests überprüfen, ob die [Status](../../../ado/reference/ado-api/state-property-ado.md) Eigenschaft auf die **Recordset**. Wenn es keine weiteren Ergebnisse sind *Recordset* festgelegt, um *nichts*.  
  
 Die **NextRecordset** Methode ist nicht verfügbar, auf einem getrennten **Recordset** Objekt, in dem [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) vorsieht **nichts**(in Microsoft Visual Basic) oder NULL (in anderen Sprachen).  
  
 Ist eine Bearbeitung ausgeführt, während Sie sich im sofortupdatemodus, Aufrufen der **NextRecordset** Methode wird ein Fehler generiert, rufen Sie die [aktualisieren](../../../ado/reference/ado-api/update-method.md) oder [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode erste.  
  
 Zum Übergeben von Parametern für mehr als einen Befehl in die verbundanweisung durch Ausfüllen der [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Sammlung oder durch Übergeben eines Arrays mit dem ursprünglichen **öffnen** oder **Execute** aufrufen, müssen die Parameter in der gleichen Reihenfolge in der Auflistung oder ein Array als den dazugehörigen Befehlen in der Reihe Befehl sein. Lesen alle Ergebnisse vor dem Lesen Ausgabeparameterwerte muss abgeschlossen werden.  
  
 OLE DB-Anbieter bestimmt, wenn jeder Befehl in einer verbundanweisung ausgeführt wird. Die [Microsoft OLE DB-Anbieter für SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), z. B. alle Befehle in einem Batch nach dem Empfang der verbundanweisung führt. Das resultierende **Recordsets** werden einfach zurückgegeben werden, wenn Sie rufen **NextRecordset**.  
  
 Allerdings können andere Anbieter ausgeführt werden, den nächsten Befehl in einer Anweisung nur nachdem NextRecordset aufgerufen wird. Bei diesen Anbietern, wenn Sie explizit schließen, die **Recordset** Objekt vor dem Ausführen in Einzelschritten, über die gesamte Command-Anweisung ADO nie der restlichen Befehle ausführt.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [NextRecordset-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset-Methode – Beispiel (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
