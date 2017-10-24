---
title: Kommentare zur HelloData | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b84d5aef9958c15682c6aeae2942487f30a6581
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="comments-on-hellodata"></a>Kommentare zur HelloData
Die HelloData-Anwendung führt Sie durch die grundlegenden Operationen des eine typische ADO-Anwendung: erste, untersuchen, bearbeiten und Aktualisieren von Daten. Wenn Sie die Anwendung starten, klicken Sie auf die erste Schaltfläche **Daten abrufen**. Dies führt die **GetData** Unterroutine.  
  
## <a name="getdata"></a>GetData  
 **GetData** setzt eine gültige Verbindungszeichenfolge in einer Variablen auf Modulebene *M_sConnStr*. Weitere Informationen zu Verbindungszeichenfolgen finden Sie unter [Erstellen der Verbindungszeichenfolge](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Zuweisen ein fehlerhandlers mit einem Visual Basic **OnError** Anweisung. Weitere Informationen zur Fehlerbehandlung in ADO finden Sie unter [Fehlerbehandlung](../../../ado/guide/data/error-handling.md). Ein neues **Verbindung** -Objekt wird erstellt, und die **CursorLocation** -Eigenschaftensatz auf **AdUseClient** daran, dass die HelloData-Beispiel erstellt eine * getrenntes Recordset*. Dies bedeutet, dass, sobald die Daten aus der Datenquelle abgerufen wurden, die physische Verbindung mit der Datenquelle unterbrochen ist, aber Sie können weiterhin arbeiten mit den Daten, die lokal im zwischengespeichert werden Ihre **Recordset** Objekt.  
  
 Nachdem die Verbindung geöffnet wurde, weisen Sie eine SQL-Zeichenfolge an eine Variable (sSQL). Erstellen Sie eine Instanz eines neuen **Recordset** Objekt `m_oRecordset1`. Öffnen Sie in der nächsten Zeile des Codes, der **Recordset** über die vorhandene **Verbindung**, und übergeben Sie `sSQL` als Quelle für die **Recordset**. Hilfsmittel ADO treffen die Entscheidung, dass Sie die SQL-Zeichenfolge übergeben wurden, als Quelle für die **Recordset** ist Textdefinition eines Befehls, übergeben Sie **AdCmdText** in das letzte Argument für die **Recordset öffnen** Methode. Diese Zeile setzt auch die **LockType** und **CursorType** zugeordneten der **Recordset**.  
  
 Die nächste Zeile von Code legt die **MarshalOptions** -Eigenschaft gleich **AdMarshalModifiedOnly**. **MarshalOptions** gibt an, welche Datensätze auf der mittleren Ebene (oder Webserver) gemarshallt werden sollen. Weitere Informationen zum Marshalling finden Sie in der COM-Dokumentation. Bei Verwendung von **AdMarshalModifiedOnly** mit einem clientseitigen Cursor ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **AdUseClient**), nur die Datensätze, die auf geändert wurden die Client zurückgeschrieben werden auf der mittleren Ebene. Festlegen von **MarshalOptions** auf **AdMarshalModifiedOnly** kann die Leistung verbessern, da weniger Zeilen gemarshallt werden.  
  
 Trennen Sie die **Recordset** durch Festlegen seiner **ActiveConnection** -Eigenschaft gleich **nichts**. Weitere Informationen finden Sie im Abschnitt "Trennen und Wiederherstellen der Verbindung das Recordset" in [wird aktualisiert und Beibehalten von Daten](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Schließen Sie die Verbindung mit der Datenquelle, und löschen die vorhandene **Verbindung** Objekt. Dies gibt die Ressourcen, die sie in Anspruch genommen frei.  
  
 Der letzte Schritt besteht, Festlegen der **Recordset** als die **DataSource** für die Microsoft-DataGrid Steuern auf dem Formular so, können Sie leicht anzuzeigen, auf die Daten aus der **Recordset** auf die das Formular.  
  
 Klicken Sie auf die zweite Schaltfläche **Daten untersuchen**. Dadurch wird ausgeführt, die **ExamineData** Unterroutine.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData verwendet verschiedene Methoden und Eigenschaften der **Recordset** Objekt zum Anzeigen von Informationen zu den Daten in der **Recordset**. Es gibt die Anzahl der Datensätze mithilfe der **RecordCount** Eigenschaft. Es durchläuft die **Recordset** und gibt den Wert des der **AbsolutePosition** Eigenschaft in das Textfeld anzeigen, auf dem Formular. Während Sie sich auch in der Schleife, die den Wert des der **Lesezeichen** -Eigenschaft für die dritte Datensatz befindet sich in einer variant-Variablen, *vBookmark*, für die spätere Verwendung.  
  
 Die Routine navigiert direkt an der dritte Datensatz mit der Lesezeichen-Variablen, die sie zuvor gespeichert. Ruft die Routine die **WalkFields** -Unterroutine, die Schleife durchläuft die **Felder** Auflistung von der **Recordset** und zeigt Details zu den einzelnen **Feld ** in der Auflistung.  
  
 Schließlich **ExamineData** verwendet die **Filter** Eigenschaft von der **Recordset** Bildschirm für nur die Datensätze mit einer **CategoryId** gleich 2. Das Ergebnis dieses Filters ist sofort sichtbar, in dem Anzeigeraster, auf dem Formular.  
  
 Weitere Informationen zu der Funktionalität, die der **ExamineData** Unterroutine, finden Sie unter [Untersuchen von Daten](../../../ado/guide/data/examining-data.md).  
  
 Klicken Sie anschließend auf die dritte Schaltfläche **Daten bearbeiten**. Dies führt die **EditData** Unterroutine.  
  
## <a name="editdata"></a>EditData  
 Wenn der Code geht in die **EditData** Unterroutine, die **Recordset** weiterhin gefiltert **CategoryId** gleich 2, sodass nur die Elemente, die den Filterkriterien entsprechen sichtbar. Durchläuft es zuerst den **Recordset** und erhöht den Preis jedes sichtbaren Elements in der **Recordset** um 10 Prozent. Der Wert des der **Preis** Feld geändert, indem die **Wert** Eigenschaft für dieses Feld einen neuen, gültigen Betrag gleich.  
  
 Beachten Sie, dass die **Recordset** nicht mit der Datenquelle verbunden ist. Die Änderungen, die tätigen **EditData** nur für die lokal zwischengespeicherte Kopie der Daten vorgenommen werden. Weitere Informationen finden Sie unter [Bearbeiten von Daten](../../../ado/guide/data/editing-data.md).  
  
 Die Änderungen werden nicht für die Datenquelle vorgenommen werden, bis Sie die vierte Schaltfläche auf **Aktualisierungsdaten**. Dies führt die **UpdateData** Unterroutine.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData entfernt zuerst den Filter, die angewendet wurde die **Recordset**. Der Code entfernt, und setzt `m_oRecordset1` als die **DataSource** für das Microsoft gebunden DataGrid-Steuerelement im Formular, damit die ungefilterte **Recordset** werden im Raster angezeigt.  
  
 Der Code dann prüft, ob Sie rückwärts zu in bewegen können der **Recordset** mithilfe der **unterstützt** Methode mit der **AdMovePrevious** Argument.  
  
 Die Routine mit dem ersten Datensatz verschiebt die **MoveFirst** Methode und zeigt das Feld ursprünglichen und aktuellen Werte mithilfe der **OriginalValue** und **Wert** Eigenschaften der **Feld** Objekt. Diese Eigenschaften werden zusammen mit den **OriginalValue** Eigenschaft (hier nicht verwendet), werden im erläutert [wird aktualisiert und Beibehalten von Daten](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Anschließend wird eine neue **Verbindung** Objekt erstellt und verwendet eine Verbindung mit der Datenquelle her. Sie Verbinden der **Recordset** mit der Datenquelle durch Festlegen der neuen **Verbindung** als der **ActiveConnection** für die **Recordset**. Senden Sie die Updates an den Server, der Code ruft **UpdateBatch** auf die **Recordset**.  
  
 Wenn der, eine Variablen auf Modulebene Flag erfolgreicher Batchaktualisierung `m_flgPriceUpdated`, auf "true" festgelegt ist. Dies wird erinnern Sie später zu bereinigen alle Änderungen, die in der Datenbank vorgenommen wurden.  
  
 Schließlich der Code verschiebt, wieder auf den ersten Eintrag in der **Recordset** und zeigt die ursprünglichen und aktuellen Werte. Die Werte identisch sind, nach dem Aufruf von **UpdateBatch**.  
  
 Ausführliche Informationen zum Aktualisieren von Daten, einschließlich der Vorgehensweise, wenn Daten auf die serveränderungen während Ihrer **Recordset** ist getrennt, finden Sie unter [wird aktualisiert und Beibehalten von Daten](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="formunload"></a>Form_Unload  
 Die **Form_Unload** Unterroutine ist wichtig, verschiedene Ursachen. Zuerst, da dies eine beispielanwendung ist, bereinigt Form_Unload die Änderungen, die in der Datenbank vor dem Beenden der Anwendung vorgenommen wurden. Zweitens im Code wird gezeigt, wie ein Befehl direkt aus einem geöffneten ausgeführt werden kann **Verbindung** Objekt mithilfe der **Execute** Methode. Abschließend wird ein Beispiel für das Ausführen einer Abfrage nicht Zeile zurückgibt (eine UPDATE-Abfrage), für die Datenquelle.

