---
title: Arbeiten mit Recordsets | Microsoft Docs
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
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b83fb8d5ad4e2e063ca840b7e8fb31bbf15fde14
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-recordsets"></a>Arbeiten mit Recordsets
Die **Recordset** Objekt verfügt über integrierte Funktionen, mit denen Sie die Reihenfolge der Daten in das Resultset für die Suche nach einem bestimmten Datensatz basierend auf Kriterien, die Sie bereitstellen und sogar diese Suchvorgänge mithilfe von Indizes optimieren ändern können. Gibt an, ob diese Funktionen zur Verfügung stehen, hängt von den Anbieter sowie in einigen Fällen –, beispielsweise von der [Index](../../../ado/reference/ado-api/index-property.md) Eigenschaft – die Struktur der Datenquelle selbst.  
  
## <a name="arranging-data"></a>Anordnen von Daten  
 In vielen Fällen die effizienteste Methode zum Sortieren der Daten in Ihrem **Recordset** ist, indem Sie eine ORDER BY-Klausel in der SQL-Befehl verwendet, um die Ergebnisse zurückgeben. Allerdings möglicherweise so ändern Sie die Reihenfolge der Daten in einem **Recordset** , die bereits erstellt wurde. Können Sie die **sortieren** Eigenschaft, um die Reihenfolge festlegen, welche Zeilen der einen **Recordset** durchlaufen werden. Darüber hinaus die **Filter** Eigenschaft bestimmt, welche Zeilen kann zugegriffen werden, wenn Zeilen zu durchlaufen.  
  
 Die **sortieren** Eigenschaft legt fest oder gibt einen **Zeichenfolge** Wert an das Feld den Namen der **Recordset** für die Sortierung. Jeder Name wird durch ein Komma getrennt und ist optional gefolgt von einem Leerzeichen und das Schlüsselwort **ASC** (die sortiert des Felds in aufsteigender Reihenfolge) oder **"DESC"** (die sortiert des Felds in absteigender Reihenfolge). In der Standardeinstellung Wenn kein Schlüsselwort angegeben ist, wird das Feld in aufsteigender Reihenfolge sortiert.  
  
 Der Sortiervorgang ist effizient, da Daten nicht physisch neu angeordnet, aber in der Reihenfolge angegeben, die durch einen Index zugegriffen werden.  
  
 Die **sortieren** Eigenschaft ist erforderlich, die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft festgelegt werden, um **AdUseClient**. Ein temporärer Index wird für jedes Feld im angegebenen erstellt die **sortieren** Eigenschaft, wenn ein Index nicht bereits vorhanden ist.  
  
 Festlegen der **sortieren** Eigenschaft auf eine leere Zeichenfolge wird die Zeilen in der ursprünglichen Reihenfolge zurückgesetzt und temporäre Indizes zu löschen. Vorhandene Indizes werden nicht gelöscht werden.  
  
 Nehmen Sie an einer **Recordset** enthält drei Felder mit dem Namen *FirstName*, *MiddleInitial*, und *LastName*. Legen Sie die **sortieren** -Eigenschaft die Zeichenfolge "`lastName DESC, firstName ASC`", die Reihenfolge der **Recordset** nach dem Nachnamen in absteigender Reihenfolge und dann nach Vornamen in aufsteigender Reihenfolge. Der Wert von MiddleInitial wird ignoriert.  
  
 Kein Feld in einer Sortierreihenfolge Kriterien-Zeichenfolge verwiesen werden, kann benannte "ASC" oder "DESC", da diese Namen in mit den Schlüsselwörtern Konflikt **ASC** und **"DESC"**. Geben Sie ein Feld mit einem in Konflikt stehenden Namen einen Alias mithilfe die **AS** Schlüsselwort in der Abfrage, die zurückgibt der **Recordset**.  
  
 Weitere Informationen zu **Recordset** filtern, finden Sie unter "Filtern der Ergebnisse" weiter unten in diesem Thema.  
  
