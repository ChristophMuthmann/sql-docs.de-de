---
title: "Schritt 3: Untersuchen und Visualisieren von Daten (Tutorial f&#252;r datenbankinterne Advanced Analytics) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Schritt 3: Untersuchen und Visualisieren von Daten (Tutorial f&#252;r datenbankinterne Advanced Analytics)
Das Entwickeln einer Data Science-Lösung bringt normalerweise die intensive Untersuchung und Visualisierung von Daten mit sich. In diesem Schritt überprüfen Sie die Beispieldaten und generieren anschließend einige Diagramme mithilfe von R-Funktionen. Diese R-Funktionen sind bereits in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten. In dieser exemplarischen Vorgehensweise, üben Sie, R-Funktionen von [!INCLUDE[tsql](../../includes/tsql-md.md)] aufzurufen.  
  
## Überprüfen der Daten  
Nehmen Sie sich zunächst ein paar Minuten Zeit, um die Beispieldaten zu überprüfen, falls Sie das noch nicht getan haben.  
  
Im ursprünglichen Dataset wurden die Taxi-IDs und die Fahrtendatensätze in separaten Dateien bereitgestellt. Die beiden ursprünglichen Datasets wurden in den Spalten _medallion_, _hack_license_ und _pickup_datetime_ zusammengefügt, damit die Beispieldaten einfacher verwendet werden können.  Die Datensätze wurden ebenso auf Stichproben reduziert, um nur 1 % der ursprünglichen Anzahl der Datensätze zu erhalten. Der auf Stichproben reduzierte Datensatz hat 1.703.957 Zeilen und 23 Spalten.  
  
**Taxi-IDs**  
  
-   Die Spalte _medallion_ stellt die eindeutige ID-Nummer des Taxis dar.  
  
-   Die Spalte _hack_license_ enthält die (anonymisierte) Lizenznummer des Taxifahrers.  
  
**Datensätze von Fahrten und Fahrpreisen**  
  
-   Jeder Datensatz für Fahrten enthält den genauen Abhol- und Zielort und die Zeit sowie die Fahrstrecke.  
  
-   Jeder Fahrpreisdatensatz enthält die Zahlungsinformationen wie die Zahlungsart, der Gesamtbetrag und den Fahrtpreis.  
  
-   Die letzten drei Spalten können für verschiedene Machine Learning-Tasks verwendet werden.  Die Spalte _tip_amount_ enthält fortlaufende numerische Werte und kann als die **label**-Spalte für die Regressionsanalyse verwendet werden. Die Spalte _tipped_ verfügt nur über Ja/Nein-Werte und wird für die binäre Klassifikation verwendet. Die _tip_class_-Spalte weist mehrere **Klassenbezeichnungen** auf und kann deshalb als Bezeichnung für mehrklassige Klassifizierungsaufgaben verwendet werden.  
  
    Diese exemplarische Vorgehensweise enthält nur die binäre Klassifizierungsaufgabe. Sie können gerne versuchen, Modelle für die anderen beiden Machine Learning-Tasks und für mehrklassige Klassifizierung zu erstellen.  
  
-   Die Werte für die Bezeichnungsspalten basieren alle auf der _tip_amount_-Spalte und verwenden folgende Geschäftsregeln:  
  
    |Name der abgeleiteten Spalte|Rule|  
    |-|-|  
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|  
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|  
  
## Erstellen von Diagrammen mit R in T-SQL  
Da die Visualisierung ein leistungsfähiges Tool für das Verständnis der Verteilung von Daten- und Ausreißern ist, stellt R viele Pakete für die Visualisierung von Daten bereit. Die Open Source-Standardverteilung von R enthält auch viele Funktionen für die Erstellung von Histogrammen, Punktdiagrammen, Boxplots sowie andere Diagramme zum Untersuchen von Daten.  
  
R erstellt in der Regel Bilder mithilfe eines R-Geräts für die grafische Ausgabe. Sie können die Ausgabe dieses Geräts erfassen und das Bild in einem **varbinary**-Datentyp für das Rendering in einer Anwendung speichern. Alternativ können Sie die Bilder in einem beliebigen Dateiformat speichern (.jpg, .pdf usw).  
  
