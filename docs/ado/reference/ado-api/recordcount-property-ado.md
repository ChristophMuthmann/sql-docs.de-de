---
title: RecordCount-Eigenschaft (ADO) | Microsoft Docs
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
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7c2a7900d47b2e80227e470219fd7a7566dc41e4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="recordcount-property-ado"></a>RecordCount-Eigenschaft (ADO)

Gibt die Anzahl der Datensätze in einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.
  
## <a name="return-value"></a>Rückgabewert

Gibt eine **lange** -Wert, der die Anzahl der Datensätze in der **Recordset**.
  
## <a name="remarks"></a>Hinweise

Verwenden der **RecordCount** Eigenschaft, um herauszufinden, wie viele Datensätze werden einem **Recordset** Objekt. Die Eigenschaft gibt-1 zurück, wenn ADO die Anzahl der Datensätze bestimmt werden kann oder wenn der Anbieter oder Cursor-Typ nicht unterstützt **RecordCount**. Lesen der **RecordCount** Eigenschaft für ein geschlossenes **Recordset** verursacht einen Fehler.

#### <a name="bookmarks-or-approximate-positioning"></a>Lesezeichen oder ungefähre Positionierung

Wenn das Recordset-Objekt *ist* entweder Lesezeichen unterstützen oder Ungefährer Positionierung, diese Eigenschaft gibt die genaue Anzahl der Datensätze im Recordset. Diese Eigenschaft gibt die genaue Anzahl unabhängig davon, ob das Recordset vollständig aufgefüllt wurde.

Im Gegensatz dazu wird das Recordset-Objekt ist *nicht* unterstützen Lesezeichen oder ungefähre Positionierung, Zugriff auf diese Eigenschaft ist möglicherweise zahlreiche erhebliche Ressourcen. Der Ausgleichsmodus tritt auf, weil alle Datensätze müssen abgerufen und gezählt, um einen genauen RecordCount Wert zurückzugeben.

- **zulässt** im Zusammenhang mit Lesezeichen.
- **AdApproxPosition** bezieht sich auf die ungefähre Positionierung.

> [!NOTE]
> In ADO-Versionen mit 2,8 und früher, ruft der SQLOLEDB-Anbieter alle Datensätze bei ein serverseitigen Cursor trotz der Tatsache verwendet wird, die zurückgegebenen **"true"** für beide **unterstützt (AdApproxPosition)** und **Unterstützt (zulässt)**.
  
Cursor-Datentyp, der die **Recordset** Objekt auswirkt, ob die Anzahl der Datensätze bestimmt werden kann. Die **RecordCount** Eigenschaft-1 für einen Vorwärtscursor; die tatsächliche Anzahl der für einen statischen oder Keysetcursor; und entweder-1 oder die tatsächliche Anzahl der für einen dynamischen Cursor, abhängig von der Datenquelle zurück.
  
## <a name="applies-to"></a>Gilt für

[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch

[Filter- und RecordCount Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter- und RecordCount Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition-Eigenschaft (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