## <a name="finding-a-specific-record"></a>Suchen eines bestimmten Datensatzes  
 ADO bietet die [suchen](../../../ado/reference/ado-api/find-method-ado.md) und [Seek](../../../ado/reference/ado-api/seek-method.md) Methoden für die Suche nach einem bestimmten Datensatz in einem **Recordset**. Die **suchen** Methode wird von einer Vielzahl von Anbietern unterstützt, sondern auf ein einzelnes Suchkriterium beschränkt ist. Die **Seek** Methode unterstützt die Suche nach mehreren Kriterien, aber wird nicht von vielen Anbietern unterstützt.  
  
 Indizes für Felder können die Leistung erheblich verbessern die **suchen** Methode und **sortieren** und **Filter** Eigenschaften der **Recordset** -Objekt. Sie können einen internen Index erstellen eine **Feld** Objekt durch Festlegen seiner dynamischen [optimieren](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) Eigenschaft. Diese dynamische Eigenschaft hinzugefügt wird die **Eigenschaften** Auflistung von der **Feld** Objekt, wenn Sie festlegen, die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**. Denken Sie daran, dass dieser Index für ADO intern ist – Sie können nicht auf ihn zugreifen oder für andere Zwecke verwenden. Außerdem dieser Index eignet sich von der [Index](../../../ado/reference/ado-api/index-property.md) Eigenschaft von der **Recordset** Objekt.  
  
 Die **suchen** Methode ermittelt schnell einen Wert innerhalb einer Spalte (Feld) ein **Recordset**. Sie können häufig verbessern die Geschwindigkeit des der **suchen** Methode für eine Spalte mit der **optimieren** Eigenschaft zum Erstellen eines Indexes.  
  
 Die **suchen** -Methode schränkt die Suche auf den Inhalt des Felds ein. Die **Seek** Methode erfordert, dass Sie weitere Einschränkungen sowie noch und einen Index haben. Wenn müssen Sie auf mehrere Felder, die nicht die Basis eines Indexes suchen, oder wenn Ihr Anbieter Indizes nicht unterstützt, können Sie Ihre Ergebnisse einschränken, indem Sie mit der **Filter** Eigenschaft von der **Recordset** Objekt.  
  
### <a name="find"></a>Suchen  
 Die **suchen** Methode sucht eine **Recordset** für die Zeile, die ein angegebenes Kriterium erfüllt. Optional kann die Richtung der Suche, Startzeile und Offset von der Startzeile angegeben werden. Wenn das Kriterium erfüllt ist, wird die aktuelle Zeilenposition bei dem gefundenen Datensatz festgelegt. hingegen wird die Position festgelegt, zum Ende (oder Start) von der **Recordset**suchrichtung abhängig.  
  
 Für das Kriterium kann nur ein einzelner Spaltennamen angegeben werden. Das heißt, unterstützt diese Methode nicht für mehrere Spalten sucht.  
  
 Der Vergleichsoperator für das Kriterium kann"**>**"(größer als),"**\<**" (kleiner als), "=" (gleich), "> =" (größer als oder gleich), "< =" (kleiner oder gleich), " <> "(nicht gleich), oder"LIKE"(Mustervergleich).  
  
 Das kriteriumwert kann es sich um eine Zeichenfolge, eine Gleitkommazahl oder ein Datum sein. Zeichenfolgenwerte werden in einfache Anführungszeichen oder "#" (Nummernzeichen) gesetzt (z. B. "State ="WA"" oder "Status = #WA #"). Datumswerte in ein "#" (Nummernzeichen) als Trennzeichen (z. B. "Start_date > #7/22/97 #").  
  
 Wenn der Vergleichsoperator "wie" ist, darf der Zeichenfolgenwert ein Sternchen (*), um ein oder mehr Vorkommen eines beliebigen Zeichens oder einer Teilzeichenfolge gefunden. Z. B. "Zustand wie bin\*" "Maine und Massachusetts. Führende und nachfolgende Sternchen können auch eine Teilzeichenfolge finden, die die Werte enthalten ist. Z. B. "State wie"\*als\*"" Alaska, Arkansas und Massachusetts übereinstimmt.  
  
 Sternchen können nur am Ende einer Zeichenfolge der Suchkriterien oder zusammen am Anfang und Ende einer Kriterienzeichenfolge verwendet werden, wie oben beschrieben. Sie können nicht mithilfe des Sternchens als führenden Platzhalter ("* str') oder Platzhalter ('s eingebettet\*R"). Dies verursacht einen Fehler.  
  
