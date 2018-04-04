---
title: 'Lektion 3: Durchsuchen und Visualisieren von Daten | Microsoft Docs'
ms.custom: ''
ms.date: 07/26/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: db9e21e69090c198af7b2ecfd2aad30c0877488d
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>Lektion 3: Durchsuchen und Visualisieren von Daten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil eines Lernprogramms für SQL-Entwicklern zum Verwenden von R in SQL Server.

Sie müssen in dieser Lektion überprüfen Sie die Beispieldaten und generieren Sie dann einige grafische Darstellungen in R-Funktionen verwenden. Diese R-Funktionen sind bereits in enthaltenen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Sie können die R-Funktionen aus aufrufen [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="review-the-data"></a>Überprüfen Sie die Daten

Das Entwickeln einer Data Science-Lösung bringt normalerweise die intensive Untersuchung und Visualisierung von Daten mit sich. Daher zuerst nehmen Sie sich, überprüfen die Beispieldaten, sofern Sie noch nicht geschehen.

Im ursprünglichen Dataset wurden die Taxi-IDs und die Fahrtendatensätze in separaten Dateien bereitgestellt. Jedoch, um die Beispieldaten einfacher zu verwenden ist, die beiden ursprünglichen Datasets verknüpft wurde für die Spalten _Medallion_, _hack\_Lizenz_, und _Abholung\_ "DateTime"_.  Die Datensätze wurden ebenso auf Stichproben reduziert, um nur 1 % der ursprünglichen Anzahl der Datensätze zu erhalten. Der auf Stichproben reduzierte Datensatz hat 1.703.957 Zeilen und 23 Spalten.

**Taxi-IDs**
  
-   Die Spalte _medallion_ stellt die eindeutige ID-Nummer des Taxis dar.
  
-   Die _hack\_Lizenz_ Spalte enthält den Taxi Treiber Lizenznummer (anonymisiert).
  
**Datensätze von Fahrten und Fahrpreisen**
  
-   Jeder Datensatz für Fahrten enthält den genauen Abhol- und Zielort und die Zeit sowie die Fahrstrecke.
  
-   Jeder Fahrpreisdatensatz enthält die Zahlungsinformationen wie die Zahlungsart, der Gesamtbetrag und den Fahrtpreis.
  
-   Die letzten drei Spalten können für verschiedene Machine Learning-Tasks verwendet werden.  Die _Tipp\_Betrag_ Spalte kontinuierliche numerische Werte enthält, und kann verwendet werden, als die **Bezeichnung** Spalte für Regressionsanalyse. Die Spalte _tipped_ verfügt nur über Ja/Nein-Werte und wird für die binäre Klassifikation verwendet. Die _Tipp\_Klasse_ Spalte weist mehrere **-Klasse Bezeichnungen** und kann daher für mehrklassige Klassifizierungsaufgaben als Bezeichnung verwendet werden.
  
    Diese exemplarische Vorgehensweise enthält nur die binäre Klassifizierungsaufgabe. Sie können gerne versuchen, Modelle für die anderen beiden Machine Learning-Tasks und für mehrklassige Klassifizierung zu erstellen.
  
-   Die Werte für die Bezeichnungsspalte basieren auf der _Tipp\_Betrag_ Spalte mithilfe dieser Geschäftsregeln:
  
    |Name der abgeleiteten Spalte|Rule|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>Erstellen von Darstellungen, die Verwendung von R in T-SQL

Da die Visualisierung ein leistungsfähiges Tool für das Verständnis der Verteilung von Daten- und Ausreißern ist, stellt R viele Pakete für die Visualisierung von Daten bereit. Die Open Source-Standardverteilung von R enthält auch viele Funktionen für die Erstellung von Histogrammen, Punktdiagrammen, Boxplots sowie andere Diagramme zum Untersuchen von Daten.

R erstellt in der Regel Bilder mithilfe eines R-Geräts für die grafische Ausgabe. Sie können die Ausgabe dieses Geräts erfassen und das Bild in einem **varbinary** -Datentyp für das Rendering in einer Anwendung speichern. Alternativ können Sie die Bilder in einem beliebigen Dateiformat speichern (.jpg, .pdf usw).

In diesem Abschnitt erfahren Sie, wie Sie mit jeder Art von Ausgabe mithilfe von gespeicherten Prozeduren arbeiten. Das generelle Verfahren ist wie folgt aus:

- Erstellen einer gespeicherten Prozedur um ein R-Plots als Varbinary-Daten zu generieren.

- Generieren Sie des Diagramms, und speichern Sie es in eine Bilddatei

- Verwenden Sie eine gespeicherte Prozedur, um die binäre Darstellung-Daten in einer JPG oder PDF-Datei konvertieren

### <a name="create-the-stored-procedure-plothistogram"></a>Erstellen Sie die gespeicherte Prozedur PlotHistogram

1. Verwenden Sie zum Erstellen des Diagramms `rxHistogram`, eine der erweiterten R-Funktionen, die in bereitgestellten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], zeichnen ein Histogramm, das basierend auf Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage. Damit die R-Funktion einfacher aufgerufen werden kann, schließen Sie sie in einer gespeicherten Prozedur, _PlotHistogram_, ein.

    In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], öffnen Sie ein neues **Abfrage** Fenster.