In diesem Abschnitt erfahren Sie, wie Sie mit jeder Art von Ausgabe mithilfe von gespeicherten Prozeduren arbeiten.  
  
-   Speichern von Diagrammen als varbinary-Datentyp  
  
-   Speichern von Diagrammen in Dateien (.jpg, .pdf) auf dem Server  
  
### Speichern von Diagrammen als varbinary-Datentyp  
Sie werden `rxHistogram` verwenden, eine der erweiterten R-Funktionen, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bereitgestellt werden, um ein Histogramm auf Grundlage von Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage zu zeichnen. Damit die R-Funktion einfacher aufgerufen werden kann, schließen Sie sie in einer gespeicherten Prozedur, _PlotHistogram_, ein.  
  
Die gespeicherte Prozedur gibt das Bild als Strom von varbinary-Daten zurück, die Sie natürlich nicht direkt anzeigen können. Sie können jedoch das Hilfsprogramm **bcp** verwenden, um die varbinary-Daten abzurufen und sie als Bilddatei auf einem Clientcomputer zu speichern.  
  
##### So erstellen Sie die gespeicherte Prozedur PlotHistogram  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ein neues Abfragefenster.  
  
2.  Wählen Sie die Datenbank für die exemplarische Vorgehensweise aus, und erstellen Sie die Prozedur mit dieser Anweisung.  
  
    ```  
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
  
    -   R-Skript ist recht einfach: Eine R-Variable (`image_file`) wird definiert, um das Bild zu speichern. Anschließend wird die `rxHistogram`-Funktion aufgerufen, um die Zeichnung zu generieren.  
  
    -   Das R-Gerät wird auf **aus** festgelegt.  
  
        Wenn Sie in R einen Zeichenbefehl für hohe Ebenen ausgeben, öffnet R ein Grafikfenster, das *device* genannt wird. Sie können die Größe und Farben sowie andere Aspekte des Fensters ändern. Sie können alternativ das Gerät ausschalten, wenn Sie in eine Datei schreiben oder die Ausgabe auf eine andere Art handhaben.  
  
    -   Das R-Grafikobjekt wird zu einem R-Datenrahmen für die Ausgabe serialisiert. Dies ist eine vorübergehende Problemumgehung für CTP3.  
  
##### So geben Sie varbinary-Daten in eine anzeigbare Grafikdatei aus  
  
1.  Führen Sie die folgende Anweisung in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] aus:  
  
    ```  
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
    > Befehlsschalter für **bcp** beachten die Groß-/Kleinschreibung.  
  
3.  Wenn die Verbindung erfolgreich hergestellt wurde, werden Sie dazu aufgefordert, weitere Informationen über das Format der Grafikdatei einzugeben. Drücken Sie bei jeder Eingabeaufforderung die EINGABETASTE, um die bestehenden Angaben zu akzeptieren, außer der folgenden Änderungen:  
  
    -   Geben Sie für **prefix-length of field plot** 0 ein  
  
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
  
*Kopiervorgang wird gestartet...*  
*1 Zeilen kopiert.*  
*Netzwerkpaketgröße (Bytes): 4096*  
*Uhrzeit (ms) Gesamt: 3922 Durchschnitt: (0,25 Zeilen pro Sekunde)*  
   
> [!TIP]  
 > Wenn Sie die Formatinformationen in einer Datei (bcp.fmt) speichern, generiert das Hilfsprogramm **bcp** eine Formatdefinition, die Sie zukünftig auf ähnliche Befehle anwenden können, ohne zur Eingabe von Formatoptionen für Grafikdateien aufgefordert zu werden. Fügen Sie zum Verwenden der Formatdatei `-f bcp.fmt` an das Ende einer beliebigen Befehlszeile nach dem Argument „Kennwort“ ein.  
  
4.  Die Ausgabedatei wird im gleichen Verzeichnis erstellt, in dem Sie den PowerShell-Befehl ausgeführt haben. Um die Grafik anzuzeigen, öffnen Sie einfach die Datei plot.jpg.  
  
    ![taxi trips with and without tips](../../advanced-analytics/r-services/media/rsql-devtut-tippedornot.jpg "taxi trips with and without tips")  
  
