---
title: Fields-Auflistung | Microsoft Docs
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
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4482e9270032e16ea805fde065175f5ce8a10784
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="the-fields-collection"></a>Fields-Auflistung
Die **Felder** Auflistung ist eine systeminterne Funktion der ADO-Auflistungen. Eine Auflistung ist eine geordnete Menge von Elementen, die auf die als Einheit verwiesen werden kann. Weitere Informationen zu Sammlungen ADO finden Sie unter [der ADO-Objektmodell](../../../ado/guide/data/ado-objects-and-collections.md).  
  
 Die **Felder** Auflistung enthält ein **Feld** -Objekt für jedes Feld (Spalte) in der **Recordset**. Wie alle Auflistungen von ADO, er hat **Anzahl** und **Element** Eigenschaften als auch **Append** und **aktualisieren** Methoden. Sie hat auch **CancelUpdate**, **löschen**, **Resync**, und **Update** -Methoden, die nicht mit anderen Sammlungen ADO verfügbar sind.  
  
## <a name="examining-the-fields-collection"></a>Untersuchen der Fields-Auflistung  
 Betrachten Sie die **Felder** Auflistung des Beispiels **Recordset** eingeführt, die in diesem Abschnitt. Im Beispiel **Recordset** abgeleitet wurde, aus der SQL-Anweisung  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 Daher sollten Sie suchen, die die **Recordset Fields** Auflistung enthält drei Felder.  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 Dieser Code einfach bestimmt die Anzahl der **Feld** Objekte in der **Felder** Auflistung mithilfe der **Anzahl** Eigenschaft und durchläuft die Auflistung, der Wert von die **Namen** Eigenschaft für die einzelnen **Feld** Objekt. Sie können viele weitere **Feld** Eigenschaften zum Abrufen von Informationen zu einem Feld. Weitere Informationen zum Abfragen einer **Feld**, finden Sie unter [Field-Objekt](../../../ado/guide/data/the-field-object.md).  
  
## <a name="counting-columns"></a>Zählen von Spalten  
 Wie zu erwarten, die **Anzahl** Eigenschaft gibt die tatsächliche Anzahl von **Feld** Objekte in der **Felder** Auflistung. Nummerierung für Mitglieder einer Sammlung mit 0 (null) beginnt, Sie sollten immer code Schleifen, beginnend mit 0 (null) dem Element und endend mit dem Wert der **Anzahl** Eigenschaft minus 1. Wenn Sie Microsoft Visual Basic verwenden und, die Mitglieder einer Sammlung ohne Überprüfung durchlaufen möchten die **Anzahl** -Eigenschaft die **für jede... Nächste** Befehl.  
  
 Wenn die **Anzahl** Eigenschaft ist 0 (null), es sind keine Objekte in der Auflistung.  
  
## <a name="getting-to-the-field"></a>Beim Einstieg in das Feld  
 Wie bei jeder ADO-Auflistung, die **Element** Eigenschaft ist die Standardeigenschaft der Auflistung. Gibt die einzelnen **Feld** durch seinen Namen angegebenen Objekt oder einen Index, die an sie übergeben. Daher sind die folgenden Anweisungen für das Beispiel entsprechende **Recordset**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 Wenn diese Methoden äquivalent sind, ist die beste? Es setzt. Verwenden einen Index zum Abrufen einer **Feld** aus der Auflistung ist schneller, da er greift auf die **Feld** ohne eine Zeichenfolgensuche ausgeführt. Andererseits, die Reihenfolge der **Felder** innerhalb der Sammlung muss bekannt sein, und wenn sich die Reihenfolge ändert, den Verweis auf die **des Felds** Index müssen geändert werden, wo es auftritt. Obwohl etwas langsamer, mit dem Namen des der **Feld** ist flexibler, da es nicht auf der Reihenfolge des abhängig ist die **Felder** in der Auflistung.  
  
## <a name="using-the-refresh-method"></a>Verwenden die Refresh-Methode  
 Im Gegensatz zu einigen anderen ADO Auflistungen mit den **aktualisieren** Methode für die **Felder** Auflistung wirkt sich nicht sichtbar. Abrufen von Änderungen aus der Struktur der zugrunde liegenden Datenbank müssen Sie verwenden Sie entweder die **Requery** -Methode, oder, wenn die **Recordset** Objekt unterstützt keine Lesezeichen, die **MoveFirst**Methode, wodurch den Befehl für den Anbieter erneut ausgeführt werden.  
  
## <a name="adding-fields-to-a-recordset"></a>Hinzufügen von Feldern zu einem Recordset  
 Die **Append** Methode wird verwendet, um Felder zum Hinzufügen einer **Recordset**.  
  
 Können Sie die **Append** aufzurufende Methode erstellt eine **Recordset** programmgesteuert, ohne eine Verbindung mit einer Datenquelle öffnen. Wird ein Laufzeitfehler auftreten, wenn der **Anfügen** Methode wird aufgerufen, auf der **Felder** Auflistung eines geöffneten **Recordset** oder auf eine **Recordset** in dem die **ActiveConnection** Eigenschaft festgelegt wurde. Sie können nur für Felder Anfügen einer **Recordset** , die nicht geöffnet ist und noch nicht mit einer Datenquelle verbunden. Allerdings Angabe von Werten für das neu angefügte **Felder**, **Recordset** muss zuerst geöffnet werden.  
  
 Entwicklern benötigen häufig eine vorübergehend einige Daten zu speichern, oder möchten einige Daten zu verwenden, als hätte er einen Server stammt, damit bei der Datenbindung in einer Benutzeroberfläche einbezogen werden können. ADO (in Verbindung mit der [Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) kann der Entwickler erstellt ein leeres **Recordset** Objekt, indem Sie die Informationen in der Spalte angeben und Aufrufen **Öffnen**. Im folgenden Beispiel werden drei neue Felder zu einer neuen angefügt **Recordset** Objekt. Die **Recordset** geöffnet wird, zwei neue Einträge hinzugefügt werden, und die **Recordset** in einer Datei gespeichert wird. (Weitere Informationen zu **Recordset** Persistenz, finden Sie unter [wird aktualisiert und Beibehalten von Daten](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 Die Verwendung der **Felder anfügen** Methoden unterscheiden sich zwischen der **Recordset** Objekt und die **Datensatz** Objekt. Weitere Informationen zu den **Datensatz** Objekt, finden Sie unter [Datensätze und Datenströme](../../../ado/guide/data/records-and-streams.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Fabricating Hierarchical Recordsets (Herstellen hierarchischer Recordsets)](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