2. Erstellen Sie in der Datenbank, die das Lernprogrammen Daten enthält, die Prozedur, die mit dieser Anweisung ein:

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

    Achten Sie darauf, dass Sie den Code bei Bedarf ändern, um den richtigen Tabellennamen zu verwenden.
  
    -   Die Variable `@query` definiert den Abfragetext (`'SELECT tipped FROM nyctaxi_sample'`), der an das R-Skript als das Argument für die Skripteingabevariable, `@input_data_1`, übergeben wird.
  
    -   R-Skript ist recht einfach: Eine R-Variable (`image_file`) wird definiert, um das Bild zu speichern. Anschließend wird die `rxHistogram` -Funktion aufgerufen, um die Zeichnung zu generieren.
  
    -   Das R-Gerät wird auf **aus**festgelegt.
  
        Wenn Sie in R einen Zeichenbefehl für hohe Ebenen ausgeben, öffnet R ein Grafikfenster, das *device*genannt wird. Sie können die Größe und Farben sowie andere Aspekte des Fensters ändern. Sie können alternativ das Gerät ausschalten, wenn Sie in eine Datei schreiben oder die Ausgabe auf eine andere Art handhaben.
  
    -   Das R-Grafikobjekt wird zu einem R-Datenrahmen für die Ausgabe serialisiert.

### <a name="generate-the-graphics-data-and-save-to-file"></a>Die Grafikdaten zu generieren und in Datei speichern

Die gespeicherte Prozedur gibt das Bild als Strom von varbinary-Daten zurück, die Sie natürlich nicht direkt anzeigen können. Sie können jedoch das Hilfsprogramm **bcp** verwenden, um die varbinary-Daten abzurufen und sie als Bilddatei auf einem Clientcomputer zu speichern.
  
1.  Führen Sie die folgende Anweisung in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aus:
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **Ergebnisse**
    
    *plot*
    *0xFFD8FFE000104A4649...*
  
2.  Öffnen Sie eine PowerShell-Eingabeaufforderung, führen Sie den folgenden Befehl aus, und stellen Sie den erforderlichen Instanznamen, Datenbanknamen, Benutzernamen und die Anmeldeinformationen als Argumente bereit:
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Befehlszeilenoptionen für Bcp Groß-und Kleinschreibung.
  
3.  Wenn die Verbindung erfolgreich hergestellt wurde, werden Sie dazu aufgefordert, weitere Informationen über das Format der Grafikdatei einzugeben. Drücken Sie bei jeder Eingabeaufforderung die EINGABETASTE, um die bestehenden Angaben zu akzeptieren, außer der folgenden Änderungen:
  
    -   Geben Sie für **prefix-length of field plot**0 ein
  
    -   Geben Sie **Y** ein, wenn Sie die Ausgabeparameter für den späteren Gebrauch speichern möchten.
  
    ```
    Enter the file storage type of field plot [varbinary(max)]:
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **Ergebnisse**
    
    ```
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > Wenn Sie die Formatinformationen in einer Datei (bcp.fmt) speichern, generiert das Hilfsprogramm **bcp** eine Formatdefinition, die Sie zukünftig auf ähnliche Befehle anwenden können, ohne zur Eingabe von Formatoptionen für Grafikdateien aufgefordert zu werden. Fügen Sie zum Verwenden der Formatdatei `-f bcp.fmt` an das Ende einer beliebigen Befehlszeile nach dem Argument „Kennwort“ ein.
  
4.  Die Ausgabedatei wird im gleichen Verzeichnis erstellt, in dem Sie den PowerShell-Befehl ausgeführt haben. Um die Grafik anzuzeigen, öffnen Sie einfach die Datei plot.jpg.
  
    ![Taxifahrten mit und ohne Trinkgeld](media/rsql-devtut-tippedornot.jpg "Taxifahrten mit und ohne Trinkgeld")  
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>Exportieren der gezeichneten Daten in eine Datei angezeigt werden kann