### Speichern von Diagrammen in Dateien (.jpg, .pdf) auf dem Server  
Die Ausgabe einer R-Zeichnung in einem binären Datentyp mag hilfreich für die Nutzung in Anwendungen sein. Ein Datenanalyst profitiert davon jedoch nicht, denn er benötigt beim Durchsuchen der Daten das gerenderte Diagramm. In der Regel generiert der Datenanalyst mehrere Datenvisualisierungen, um Einblicke in die Daten aus verschiedenen Perspektiven zu erhalten.  
  
Um Diagramme zu generieren, die leichter angezeigt werden können, können Sie eine gespeicherte Prozedur verwenden, die die Ausgabe von R in gängigen Formaten wie z.B. .jpg, .pdf und .png erstellt. Nachdem die gespeicherte Prozedur die Grafik erstellt hat, öffnen Sie einfach die Datei, um die Zeichnung zu visualisieren.  
  
In diesem Schritt erstellen Sie eine neue gespeicherte Prozedur _PlotInOutputFiles_, die veranschaulicht, wie R Zeichenfunktion zum Erstellen von Histogrammen, Punktdiagrammen usw. im JPG- und PDF-Format verwendet. Die Grafikdateien werden in lokalen Dateien gespeichert. Diese befinden sich in einem Ordner auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
##### So erstellen Sie die gespeicherte Prozedur PlotInOutputFiles  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ein neues Abfragefenster, und fügen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ein.  
  
    ```  
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
  
    -   Alle Dateien werden im lokalen Ordner _C:\temp\Plots\\_ gespeichert.  
  
        Der Zielordner wird durch die Argumente für das R-Skript als Teil der gespeicherten Prozedur definiert.  Sie können den Zielordner ändern, indem Sie den Wert der Variable, `mainDir`, ändern.  
  
2.  Führen Sie die Anweisung aus, um die gespeicherte Prozedur zu erstellen.  
  
  
##### So generieren Sie die Grafikdateien  
  
1.  Führen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] die folgende SQL-Anweisung aus:  
  
    ```  
    EXEC PlotInOutputFiles  
  
    ```  
  
**Ergebnisse**  
  
*STDOUT message(s) from external script:*  
*[1] Creating output plot files:[1]* *C:\\\temp\\\plots\\\rHistogram_Tipped_18887f6265d4.jpg[1]* *C:\\\temp\\\plots\\\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]* *C:\\\temp\\\plots\\\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf*  
  
2.  Öffnen Sie den Zielordner, und überprüfen Sie die Dateien, die vom R-Code in der gespeicherten Prozedur erstellt wurden. (Die Zahlen in den Dateinamen werden nach dem Zufallsprinzip generiert.)  
  
*  rHistogram_Tipped_*nnnn*.jpg: Zeigt die Anzahl der Fahrten an, bei denen der Fahrer ein Trinkgeld erhalten hat (1) vs. die Fahrten, bei denen der Fahrer kein Trinkgeld erhalten hat (0). Das Histogramm ist ähnlich wie das, das Sie im vorherigen Schritt erstellt haben.  
  
*  rHistograms_Tip_and_Fare_Amount_*nnnn*.pdf: Zeigt die Verteilung von Werten in den Spalten „tip_amount“ und „fare_amount“ an.  
  
        ![histogram showing tip_amount and fare_amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtfareamt.PNG "histogram showing tip_amount and fare_amount")  
  
*  rXYPlots_Tip_vs_Fare_Amount_*nnnn*.pdf: ein Punktdiagramm mit der Höhe des Fahrpreises auf der X-Achse und der Höhe des Trinkgelds auf der Y-Achse.  
  
        ![tip amount plotted over fare amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtbyfareamt.PNG "tip amount plotted over fare amount")  
  
3.  Um die Dateien in einem anderen Ordner auszugeben, ändern Sie den Wert der `mainDir`-Variable im R-Skript, das in der gespeicherten Prozedur gespeichert ist.  
  
    Sie können auch das Skript ändern, damit es verschiedene Formate, mehr Dateien usw. ausgibt.  
  
## Nächster Schritt  
[Schritt 4: Erstellen von Datenfunktionen mit T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Vorheriger Schritt  
[Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## Siehe auch  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Datenbankinterne Advanced-Analytics für SQL-Entwickler (Tutorial))](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
