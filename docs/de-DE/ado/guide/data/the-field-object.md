---
title: Field-Objekt | Microsoft Docs
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
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b2fc3f1716f39d5c45aab95c504fef4d9e7437f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="the-field-object"></a>Field-Objekt
Jede **Feld** Objekt entspricht in der Regel an eine Spalte in einer Datenbanktabelle. Allerdings eine **Feld** kann auch einen Zeiger auf einen anderen repräsentieren **Recordset**, einem Kapitel aufgerufen. Ausnahmen, z. B. Kapitelspalten, werden weiter unten in diesem Handbuch behandelt.  
  
 Verwenden der **Wert** Eigenschaft **Feld** Objekte so festlegen oder Zurückgeben von Daten für den aktuellen Datensatz. Abhängig von den Funktionen der Anbieter verfügbar macht, einige Auflistungen, Methoden oder Eigenschaften eine **Feld** Objekt möglicherweise nicht zur Verfügung.  
  
 Mit den Auflistungen, Methoden und Eigenschaften von einer **Feld** -Objekts können Sie folgende Möglichkeiten:  
  
-   Der Name eines Felds zurückgeben, indem die **Namen** Eigenschaft.  
  
-   Anzeigen oder ändern Sie die Daten in das Feld mit der **Wert** Eigenschaft. **Wert** ist die Standardeigenschaft eines der **Feld** Objekt.  
  
-   Zurückgeben der grundlegenden Merkmale eines Felds mithilfe der **Typ**, **Genauigkeit**, und **NumericScale** Eigenschaften.  
  
-   Geben Sie die deklarierte Größe eines Felds mithilfe der **DefinedSize** Eigenschaft.  
  
-   Die tatsächliche Größe der Daten in einem bestimmten Feld zurückgeben, indem die **ActualSize** Eigenschaft.  
  
-   Bestimmen, welche Arten von Funktionen für ein bestimmtes Feld unterstützt werden, mithilfe der **Attribute** Eigenschaft und **Eigenschaften** Auflistung.  
  
-   Bearbeiten Sie die Werte von Feldern, die lange Binär-oder Zeichendaten mithilfe der **AppendChunk** und **GetChunk** Methoden.  
  
 Auflösen von Diskrepanzen in Feldwerten während der Batchaktualisierung mithilfe der **OriginalValue** und **OriginalValue** Eigenschaften, wenn der Anbieter Batchaktualisierungen unterstützt.  
  