### <a name="seek-and-index"></a>Suche und Index  
 Verwenden der **Seek** -Methode zusammen mit der **Index** Eigenschaft, wenn der zugrunde liegende Anbieter Indizes unterstützt die **Recordset** Objekt. Verwenden der [unterstützt](../../../ado/reference/ado-api/supports-method.md)**(AdSeek)** Methode, um zu bestimmen, ob der zugrunde liegende Anbieter unterstützt **Seek**, und die **Supports(adIndex)** Methode, um zu bestimmen, ob der Anbieter Indizes unterstützt. (Z. B. die [OLE DB-Anbieter für Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) unterstützt **Seek** und **Index**.)  
  
 Wenn **Seek** befindet sich nicht Suchen der gewünschten Zeile, kein Fehler auftritt, und für die Zeile am Ende der **Recordset**. Legen Sie die **Index** Eigenschaft auf den gewünschten Index vor dem Ausführen dieser Methode.  
  
 Diese Methode ist nur mit serverseitiger Cursor unterstützt. Seek nicht unterstützt, wenn die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaftswert, der die **Recordset** Objekt **AdUseClient**.  
  
 Diese Methode kann verwendet werden nur, wenn die **Recordset** Objekt geöffnet wurde, mit einer [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) Wert **AdCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtern der Ergebnisse  
 Die **suchen** -Methode schränkt die Suche auf den Inhalt des Felds ein. Die **Seek** Methode erfordert, dass Sie weitere Einschränkungen sowie noch und einen Index haben. Wenn Sie auf mehrere Felder, die nicht auf der Grundlage eines Indexes sind suchen oder müssen wenn Ihr Anbieter Indizes nicht unterstützt, können Sie Ihre Ergebnisse einschränken, indem Sie mit der **Filter** Eigenschaft von der **Recordset** Objekt.  
  
 Verwenden der **Filter** Eigenschaft, um selektiv herauszufiltern Datensätze in einem **Recordset** Objekt. Die gefilterten **Recordset** wird der aktuelle Cursor, der Möglichkeit, die Datensätze nicht erfüllen die **Filter** Kriterien sind nicht verfügbar in der **Recordset** bis der **Filter** wird entfernt. Weitere Eigenschaften, die Rückgabe von Werten basierend auf den aktuellen Cursor betroffen sind, z. B. **AbsolutePosition**, **AbsolutePage**, **RecordCount**, und  **"PageCount"**. Dies ist, da das Festlegen der **Filter** Eigenschaft auf einen bestimmten Wert wird den aktuellen Datensatz verschoben, auf den ersten Eintrag, der den neuen Wert entspricht.  
  
 Die **Filter** Eigenschaft akzeptiert einen variant-Argument. Dieser Wert gibt eine der drei Methoden für die Verwendung der **Filter** Eigenschaft: eine Kriterienzeichenfolge eine **FilterGroupEnum** -Konstante oder ein Array von Lesezeichen. Weitere Informationen finden Sie weiter unten in diesem Thema mit einem Zeichenfolgen-Kriterien filtern, Filtern mit einer Konstante und Filtern mit Lesezeichen.  
  
> [!NOTE]
>  Wenn Sie die Daten, die Sie auswählen möchten kennen, ist in der Regel effizienter, öffnen Sie eine **Recordset** mit einer SQL­Anweisung, die das Resultset auf, statt die standardremotedatenbank effektiv filtert die **Filter** Eigenschaft.  
  
 So entfernen Sie einen Filter aus einem **Recordset**, verwenden Sie die **AdFilterNone** konstant. Festlegen der **Filter** Eigenschaft, um eine leere Zeichenfolge ("") hat dieselbe Wirkung wie das Verwenden von der **AdFilterNone** konstant.  
  
### <a name="filtering-with-a-criteria-string"></a>Mit einem Zeichenfolgen-Kriterien filtern  
 Die Zeichenfolge der Suchkriterien besteht aus Klauseln in der Form *Feldname Operatorwert* (z. B. `"LastName = 'Smith'"`). Sie können zusammengesetzte Klauseln erstellen, indem Sie einzelne Klauseln mit verketten **AND** (z. B. `"LastName = 'Smith' AND FirstName = 'John'"`) und **oder** (z. B. `"LastName = 'Smith' OR LastName = 'Jones'"`). Verwenden Sie die folgenden Richtlinien für Kriterienzeichenfolgen an:  
  
-   *Feldname* muss ein gültigen Feldnamen aus der **Recordset**. Wenn das Feldname Leerzeichen enthält, müssen Sie den Namen in eckige Klammern einschließen.  
  
-   *Operator* muss eines der folgenden sein: **\<**, **>**, **\< =**, **>=** , **<>**, **=**, oder **wie**.  
  
