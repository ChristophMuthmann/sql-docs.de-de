---
title: "Aktueller Datensatz und Größe der Recordset | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6cc6f4bbded2e78203d95820cc590f6c69380fcd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="current-record-and-size-of-recordset"></a>Aktueller Datensatz und Größe des Recordsets
In diesem Abschnitt wird beschrieben, wie die aktuelle Position des Cursors im Beispiel finden **Recordset** in [JScript-Codebeispiel wird ein Recordset zurückzugebenden](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Aktueller Datensatz  
 Der aktuelle Datensatz im Dataset entspricht, die durch die Position des Cursors von gezeigt die **Recordset** Objekt. Wenn eine **Recordset** Objekt wird aus der Datenquelle zurückgegeben, als das Ergebnis des Aufrufs **Recordset.Open**, **Recordset.Open**, oder **Connection.Execute**  (einschließlich **Connection.NamedCommand** und **Connection.StoredProcedure**), der Cursor wird festgelegt, dass beim ersten Datensatz verweist. In das Beispieldataset ist der anfängliche aktuellen Datensatz der "Onkel Bobs organischem Dried Pears" Element.  
  
## <a name="size-of-recordset"></a>Größe des Recordsets  
 Zum Ermitteln der Größe einer **Recordset** Objekt, rufen Sie den Wert von der **Recordset.RecordCount** Eigenschaft. Dieser Wert ist ein long integer-Wert, der die Anzahl der Datensätze in angibt der **Recordset**. Wenn das Dataset aus der OLE DB-Anbieter für Microsoft SQL Server zurückgegeben wird, wird mit diesem Wert die Anzahl der zurückgegebenen Zeilen. Lesen der **RecordCount** Eigenschaft für ein geschlossenes **Recordset** verursacht einen Fehler.  
  
 Wenn die Anzahl der Datensätze bestimmt werden kann, ist der Wert der Eigenschaft – 1.  
  
 Der Wert, der die **RecordCount** Eigenschaft hängt auch die Funktionen des Anbieters und den Typ des Cursors verwendet. Für einen Vorwärtscursor ist der Wert-1 auf. Für eine statische oder keysetgesteuerte Cursor der Wert ist die tatsächliche Anzahl der zurückgegebenen Datensätze in der **Recordset** Objekt. Bei einem dynamischen Cursor ist der Wert-1 oder die tatsächliche Anzahl von Datensätzen, abhängig von der Datenquelle.  
  
 Ein Cursor, der unterstützt **Recordcount** müssen Arbeit schwieriger, und daher erfordert mehr rechenleistung als ein Cursor nicht unterstützt **Recordcount**. Wenn Sie nicht die Anzahl der Datensätze kennen müssen, können anderen Cursortyps Informationen verbessern die Leistung Ihrer Anwendung, insbesondere dann, wenn Sie ein großes DataSet behandelt werden müssen.  
  
 In einigen Fällen ein Anbieter oder der Cursor ist nicht ermitteln der **RecordCount** Wert ohne zuerst alle Datensätze aus der Datenquelle abrufen. Aufrufen, um sicherzustellen, dass genau zählen, die **Recordset**. **MoveLast** Methode vor dem Aufruf **Recordset.RecordCount**.  
  
 Im Beispiel **Recordset** -Objekt abgerufen, mit der [JScript-Codebeispiel](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) verwendet einen Vorwärtscursor, deshalb wird beim Aufrufen **RecordCount** für dieses Objekt führt immer -1. Wenn Sie die Zeile des Codes ändern, die Aufrufe der **Recordset**. **Open** Methode, wie im folgenden Beispiel dargestellt die **RecordCount** Eigenschaft gibt die tatsächliche Anzahl der abgerufenen Datensätze zurück.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Grund hierfür ist, statische Cursor mit dem [Microsoft OLE DB-Anbieter für SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) unterstützen **RecordCount**. In diesem Beispiel fünf Datensätze vorliegen und somit **RecordCount** sollte den Wert 5 ergeben.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
 [Grenzen eines Recordsets](../../../ado/guide/data/boundaries-of-a-recordset.md)