Ein R-Plots in eine binären Daten ausgeben Typ kann zwar zweckmäßig sein für die Nutzung von Anwendungen, aber es ist nicht sehr nützlich, um ein datenanalyst, der die gerenderte Zeichnung Phase zum Durchsuchen von Daten benötigt. In der Regel generiert der Datenanalyst mehrere Datenvisualisierungen, um Einblicke in die Daten aus verschiedenen Perspektiven zu erhalten.

Um Diagramme für Benutzer zu generieren, können Sie eine gespeicherte Prozedur, die die Ausgabe von R in gängigen Formaten wie z. B. erstellt. JPG. PDF-Datei, und. PNG. Nachdem die gespeicherte Prozedur die Grafik erstellt hat, öffnen Sie einfach die Datei, um die Zeichnung zu visualisieren.

1. Erstellen einer neue gespeicherten Prozedur _PlotInOutputFiles_, veranschaulicht, dass zum Schreiben von Histogrammen, Scatterplots und andere R Grafiken. JPG und. PDF-Format.

    In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], öffnen Sie ein neues **Abfrage** Fenster, und fügen Sie in der folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
    -   Die Ausgabe der SELECT-Abfrage in der gespeicherten Prozedur wird im Standarddatenrahmen von R, `InputDataSet`, gespeichert. Anschließend können verschiedene Zeichenfunktionen von R aufgerufen werden, um die tatsächlichen Grafikdateien zu generieren.
  
        Die meisten der eingebetteten R-Skripts stellen Optionen für diese Grafikfunktionen dar, z.B. `plot` oder `hist`.
  
    -   Alle Dateien werden im lokalen Ordner _C:\temp\Plots\\_ gespeichert. Der Zielordner wird durch die Argumente für das R-Skript als Teil der gespeicherten Prozedur definiert.  Sie können den Zielordner ändern, indem Sie den Wert der Variable, `mainDir`, ändern.
  
2.  Führen Sie die Anweisung aus, um die gespeicherte Prozedur zu erstellen.

    ```SQL
    EXEC PlotInOutputFiles
    ```

    **Ergebnisse**
    
    ```
    STDOUT message(s) from external script:
    [1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 
    
    C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]
    
    C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
    ```

    Die Zahlen in den Dateinamen werden nach dem Zufallsprinzip generiert, um sicherzustellen, dass Sie keine Fehlermeldung erhalten, wenn beim Schreiben in die vorhandene Datei.

3. Klicken Sie zum Anzeigen des Diagramms öffnen Sie den Zielordner, und überprüfen Sie die Dateien, die von der R-Code in der gespeicherten Prozedur erstellt wurden.

    + Die Datei `rHistogram_Tipped.jpg` zeigt die Anzahl der Roundtrips an, die einen Tipp im Vergleich zu den Roundtrips erhalten haben, die keine Tipp erhalten haben. (Das Histogramm ist ähnlich, die Sie im vorherigen Schritt generiert haben.)

    + Die Datei `rHistograms_Tip_and_Fare_Amount.pdf` zeigt die Verteilung der Tipp Mengen, gegen die Beträge der Fahrpreis gezeichnet.
    
    ![Histogramm mit Tip_amount und Fare_amount](media/rsql-devtut-tipamtfareamt.PNG "Histogramm mit Tip_amount und Fare_amount")

    + Die Datei `rXYPlots_Tip_vs_Fare_Amount.pdf` enthält eine Scatterplot mit der Fahrpreis-Menge auf der x-Achse und die QuickInfo-Menge auf der y-Achse.

    ![Tipp Betrag zeitlichen Verlauf Fahrpreis Menge dargestellt](media/rsql-devtut-tipamtbyfareamt.PNG "Tipp Betrag zeitlichen Verlauf Fahrpreis Menge dargestellt.")

2.  Um die Dateien in einem anderen Ordner auszugeben, ändern Sie den Wert der `mainDir` -Variable im R-Skript, das in der gespeicherten Prozedur gespeichert ist. Sie können auch das Skript ändern, damit es verschiedene Formate, mehr Dateien usw. ausgibt.

## <a name="next-lesson"></a>Nächste Lektion

[Lektion 4: Erstellen von Data-Funktionen, die mithilfe des T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Lektion 2: Importieren von Daten in SQL Server mit PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)