-   *Wert* ist der Wert, mit denen Sie die Feldwerte vergleichen (z. B. `'Smith'`, `#8/24/95#`, `12.345`, oder `$50.00`). Verwenden Sie einfache Anführungszeichen (') mit Zeichenfolgen und Nummernzeichen (`#`) mit Datumsangaben. Für Zahlen können Sie das Dezimaltrennzeichen, Dollarzeichen sowie die wissenschaftliche Schreibweise. Wenn *Operator* ist **wie**, *Wert* können Platzhalterzeichen verwenden. Nur das Sternchen (\*) und Prozentzeichen (%) Platzhalter Zeichen sind zulässig und sie müssen das letzte Zeichen in der Zeichenfolge sein. *Wert* darf nicht null sein.  
  
    > [!NOTE]
    >  Einfache Anführungszeichen (') im Filter eingeschlossen *Wert*, verwenden Sie zwei einfache Anführungszeichen, um eine darzustellen. Z. B. zum Filtern nach *lautet*, muss die Zeichenfolge der Suchkriterien `"col1 = 'O''Malley'"`. Um einfache Anführungszeichen am Anfang und Ende der Filterwert einzuschließen, schließen Sie die Zeichenfolge in Nummernzeichen (#). Z. B. zum Filtern nach *"1"*, muss die Zeichenfolge der Suchkriterien `"col1 = #'1'#"`.  
  
 Es gibt keine Rangfolge zwischen **AND** und **oder**. Klauseln können in Klammern gruppiert werden. Sie können keine jedoch durch verknüpften Klauseln gruppieren ein **oder** und verknüpfen Sie anschließend die Gruppe mit einer anderen Klausel mit einer AND wie folgt.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 Stattdessen würden Sie wie folgt Filter erstellen.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 In einer **wie** -Klausel, können Sie am Anfang und Ende des Musters einen Platzhalter (z. B. `LastName Like '*mit*'`) oder nur am Ende des Musters (z. B. `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Mit einer Konstanten filtern  
 Die folgenden Konstanten für das Filtern stehen **Recordsets**.  
  
|Konstante|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|Filter für die Anzeige von nur Datensätze, die von der letzten betroffenen **löschen**, **Resync**, **UpdateBatch**, oder **CancelBatch** aufrufen.|  
|**adFilterConflictingRecords**|Filter für die Anzeige der Datensätze, die die letzte Batchaktualisierung fehlgeschlagen ist.|  
|**adFilterFetchedRecords**|Filter für die Anzeige der Datensätze im aktuellen Cache – d. h. die Ergebnisse der dem letzten Aufruf von Datensätzen aus der Datenbank abzurufen.|  
|**adFilterNone**|Entfernt den aktuellen Filter und alle Datensätze für die Anzeige wiederhergestellt.|  
|**adFilterPendingRecords**|Filter für die Anzeige von Datensätzen, die geändert wurden, aber noch nicht an den Server gesendet wurden. Gilt nur für Batch-Updatemodus.|  
  
 Die Filter-Konstanten erleichtern das zum Auflösen einzelner Datensatz Konflikte während der Batch-Aktualisierungsmodus können Sie anzeigen, z. B. nur die Datensätze, die während des letzten betroffen **UpdateBatch** -Methodenaufruf, entsprechend der folgende.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Filtern mit Lesezeichen  
 Schließlich können Sie ein variant-Array von Lesezeichen, übergeben die **Filter** Eigenschaft. Der resultierende Cursor enthält nur die Datensätze, deren Lesezeichen in der Eigenschaft übergeben wurde. Das folgende Codebeispiel erstellt ein Array von Lesezeichen aus den Datensätzen in einer **Recordset** wofür eine "B" in der *ProductName* Feld. Es übergibt dann das Array, das die **Filter** Eigenschaft und zeigt Informationen über das resultierende gefilterte **Recordset**.  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>Erstellen eines Klons einer Datensatzgruppe  
 Verwenden der **Klon** Methode zum Erstellen mehrerer dupliziert **Recordset** Objekten, insbesondere, wenn Sie mehr als ein aktuellen Datensatz in einem angegebenen Satz von Datensätzen beibehalten möchten. Mithilfe der **Klon** Methode ist effizienter als das Erstellen und öffnen ein neues **Recordset** mit derselben Definition wie das ursprüngliche Objekt.  
  
 Der aktuelle Datensatz eines neu erstellten Klons ist ursprünglich auf den ersten Eintrag festgelegt. Der Zeiger des aktuellen Datensatzes in einer geklonten **Recordset** wird nicht synchronisiert werden, mit der ursprünglichen oder umgekehrt. Sie können unabhängig voneinander navigieren, in den einzelnen **Recordset**.  
  
 Änderungen an einer **Recordset** Objekt aller seiner Klone unabhängig von der Cursortyp sichtbar sind. Allerdings nach dem Ausführen [Requery](../../../ado/reference/ado-api/requery-method.md) am ursprünglichen **Recordset**, Klone werden nicht mehr mit dem ursprünglichen synchronisiert werden.  
  
 Schließen die ursprüngliche **Recordset** seine Datenbankkopien wird nicht geschlossen, ebenso wie nicht schließen schließen eine Kopie der ursprünglichen oder keines der anderen Kopien.  
  
 Klonvorgänge können eine **Recordset** Objekt nur, wenn sie Lesezeichen unterstützt. Lesezeichenwerte sind austauschbar. d. h. ein Lesezeichenverweis von einem **Recordset** Objekt bezieht sich auf den gleichen Datensatz in einer seiner Klone.
