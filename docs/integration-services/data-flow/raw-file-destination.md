---
title: Rohdatendatei-Ziel | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: d92f79e7a43f8d8368ec44b33aef7297749eb351
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="raw-file-destination"></a>Rohdatendatei-Ziel
  Das Rohdatendatei-Ziel schreibt Rohdaten in eine Datei. Die Daten liegen im systemeigenen Zielformat vor, sodass die Daten nicht übersetzt und kaum analysiert werden müssen. Dies bedeutet, dass das Rohdatendatei-Ziel Daten schneller als andere Ziele, wie z. B. Flatfile- und OLE DB-Ziele, schreiben kann.  
  
 Zusätzlich zur Option, Rohdatendateien in eine Datei schreiben zu können, können Sie auch das Rohdatendatei-Ziel verwenden, um eine leere Rohdatendatei zu generieren, die nur die Spalten (Nur-Metadatendatei) enthält, ohne dass das Paket ausgeführt werden muss. Mithilfe der Rohdatendatei-Quelle werden Rohdaten abgerufen, die zuvor vom Ziel geschrieben wurden. Sie können die Rohdatendatei-Quelle zudem auf die Nur-Metadaten-Datei verweisen.  
  
 Das Format der Rohdatendatei enthält Sortierungsinformationen: Das Rohdatendatei-Ziel speichert alle Sortierungsinformationen, einschließlich der Vergleichsflags für Zeichenfolgenspalten. Die Rohdatendatei-Quelle liest und beachtet die Sortierungsinformationen. Sie können die Rohdatendatei-Quelle dergestalt konfigurieren, dass die Sortierflags in der Datei mit dem erweiterten Editor ignoriert werden. Weitere Informationen zu Vergleichsflags finden Sie unter [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 Es gibt folgende Möglichkeiten, um das Rohdatendatei-Ziel zu konfigurieren:  
  
-   Geben Sie einen Zugriffsmodus an, wobei es sich entweder um den Namen der Datei oder eine Variable handelt, die den Namen der Datei enthält, in die das Rohdatendatei-Ziel schreibt.  
  
-   Geben Sie an, ob das Rohdatendatei-Ziel Daten an eine vorhandene gleichnamige Datei anfügt oder eine neue Datei erstellt.  
  
 Das Rohdatendatei-Ziel wird häufig zum Schreiben von Zwischenergebnissen teilweise verarbeiteter Daten zwischen Paketausführungen verwendet. Das Speichern von Rohdatendateien bedeutet, dass die Daten schnell von einer Rohdatendatei-Quelle gelesen und dann weiter transformiert werden können, bevor sie in das endgültige Ziel geladen werden. Beispielsweise kann ein Paket mehrmals ausgeführt werden, wobei jedes Mal Rohdaten in Dateien geschrieben werden. Später kann ein anderes Paket die Rohdatendatei-Quelle zum Lesen aus jeder Datei verwenden und mit einer Transformation für UNION ALL die Daten zu einem einzigen Dataset zusammenführen. Dann kann das Paket zusätzliche Transformationen anwenden, mit denen die Daten zusammengefasst werden, bevor sie in das endgültige Ziel, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle, geladen werden.  
  
> [!NOTE]  
>  Das Rohdatendatei-Ziel unterstützt NULL-Werte, aber keine BLOB-Daten (Binary Large Object).  
  
> [!NOTE]  
>  Für das Rohdatendatei-Ziel wird kein Verbindungs-Manager verwendet.  
  
 Diese Quelle hat nur eine reguläre Eingabe. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="append-and-new-file-options"></a>Optionen zum Anfügen und zum Erstellen einer neuen Datei  
 Die „WriteOption“-Eigenschaft schließt Optionen zum Anfügen von Daten an eine vorhandene Datei oder zum Erstellen einer neuen Datei ein.  
  
 In der folgenden Tabelle werden die verfügbaren Optionen für die „WriteOption“-Eigenschaft beschrieben.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Anfügen|Fügt Daten an eine vorhandene Datei an. Die Metadaten der angefügten Daten müssen mit dem Dateiformat übereinstimmen.|  
|Immer erstellen|Erstellt immer eine neue Datei.|  
|Einmal erstellen|Erstellt eine neue Datei. Wenn die Datei vorhanden ist, ist die Komponente fehlerhaft.|  
|Abschneiden und anfügen|Schneidet eine vorhandene Datei ab und schreibt dann die Daten in die Datei. Die Metadaten der angefügten Daten müssen mit dem Dateiformat übereinstimmen.|  
  
 Im Folgenden finden Sie wichtige Elemente über das Anfügen von Daten:  
  
-   Durch das Anfügen von Daten an eine vorhandene Rohdatendatei werden die Daten nicht erneut sortiert.  
  
     Sie müssen sicherstellen, dass die sortierten Schlüssel in der richtigen Reihenfolge bleiben.  
  
-   Durch das Anfügen von Daten an eine vorhandene Rohdatendatei werden die Dateimetadaten (Sortierungsinformationen) nicht geändert.  
  
 Beispielsweise liest ein Paket im ProductKey (PK) sortierte Daten. Der Paketdatenfluss fügt die Daten an eine vorhandene Rohdatendatei an. Bei der ersten Ausführung des Pakets werden drei Zeilen (PK 1000, 1100, 1200) empfangen. Die Rohdatendatei enthält nun die folgenden Daten.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 Bei der zweiten Ausführung des Pakets werden zwei neue Zeilen (PK 1001, 1300) empfangen. Die Rohdatendatei enthält nun die folgenden Daten.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 Die neuen Daten werden an das Ende der Rohdatendatei angefügt, und die sortierten Schlüssel (PK) werden nicht mehr verwendet. Zusätzlich werden die Dateimetadaten (Sortierungsinformationen) nicht durch den Anfügevorgang verändert. Wenn Sie die Datei mit der Rohdatendatei-Quelle lesen, gibt die Komponente an, dass die Datei immer noch nach PK sortiert ist, obwohl die Daten in der Datei nicht mehr in der richtigen Reihenfolge sind.  
  
 Um die sortierten Schlüssel in der richtigen Reihenfolge zu behalten, während Daten angefügt werden, können Sie den Paketdatenfluss wie folgt entwerfen:  
  
1.  Rufen Sie neue Zeilen mit Quelle A ab.  
  
2.  Rufen Sie vorhandene Zeilen mit Quelle B aus RawFile1 ab.  
  
3.  Kombinieren Sie die Eingaben von Quelle A und B mit der Transformation für UNION ALL.  
  
4.  Sortierung nach PK.  
  
5.  Schreiben Sie in RawFile2 mit dem Rohdatendatei-Ziel.  
  
     RawFile1 wird gesperrt, da im Datenfluss davon gelesen wird.  
  
6.  Ersetzen Sie RawFile1 durch RawFile2.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>Verwenden des Rohdatendatei-Ziels in einer Schleife  
 Wenn sich der Datenfluss, der das Rohdatendatei-Ziel verwendet, in einer Schleife befindet, wird die Datei möglicherweise einmal erstellt, und Daten werden an die Datei angefügt, wenn die Schleife wiederholt wird. Wenn die Daten an eine Datei angefügt werden, muss die anzufügende Datei mit dem Format der vorhandenen Datei übereinstimmen.  
  
 Um die Datei in der ersten Iteration einer Schleife zu erstellen, und dann die Zeilen in der nachfolgenden Iteration der Schleife anzufügen, müssen Sie Folgendes zur Entwurfszeit ausführen:  
  
1.  Legen Sie die „WriteOption“-Eigenschaft auf **CreateOnce** oder **CreateAlways**fest, und führen Sie dann eine Iteration der Schleife aus. Die Datei ist erstellt. Dadurch wird sichergestellt, dass die Metadaten der angefügten Daten mit der Datei übereinstimmen.  
  
2.  Setzen Sie die „WriteOption“-Eigenschaft auf **Append** zurück, und legen Sie die „ValidateExternalMetadata“-Eigenschaft auf **False**fest.  
  
 Wenn Sie die Option **TruncateAppend** statt der Option **Append** verwenden, werden die Zeilen abgeschnitten, die in einer vorherigen Iteration hinzugefügt wurden, und dann neue Zeilen angefügt. Das Verwenden der Option **TruncateAppend** erfordert auch, dass die Daten im Dateiformat übereinstimmen.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Konfiguration des Rohdatendatei-Ziels  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften der Rohdatendatei](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Informationen zum Festlegen der Eigenschaften der Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Blogeintrag, [Raw Files Are Awesome](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx), auf sqlservercentral.com  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>Ziel-Editor für Rohdatendateien (Seite Verbindungs-Manager)
  Verwenden Sie den Ziel-Editor für Rohdatendateien zum Konfigurieren des Rohdatendatei-Ziels, um Rohdaten in eine Datei zu schreiben.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Ziel-Editors für Rohdatendateien](#open)  
  
-   [Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"](#connection)  
  
-   [Festlegen von Optionen auf der Registerkarte "Spalten"](#mapping)  
  
###  <a name="open"></a> Öffnen des Ziel-Editors für Rohdatendateien  
  
1.  Fügen Sie das Rohdatendatei-Ziel in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einem [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Paket hinzu.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Komponente, und klicken Sie anschließend auf **Bearbeiten**.  
  
###  <a name="connection"></a> Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"  
 **Zugriffsmodus**  
 Wählen Sie aus, wie der Dateiname angegeben wird. Wählen Sie **Dateiname** aus, um den Dateinamen und Pfad direkt einzugeben, oder **Dateiname aus Variable** , um eine Variable anzugeben, die den Dateinamen enthält.  
  
 **Dateiname** oder **Variablenname**  
 Geben Sie den Namen und Pfad der Rohdatendatei ein, oder wählen Sie die Variable aus, die den Dateinamen enthält.  
  
 **Schreiboption**  
 Wählen Sie die Methode aus, die zum Erstellen und Schreiben in die Datei verwendet wird.  
  
 **Generieren einer anfänglichen Rohdatendatei**  
 Klicken Sie auf die Schaltfläche, um eine leere Rohdatendatei zu generieren, die nur die Spalten (Nur-Metadatendatei) enthält, ohne dass das Paket ausgeführt werden muss. Die Datei enthält die Spalten, die Sie auf der Seite **Spalten** von **Ziel-Editor für Rohdatendateien**ausgewählt haben. Sie können die Rohdatendatei-Quelle auf diese Nur-Metadaten-Datei verweisen.  
  
 Wenn Sie auf **Anfängliche Rohdatendatei generieren**klicken, wird ein Meldungsfeld angezeigt. Klicken Sie auf **OK** , um die Erstellung der Datei fortzusetzen. Klicken Sie auf **Abbrechen** , um eine andere Liste von Spalten auf der Seite **Spalten** auszuwählen.  
  
###  <a name="mapping"></a> Festlegen von Optionen auf der Registerkarte "Spalten"  
 **Verfügbare Eingabespalten**  
 Wählen Sie mindestens eine Eingabespalte aus, die in die Rohdatendatei geschrieben werden soll.  
  
 **Eingabespalte**  
 Dieser Tabelle wird automatisch eine Eingabespalte hinzugefügt, wenn Sie sie unter **Verfügbare Eingabespalten**auswählen. Alternativ können Sie die Eingabespalte direkt in dieser Tabelle auswählen.  
  
 **Ausgabealias**  
 Geben Sie einen anderen Namen an, der für die Ausgabespalte verwendet werden soll.  
  
## <a name="raw-file-destination-editor-columns-page"></a>Ziel-Editor für Rohdatendateien (Seite Spalten)
  Verwenden Sie den Ziel-Editor für Rohdatendateien zum Konfigurieren des Rohdatendatei-Ziels, um Rohdaten in eine Datei zu schreiben.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Ziel-Editors für Rohdatendateien](#open)  
  
-   [Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"](#connection)  
  
-   [Festlegen von Optionen auf der Registerkarte "Spalten"](#mapping)  
  
###  <a name="open"></a> Öffnen des Ziel-Editors für Rohdatendateien  
  
1.  Fügen Sie das Rohdatendatei-Ziel in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einem [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Paket hinzu.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Komponente, und klicken Sie anschließend auf **Bearbeiten**.  
  
###  <a name="connection"></a> Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"  
 **Zugriffsmodus**  
 Wählen Sie aus, wie der Dateiname angegeben wird. Wählen Sie **Dateiname** aus, um den Dateinamen und Pfad direkt einzugeben, oder **Dateiname aus Variable** , um eine Variable anzugeben, die den Dateinamen enthält.  
  
 **Dateiname** oder **Variablenname**  
 Geben Sie den Namen und Pfad der Rohdatendatei ein, oder wählen Sie die Variable aus, die den Dateinamen enthält.  
  
 **Schreiboption**  
 Wählen Sie die Methode aus, die zum Erstellen und Schreiben in die Datei verwendet wird.  
  
 **Generieren einer anfänglichen Rohdatendatei**  
 Klicken Sie auf die Schaltfläche, um eine leere Rohdatendatei zu generieren, die nur die Spalten (Nur-Metadatendatei) enthält, ohne dass das Paket ausgeführt werden muss. Sie können die Rohdatendatei-Quelle auf die Nur-Metadaten-Datei verweisen.  
  
 Wenn Sie auf die Schaltfläche klicken, wird eine Liste der Spalten angezeigt. Sie können auf "Abbrechen" klicken und die Spalten ändern, oder klicken Sie auf "OK", um das Erstellen der Datei fortzusetzen.  
  
###  <a name="mapping"></a> Festlegen von Optionen auf der Registerkarte "Spalten"  
 **Verfügbare Eingabespalten**  
 Wählen Sie mindestens eine Eingabespalte aus, die in die Rohdatendatei geschrieben werden soll.  
  
 **Eingabespalte**  
 Dieser Tabelle wird automatisch eine Eingabespalte hinzugefügt, wenn Sie sie unter **Verfügbare Eingabespalten**auswählen. Alternativ können Sie die Eingabespalte direkt in dieser Tabelle auswählen.  
  
 **Ausgabealias**  
 Geben Sie einen anderen Namen an, der für die Ausgabespalte verwendet werden soll.  
  
## <a name="see-also"></a>Siehe auch  
 [Rohdatendatei-Quelle](../../integration-services/data-flow/raw-file-source.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  