## <a name="describing-a-field"></a>Ein Feld beschreiben  
 Besprechen Sie die folgenden Themen werden Eigenschaften der [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt, das Informationen darstellen, die beschreibt die **Feld** Objekt selbst – d. h. Metadaten über das Feld. Diese Informationen kann verwendet werden, um zu bestimmen, viel über das Schema der der **Recordset**. Zu diesen Eigenschaften zählen **Typ**, **DefinedSize** und **ActualSize**, **Namen**, und **NumericScale**und **Genauigkeit**.  
  
### <a name="discovering-the-data-type"></a>Ermitteln des Datentyps  
 Die **Typ** Eigenschaft gibt den Datentyp des Felds an. Der Datentyp, Enumerationskonstanten, die vom ADO unterstützt werden, werden in beschrieben [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) in der *ADO Programmer's Reference*.  
  
 Für numerische Typen, z. B. Gleitkomma **Type**, können Sie weitere Informationen zu erhalten. Die **NumericScale** Eigenschaft gibt an, wie viele Ziffern rechts vom Dezimaltrennzeichen verwendet werden, zur Darstellung von Werten für die **Feld**. Die **Genauigkeit** Eigenschaft gibt die maximale Anzahl von Ziffern für die Darstellung von Werten für die **Feld**.  
  
### <a name="determining-field-size"></a>Bestimmen die Feldgröße  
 Verwenden der **DefinedSize** Eigenschaft zum Ermitteln der Datenkapazität von einem **Feld** Objekt.  
  
 Verwenden der **ActualSize** die tatsächliche Länge der zurückzugebenden Eigenschaft eine **Feld** Wert des Objekts. Für alle Felder der **ActualSize** Eigenschaft ist schreibgeschützt. Wenn die Länge des ADO bestimmt werden kann die **Feld** -Wert des Objekts, das **ActualSize** -Eigenschaft gibt **ActualSize**.  
  
 Die **DefinedSize** und **ActualSize** Eigenschaften verfügen über unterschiedliche Zwecke. Betrachten Sie beispielsweise eine **Feld** Objekt mit dem deklarierten Typ **AdVarChar** und ein **DefinedSize** Eigenschaftswert von 50 enthält ein einzelnes Zeichen. Die **ActualSize** Eigenschaftswert zurückgegeben wird, die Länge in Bytes, der das einzelne Zeichen steht.  
  
### <a name="determining-field-contents"></a>Bestimmen von Feldinhalt  
 Der Bezeichner der Spalte aus der Datenquelle wird dargestellt, indem die **Namen** Eigenschaft von der **Feld**. Die **Wert** Eigenschaft von der **Feld** Objekt zurück, oder legt Sie den tatsächlichen Dateninhalt des Felds. Dies ist die Standardeigenschaft.  
  
 Um die Daten in einem Feld zu ändern, legen die **Wert** -Eigenschaft einen neuen Wert des richtigen Typs gleich. Cursortyp muss Updates, um den Inhalt eines Felds ändern, unterstützen. Validierung der Datenbank erfolgt nicht hier im Batchmodus ausgeführt, daher müssen Sie beim Aufrufen auf Fehler hin geprüft **UpdateBatch** in einem solchen Fall. Einige Anbieter unterstützen außerdem das ADO **Feld** des Objekts **OriginalValue** und **OriginalValue** Eigenschaften bieten Unterstützung beim Lösen von Konflikten, wenn Sie versuchen BatchUpdates ausführen. Weitere Informationen dazu, wie solche Konflikte zu lösen, finden Sie unter [Bearbeiten von Daten](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  **Recordset Field** Werte können nicht festgelegt werden, wenn Sie neue Anfügen **Felder** zu einem **Recordset**. Stattdessen neue **Felder** angefügt werden zu einem geschlossenen **Recordset**. Die **Recordset** zugewiesen werden, geöffnet wird, sowie nur dann kann Werte werden diese **Felder**.  
  
### <a name="getting-more-field-information"></a>Weitere Informationen abrufen  
 ADO-Objekte sind zwei Eigenschaften: integrierte und dynamische. Zu diesem Zeitpunkt sind nur die integrierten Eigenschaften des der **Feld** Objekt haben erläutert wurde.  
  
 Vordefinierte Eigenschaften sind diese Eigenschaften in ADO implementiert und sofort zur Verfügung, um eine neue Objekt mithilfe der `MyObject.Property` Syntax. Sie werden nicht angezeigt, als **Eigenschaft** Objekte in einem Objekt **Eigenschaften** Auflistung.  
  
 Dynamische Eigenschaften werden von der zugrunde liegende Datenanbieter definiert und werden in der **Eigenschaften** Auflistung für den entsprechenden ADO-Objekt. Beispielsweise kann eine Eigenschaft, die spezifisch für den Datenanbieter anzugeben, ob ein **Recordset** Objekt unterstützt, Transaktionen oder aktualisieren. Diese zusätzlichen Eigenschaften hostnamensadresse **Eigenschaft** Objekte in diesem **Recordset** des Objekts **Eigenschaften** Auflistung. Dynamische Eigenschaften verwiesen werden können, nur über die Auflistung, die mit der Syntax `MyObject.Properties(0)` oder `MyObject.Properties("Name")`.  
  
 Beide Arten der Eigenschaft kann nicht gelöscht werden.  
  
 Eine dynamische **Eigenschaft** -Objekt hat vier integrierte Eigenschaften selbst:  
  
-   Die **Namen** Eigenschaft ist eine Zeichenfolge, die die Eigenschaft identifiziert.  
  
-   Die **Typ** Eigenschaft ist eine ganze Zahl, die den Datentyp der Eigenschaft angibt.  
  
-   Die **Wert** Eigenschaft ist eine Variante, die die Einstellung der Eigenschaft enthält. **Wert** ist die Standardeigenschaft für ein **Eigenschaft** Objekt.  
  
-   Die **Attribute** Eigenschaft ist ein **lange** Wert, der die Eigenschaften, die spezifisch für den Datenanbieter angibt.  
  
 Die **Eigenschaften** Auflistung für die **Feld** -Objekt enthält zusätzliche Metadaten über das Feld. Der Inhalt dieser Auflistung variieren je nach Anbieter. Im folgenden Codebeispiel wird untersucht die **Eigenschaften** Auflistung des Beispiels **Recordset** eingeführt, die am Anfang dieses Abschnitts. Es sucht zuerst den Inhalt der Auflistung. Dieser Code verwendet die [OLE DB-Anbieter für SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), sodass die **Eigenschaften** Auflistung enthält Informationen zu diesen Anbieter.  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>Umgang mit Binärdaten  
 Verwenden der [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) Methode auf eine **Feld** Objekt mit dem lange Binär-oder Zeichendatentypen gefüllt. In Situationen, in dem Systemspeicher beschränkt ist, können Sie die **AppendChunk** Methode, um lange Werte in Teilen anstatt in ihrer Gesamtheit zu bearbeiten.  
  
 Wenn die **AdFldLong** bit in der **Attribute** Eigenschaft eine **Feld** -Objekts festgelegt wird, um **"true"**, können Sie die  **AppendChunk** Methode für dieses Feld.  
  
 Die erste **AppendChunk** rufen Sie für eine **Feld** Objekt schreibt Daten in das Feld alle vorhandenen Daten überschrieben. Nachfolgende **AppendChunk** Aufrufe an die vorhandenen Daten hinzufügen. Anfügen von Daten werden an ein Feld, und klicken Sie dann festlegen oder Lesen Sie den Wert eines anderen Felds im aktuellen Datensatz, geht davon aus ADO, dass Sie die Daten an das erste Feld anfügen abgeschlossen haben. Beim Aufrufen der **AppendChunk** Methode auf das erste Feld erneut ADO interpretiert den Aufruf als ein neues **AppendChunk** Vorgang und die vorhandenen Daten überschrieben. Zugriff auf Felder in anderen **Recordset** Objekte, die nicht der ersten Klone sind **Recordset** Objekt wird nicht unterbrochen. **AppendChunk** Vorgänge.  
  
 Verwenden der **GetChunk** Methode auf eine **Feld** Teil oder alle zugehörigen Daten lange Binär- oder Zeichendatentypen abzurufenden Objekts. In Situationen, in dem Systemspeicher beschränkt ist, können Sie die **GetChunk** Methode, um lange Werte in Teilen und nicht in ihrer Gesamtheit zu bearbeiten.  
  
 Die Daten, die eine **GetChunk** Aufruf gibt zugewiesen *Variable*. Wenn *Größe* ist größer als die übrigen Daten der **GetChunk** Methodenrückgabe nur die verbleibenden Daten ohne Auffüllung *Variable* mit Leerzeichen. Wenn das Feld leer ist, ist die **GetChunk** Methode gibt einen null-Wert zurück.  
  
 Jeder nachfolgende **GetChunk** Aufruf ruft Daten ab, aus denen der vorherigen **GetChunk** Aufruf unterbrochen wurde. Abrufen von Daten werden von einem Feld, und klicken Sie dann festlegen oder lesen den Wert eines anderen Felds im aktuellen Datensatz nimmt ADO jedoch, dass Sie das Abrufen von Daten aus dem ersten Feld abgeschlossen haben. Beim Aufrufen der **GetChunk** Methode auf das erste Feld erneut ADO interpretiert den Aufruf als ein neues **GetChunk** Vorgang und beginnt mit der vom Anfang der Daten zu lesen. Zugriff auf Felder in anderen **Recordset** Objekte, die nicht der ersten Klone sind **Recordset** Objekt wird nicht unterbrochen. **GetChunk** Vorgänge.  
  
 Wenn die **AdFldLong** bit in der **Attribute** Eigenschaft eine **Feld** -Objekts festgelegt wird, um **"true"**, können Sie die **GetChunk**  Methode für dieses Feld.  
  
 Wenn kein aktueller Datensatz vorhanden ist, bei der Verwendung der **GetChunk** oder **AppendChunk** Methode auf eine **Feld** -Objekt Fehler 3021 (kein aktueller Datensatz) auftritt.  
  
 Ein Beispiel der Verwendung dieser Methoden zum Bearbeiten von Binärdaten, finden Sie die [AppendChunk Methode](../../../ado/reference/ado-api/appendchunk-method-ado.md) und [GetChunk-Methode](../../../ado/reference/ado-api/getchunk-method-ado.md) Beispielen in der *ADO Programmer's Reference*.
