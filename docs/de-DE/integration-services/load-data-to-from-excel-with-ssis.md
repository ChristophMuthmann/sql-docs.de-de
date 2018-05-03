---
title: Laden von Daten aus oder in Excel mit SSIS | Microsoft-Dokumentation
ms.description: Describes how to import data from Excel or export data to Excel with SQL Server Integration Services (SSIS). Also describes prerequisites, known issues, and limitations.
ms.date: 04/10/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 00e3c7b22555404654a381911a7812af666a03cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="load-data-from-or-to-excel-with-sql-server-integration-services-ssis"></a>Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS)

Dieser Artikel beschreibt, wie mit SQL Server Integration Services (SSIS) Daten aus Excel importiert oder in Excel exportiert werden können. Außerdem werden Voraussetzungen, Einschränkungen und bekannte Probleme erläutert.

Sie können Daten aus Excel importieren oder in Excel exportieren, indem Sie ein SSIS-Paket erstellen und den Excel-Verbindungs-Manager und die Excel-Quelle oder das Excel-Ziel verwenden. Sie können auch den SQL Server-Import/ Export-Assistenten in SSIS verwenden.

Dieser Artikel enthält Informationen, die Sie benötigen, um Excel erfolgreich über SSIS zu verwenden oder um häufige Probleme nachzuvollziehen und zu behandeln:
-   [Die erforderlichen Dateien:](#files-you-need)
-   Diese Informationen müssen Sie bereitstellen, wenn Sie Daten in oder aus Excel laden.
    -   Geben Sie [Excel](#specify-excel) als Datenquelle an.
    -   Geben Sie den [Namen und den Pfad der Excel-Datei](#excel-file) an.
    -   Wählen Sie die [Excel-Version](#excel-version) aus.
    -   Geben Sie an, ob [die erste Zeile Spaltennamen enthält](#first-row).
    -   Stellen Sie das [Arbeitsblatt oder den Bereich mit den Daten](#sheets-ranges) an.
-   Einschränkungen und bekannte Probleme:
    -   Probleme mit [Datentypen](#issues-types)
    -   Probleme beim [Import](#issues-importing)
    -   Probleme beim [Export](#issues-exporting)

## <a name="files-you-need"></a> Herunterladen von Dateien zum Herstellen einer Verbindung mit Excel

Bevor Sie Daten aus Excel importieren oder in Excel exportieren können, müssen Sie möglicherweise die Konnektivitätskomponenten für Excel herunterladen, sofern diese nicht bereits installiert sind. Die Konnektivitätskomponenten für Excel sind nicht standardmäßig installiert.

Die neueste Version der Konnektivitätskomponenten für Excel stehen unter [Microsoft Access Database Engine 2016 Redistributable (Microsoft Access Database Engine 2016 – Weitervertreibbare Komponente)](https://www.microsoft.com/download/details.aspx?id=54920) zum Download bereit.
  
Die aktuelle Version der Komponenten dient zum Öffnen von Dateien, die in früheren Versionen von Excel erstellt wurden.

Stellen Sie sicher, dass Sie die *weitervertreibbare Komponente* von Access Database Engine 2016 und nicht Microsoft Access 2016 *Runtime* herunterladen.

Wenn der Computer bereits über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Versionen der Komponenten installieren. Sie müssen auch sicherstellen, dass das SSIS-Paket im 32-Bit-Modus ausgeführt wird, oder führen Sie die 32-Bit-Version des Import/Export-Assistenten aus.

Wenn Sie über ein Office 365-Abonnement verfügen, wird möglicherweise eine Fehlermeldung angezeigt, wenn Sie das Installationsprogramm ausführen. Dieser Fehler gibt an, dass Sie den Download nicht parallel mit Klick-und-Los-Komponenten von Office installieren können. Führen Sie die Installation zur Umgehung dieser Fehlermeldung im stillen Modus durch, indem Sie ein Eingabeaufforderungsfenster öffnen und die EXE-Datei, die Sie heruntergeladen haben, mit der Befehlszeilenoption `/quiet` ausführen. Zum Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

Wenn Sie Probleme beim Installieren der weitervertreibbaren Komponente 2016 haben, installieren Sie die weitervertreibbare Komponente 2010: [Microsoft Access Database Engine 2010 Redistributable (Microsoft Access Database Engine 2010 – Weitervertreibbare Komponente)](https://www.microsoft.com/download/details.aspx?id=13255). (Es gibt keine weitervertreibbare Komponente für Excel 2013.)

## <a name="specify-excel"></a> Erste Schritte

Der erste Schritt ist die Angabe, dass Sie eine Verbindung mit Excel herstellen möchten.

### <a name="in-ssis"></a>In SSIS
Erstellen Sie in SSIS einen Excel-Verbindungs-Manager zur Verbindung mit der Excel-Quelldatei oder der Excel-Zieldatei. Es gibt verschiedene Möglichkeiten, diesen Verbindungs-Manager zu erstellen:

-   Klicken Sie mit der rechten Maustaste in den Bereich **Verbindungs-Manager**, und wählen Sie dann **Neue Verbindung** aus. Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** **EXCEL** und dann **Hinzufügen** aus.
 
-   Wählen Sie im Menü **SSIS** den Befehl **Neue Verbindung** aus. Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** **EXCEL** und dann **Hinzufügen** aus.

-   Erstellen Sie den Verbindungs-Manager zur gleichen Zeit wie die Konfiguration der **Excel-Quelle** oder des **Excel-Ziels** auf der Seite **Verbindungs-Manager** des **Quellen-Editors für Excel** oder des **Ziel-Editors für Excel**.

### <a name="in-the-sql-server-import-and-export-wizard"></a>Im Assistent für SQL Server-Import/Export
Wählen Sie im Import/Export-Assistenten auf den Seiten **Eine Datenquelle auswählen** oder **Ein Ziel auswählen** **Microsoft Excel** in der Liste **Datenquelle**.

Wenn Excel nicht in der Liste der Datenquellen angezeigt wird, sollten Sie überprüfen, ob Sie die 32-Bit-Version des Assistenten verwenden. Die Excel-Konnektivitätskomponenten sind in der Regel 32-Bit-Dateien und sind im 64-Bit-Assistenten nicht sichtbar.

## <a name="excel-file"></a> Excel-Datei und -Dateipfad

Zuerst geben Sie den Pfad und Dateinamen für die Excel-Datei an. Sie geben diese Informationen im **Excel-Verbindungs-Manager-Editor** in einem SSIS-Paket oder auf den Seiten **Eine Datenquelle auswählen** oder **Ein Ziel auswählen** des Import/Export-Assistenten an.

Geben Sie den Pfad und den Dateinamen in folgendem Format ein:

-   Für eine Datei auf dem lokalen Computer können Sie beispielsweise **C:\\TestData.xlsx** festlegen.

-   Für eine Datei auf einer Netzwerkfreigabe können Sie beispielsweise **\\\\Sales\\Data\\TestData.xlsx** festlegen.

Oder klicken Sie auf **Durchsuchen**, um die Kalkulationstabelle mithilfe des Dialogfelds **Öffnen** zu finden.  
  
> [!IMPORTANT]
> Es ist nicht möglich, eine Verbindung mit einer kennwortgeschützten Excel-Datei herzustellen.

## <a name="excel-version"></a> Excel-Version

Dann geben Sie die Version der Excel-Datei an. Sie geben diese Informationen im **Excel-Verbindungs-Manager-Editor** in einem SSIS-Paket oder auf den Seiten **Eine Datenquelle auswählen** oder **Ein Ziel auswählen** des Import/Export-Assistenten an.

Wählen Sie die Version von Microsoft Excel aus, die zum Erstellen der Datei verwendet wurde, oder entscheiden Sie sich für eine andere kompatible Version. Wenn Sie beispielsweise Probleme beim Installieren der Konnektivitätskomponenten 2016 hatten, können Sie die 2010-Komponenten installieren und **Microsoft Excel 2007-2010** in dieser Liste auswählen.

Sie können möglicherweise keine neuere Versionen von Excel in der Liste auswählen, wenn Sie nur ältere Versionen der Konnektivitätskomponenten installiert haben. Die Liste **Excel-Version** enthält alle von SSIS unterstützten Excel-Versionen. Das Vorhandensein von Elementen in dieser Liste, gibt nicht an, dass die erforderlichen Verbindungskomponenten installiert sind. So erscheint beispielsweise **Microsoft Excel 2016** in der Liste, auch wenn Sie die Konnektivitätskomponenten 2016 nicht installiert haben.

## <a name="first-row"></a> Erste Zeile enthält Spaltennamen

Wenn Sie Daten aus Excel importieren, müssen Sie als nächstes angeben, ob die erste Zeile der Daten Spaltennamen enthält. Sie geben diese Informationen im **Excel-Verbindungs-Manager-Editor** in einem SSIS-Paket oder auf der Seite **Eine Datenquelle auswählen** des Import/Export-Assistenten an.

-   Wenn Sie diese Option deaktivieren, da die Quelldaten keine Spaltennamen aufweisen, verwendet der Assistent F1, F2 usw. als Spaltenüberschriften.
-   Wenn die Daten Spaltennamen enthalten, Sie diese Option jedoch deaktivieren, importiert der Assistent die Spaltennamen als erste Datenzeile.
-   Wenn die Daten keine Spaltennamen enthalten, Sie diese Option jedoch aktivieren, verwendet der Assistent die erste Zeile der Quelldaten als Spaltennamen. In diesem Fall ist die erste Zeile der Quelldaten nicht länger in den Daten selbst enthalten.

Wenn Sie Daten aus Excel exportieren und diese Option aktivieren, enthält die erste Zeile der exportierten Daten die Spaltennamen.

## <a name="sheets-ranges"></a> Arbeitsblätter und Bereiche

Es gibt drei Arten von Excel-Objekten, die Sie als Quelle oder Ziel für Ihre Daten verwenden können: ein Arbeitsblatt, einen benannten Bereich oder einen unbenannten Zellbereich, den Sie mit der Adresse angeben.

-   **Arbeitsblatt:** Fügen Sie das `$`-Zeichen an das Ende des Blattnamens an, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B. **[Sheet1$]**, um ein Arbeitsblatt anzugeben. Oder suchen Sie in der Liste der vorhandenen Tabellen und Ansichten nach einem Namen, der mit dem `$`-Zeichen endet.

-   **Benannter Bereich:** Stellen Sie den Namen des Bereichs bereit, z.B. **MyDataRange**, um einen benannten Bereich anzugeben. Oder suchen Sie in der Liste der vorhandenen Tabellen und Ansichten nach einem Namen, der nicht mit dem `$`-Zeichen endet.
    
-   **Unbenannter Bereich:** Um einen Bereich von Zellen anzugeben, den Sie nicht benannt haben, fügen Sie das $-Zeichen an das Ende des Blattnamens an, fügen Sie die Bereichsspezifikation hinzu, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B: **[Sheet1$A1:B4]**.

Führen Sie einen der folgenden Schritte aus, um den Typ des Excel-Objekts auszuwählen oder anzugeben, das Sie als Quelle oder Ziel für Ihre Daten verwenden möchten:

### <a name="in-ssis"></a>In SSIS

Führen Sie in SSIS auf der Seite **Verbindungs-Manager** des **Quellen-Editors für Excel** oder **Ziel-Editors für Excel** einen der folgenden Schritte aus:

-   Wählen Sie die Option **Tabelle oder Ansicht** als **Datenzugriffsmodus** aus, um ein **Arbeitsblatt** oder einen **Benannten Bereich** zu verwenden. Wählen Sie in der Liste **Name der Excel-Tabelle** das Arbeitsblatt oder den benannten Bereich aus.

-   Wählen Sie **SQL-Befehl** als **Datenzugriffsmodus** aus, um einen **Unbenannten Bereich** zu verwenden, den Sie mit seiner Adresse angeben. Geben Sie dann im Feld **SQL-Befehlstext** eine Abfrage wie im folgenden Beispiel an:

    ```sql
    SELECT * FROM [Sheet1$A1:B5]
    ```

### <a name="in-the-sql-server-import-and-export-wizard"></a>Im Assistent für SQL Server-Import/Export
Führen Sie im Import/Export-Assistenten einen der folgenden Schritte aus:

-   Wenn Sie aus Excel **Importieren**, dann führen Sie einen der folgenden Schritte aus:

    -   Wählen Sie auf der Seite **Tabellenkopie oder Abfrage angeben** **Daten aus mindestens einer Tabelle oder Ansicht kopieren** aus, um ein **Arbeitsblatt** oder einen **Benannten Bereich** zu verwenden. Wählen Sie dann auf der Seite **Quelltabellen und -ansichten auswählen** in der Spalte **Quelle** die Arbeitsblätter und benannten Bereiche der Quelle aus.

    -   Zur Verwendung eines **Unbenannten Bereichs**, den Sie mit der Adresse angeben, wählen Sie auf der Seite **Tabellenkopie oder Abfrage angeben** **Abfrage zum Angeben der zu übertragenden Daten schreiben** aus. Geben Sie dann auf der Seite **Quellabfrage angeben** eine Abfrage wie im folgenden Beispiel an:

        ```sql
        SELECT * FROM [Sheet1$A1:B5]
        ```

-   Wenn Sie zu Excel **Exportieren**, dann führen Sie einen der folgenden Schritte aus:

    -   Wählen Sie auf der Seite **Quelltabellen und -ansichten auswählen** in der Spalte **Ziel** die Zielarbeitsblätter und benannten Bereiche aus, um ein **Arbeitsblatt** oder einen **Benannten Bereich** zu verwenden.

    -   Geben Sie auf der Seite **Quelltabellen und -ansichten auswählen** in der Spalte **Ziel** den Bereich ohne Trennzeichen im folgenden Format an:`Sheet1$A1:B5`, um einen **Unbenannten Bereich** zu verwenden, den Sie mit der Adresse angeben. Der Assistent fügt die Trennzeichen hinzu.

Sobald Sie die zu importierenden oder exportierenden Excel-Objekte ausgewählt oder eingegeben haben, können Sie auch die folgenden Schritte auf der Seite **Quelltabellen und -ansichten auswählen** des Assistenten ausführen:

-   Überprüfen Sie die Spaltenzuordnungen zwischen Quelle und Ziel, indem Sie **Zuordnungen bearbeiten** auswählen.

-   Zeigen Sie eine Vorschau der Beispieldaten an, um sicherzustellen, dass diese Ihren Erwartungen entsprechen, indem Sie **Vorschau** auswählen.

## <a name="issues-types"></a>Probleme mit Datentypen

### <a name="data-types"></a>Datentypen

Der Excel-Treiber erkennt nur einen begrenzten Satz von Datentypen. Beispielsweise werden alle numerischen Spalten als Werte mit doppelter Genauigkeit (DT_R8) interpretiert, und alle Zeichenfolgenspalten (außer Memospalten) werden als Unicode-Zeichenfolgen mit 255 Zeichen (DT_WSTR) interpretiert. SSIS ordnet die Excel-Datentypen folgendermaßen zu:

-   Numerisch – Gleitkommawert mit doppelter Genauigkeit (DT_R8)

-   Währung – Währung (DT_CY)

-   Boolesch – Boolesch (DT_BOOL)

-   Datum/Uhrzeit – DateTime (DT_DATE)

-   Zeichenfolge – Unicode-Zeichenfolge, Länge 255 (DT_WSTR)

-   Memo – Unicode-Textdatenstrom (DT_NTEXT)

### <a name="data-type-and-length-conversions"></a>Datentyp- und Längenkonvertierungen

SSIS konvertiert Datentypen nicht implizit. Daher müssen Sie u.U. die Transformationen für abgeleitete Spalten oder für die Datenkonvertierung verwenden, um Excel-Daten vor dem Laden in ein Nicht-Excel-Ziel explizit zu konvertieren bzw. um Nicht-Excel-Daten vor dem Laden in ein Excel-Ziel zu konvertieren.

Im Folgenden finden Sie einige Beispiele für ggf. erforderliche Konvertierungen:  
  
-   Konvertierung zwischen Unicode-Excel-Zeichenfolgenspalten und Nicht-Unicode-Zeichenfolgenspalten mit bestimmten Codepages.
  
-   Konvertierung zwischen Excel-Zeichenfolgenspalten mit 255 Zeichen und Zeichenfolgenspalten anderer Längen.
  
-   Konvertierung zwischen numerischen Excel-Spalten mit doppelter Genauigkeit und numerischen Spalten anderer Typen.

> [!TIP]
> Wenn Sie den Import/Export-Assistenten verwenden, und Ihre Daten einige dieser Konvertierungen erfordern, konfiguriert der Assistent die erforderlichen Konvertierungen für Sie. Auch wenn Sie ein SSIS-Paket verwenden möchten, kann es deshalb sinnvoll sein, das ursprüngliche Paket mithilfe des Import/Export-Assistenten zu erstellen. Lassen Sie den Assistenten Verbindungs-Manager, Quellen, Transformationen und Ziele für Sie erstellen und konfigurieren.

## <a name="issues-importing"></a> Probleme beim Import

### <a name="empty-rows"></a>Leere Zeilen

Wenn Sie ein Arbeitsblatt oder einen benannten Bereich als Quelle angeben, liest der Treiber den *zusammenhängenden* Zellenblock ab der ersten nicht leeren Zelle in der linken oberen Ecke des Arbeitsblatts oder Bereichs. Daher müssen Ihre Daten nicht in Zeile 1 beginnen, es dürfen jedoch keine leere Zeilen in den Quelldaten vorhanden sein. So ist beispielsweise keine leere Zeile zwischen den Spaltenüberschriften und den Datenzeilen oder ein Titel gefolgt von leeren Zeilen am Anfang des Arbeitsblatts möglich.

Wenn sich leere Zeilen über Ihren Daten befinden, können Sie die Daten nicht als Arbeitsblatt abfragen. In Excel müssen Sie Ihren Datenbereich auswählen, ihm einen Namen zuweisen, und den benannten Bereich statt des Arbeitsblatts abfragen.

### <a name="missing-values"></a>Fehlende Werte

Der Excel-Treiber liest eine bestimmte Anzahl von Zeilen (standardmäßig acht Zeilen) in der angegebenen Quelle, um den Datentyp jeder Spalte zu ermitteln. Wenn eine Spalte offensichtlich gemischte Datentypen enthält, insbesondere eine Mischung aus numerischen Daten und Textdaten, entscheidet der Treiber zugunsten des Mehrheitsdatentyps und gibt in Zellen mit Daten des anderen Datentyps NULL-Werte zurück. (In einer unentschiedenen Situation hat der numerische Datentyp Vorrang.) Die meisten Zellenformatierungsoptionen im Excel-Arbeitsblatt scheinen keinen Einfluss auf diese Datentypfestlegung zu haben.

Sie können dieses Verhalten des Excel-Treibers ändern, indem Sie den Importmodus angeben, um alle Werte als Text zu importieren. Um den Importmodus anzugeben, fügen Sie `IMEX=1` dem Wert für **Erweitere Eigenschaften** in der Verbindungszeichenfolge des Excel-Verbindungs-Managers im Eigenschaftenfenster hinzu. 

### <a name="truncated-text"></a>Abgeschnittener Text

Wenn der Anbieter bestimmt, dass eine Excel-Spalte Textdaten enthält, wählt der Treiber den Datentyp (string- oder memo-Datentyp) auf Basis des längsten Werts, der als Stichprobe genommenen wird. Wenn der Treiber in den als Stichprobe genommenen Zeilen keine Werte mit mehr als 255 Zeichen findet, wird die Spalte nicht als Memospalte, sondern als Zeichenfolgenspalte mit 255 Zeichen behandelt. Deshalb können Werte, die länger als 255 Zeichen sind, abgeschnitten werden.

Zum Importieren von Daten aus einer Memospalte ohne eine Kürzung haben Sie zwei Optionen:

-   Stellen Sie sicher, dass die Memospalte in mindestens einer der als Stichprobe genommenen Zeilen einen Wert mit mehr als 255 Zeichen enthält

-   Erhöhen Sie die Anzahl der als Stichprobe verwendeten Zeilen mit dem Treiber, um eine solche Zeile einzuschließen. Sie können die als Stichprobe genommene Zeilenanzahl mithilfe des Werts **TypeGuessRows** unter dem folgenden Registrierungsschlüssel erhöhen:

| Weitervertreibbare Komponentenversion | Registrierungsschlüssel |
|---|---|
| Excel 2016 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel |
| Excel 2010 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel |
| | |

## <a name="issues-exporting"></a> Probleme beim Export

### <a name="create-a-new-destination-file"></a>Erstellen einer neuen Zieldatei

#### <a name="in-ssis"></a>In SSIS

Erstellen Sie einen Excel-Verbindungs-Manager mit dem Pfad und Dateinamen der neuen Excel-Datei, die Sie erstellen möchten. Wählen Sie dann im **Ziel-Editor für Excel** für **Name der Excel-Tabelle** die Option **Neu** aus, um die Zieltabelle zu erstellen. An diesem Punkt erstellt SSIS die neue Excel-Datei mit dem angegebenen Arbeitsblatt.

#### <a name="in-the-sql-server-import-and-export-wizard"></a>Im Assistent für SQL Server-Import/Export

Wählen Sie auf der Seite **Ein Ziel auswählen** **Durchsuchen** aus. Navigieren Sie im Dialogfeld **Öffnen** zum Ordner, in dem die neue Excel-Datei erstellt werden soll, geben Sie einen Namen für die neue Datei an, und wählen Sie dann **Öffnen** aus.

### <a name="export-to-a-large-enough-range"></a>Exportieren in einen Bereich, der groß genug ist

Wenn Sie einen Bereich als Ziel angeben, wird ein Fehler zurückgegeben, sofern dieser Bereich weniger *Spalten* als die Quelldaten enthält. Wenn der Bereich, den Sie angeben, jedoch weniger *Zeilen* als die Quelldaten aufweist, schreibt der Assistent weiterhin Zeilen ohne Fehler und erweitert die Bereichsdefinition, sodass sie mit der neuen Zeilenanzahl übereinstimmt.

### <a name="export-long-text-values"></a>Exportieren von langen Textwerten

Zum erfolgreichen Speichern von Zeichenfolgen mit mehr als 255 Zeichen in einer Excel-Spalte muss der Treiber den Datentyp der Zielspalte als **memo** und nicht als **string**erkennen.

-   Wenn die vorhandene Zieltabelle bereits Datenzeilen enthält, müssen die ersten Zeilen, die vom Treiber als Stichprobe genommen werden, mindestens eine Instanz eines Werts mit mehr als 255 Zeichen in der Memospalte enthalten.

-   Wenn die neue Zieltabelle während des Paketentwurfs oder zur Laufzeit oder vom Import/Exportassistenten erstellt wird, muss die `CREATE TABLE`-Anweisung als Datentyp für die Zielmemospalte LONGTEXT (oder eines der Synonyme) verwenden. Überprüfen Sie im Assistent die `CREATE TABLE`-Anweisung, und bearbeiten Sie diese bei Bedarf, indem Sie auf der Seite **Spaltenzuordnungen** neben der Option **Zieltabelle erstellen** auf **SQL bearbeiten** klicken.

## <a name="related-content"></a>Verwandte Inhalte

Weitere Informationen zu den Komponenten und den in diesem Artikel beschriebenen Verfahren finden Sie in den folgenden Artikeln:

### <a name="about-ssis"></a>Über SSIS
[Excel-Verbindungs-Manager](connection-manager/excel-connection-manager.md)  
[Excel-Quelle](data-flow/excel-source.md)  
[Excel-Ziel](data-flow/excel-destination.md)  
[Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
[Arbeiten mit Excel-Dateien mit dem Skripttask](extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)

### <a name="about-the-sql-server-import-and-export-wizard"></a>Über Assistent für SQL Server-Import/Export
[Herstellen einer Verbindung mit einer Excel-Datenquelle](import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)  
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

### <a name="other-articles"></a>Andere Artikel
[Importieren von Daten aus Excel in SQL Server oder Azure SQL-Datenbank](../relational-databases/import-export/import-data-from-excel-to-sql.md)  
