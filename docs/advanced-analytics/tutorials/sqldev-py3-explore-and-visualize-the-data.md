---
title: 'Schritt 3: Untersuchen und Visualisieren von Daten | Microsoft-Dokumentation'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-python
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dfb80fcd3241b22f0ac72c2cf4cd8a18d1add857
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>Schritt 3: Untersuchen und Visualisieren von Daten

Das Entwickeln einer Data Science-Lösung bringt normalerweise die intensive Untersuchung und Visualisierung von Daten mit sich. In diesem Schritt haben Sie untersuchen der Beispieldaten und einige Darstellungen zu generieren. Später erfahren Sie, wie zum Serialisieren von Grafikobjekten in Python, und klicken Sie dann diese Objekt deserialisieren und Darstellungen.

> [!NOTE]
> Diese exemplarische Vorgehensweise enthält nur die binäre klassifikationsaufgabe; Willkommen beim TestBuild separate Modelle für die anderen beiden Machine Learning-Aufgaben, Regression und mehrklassige Klassifizierung werden.

## <a name="review-the-data"></a>Überprüfen der Daten

Im ursprünglichen Dataset wurden die Taxi-IDs und die Fahrtendatensätze in separaten Dateien bereitgestellt. Die beiden ursprünglichen Datasets wurden in den Spalten _medallion_, _hack_license_und _pickup_datetime_zusammengefügt, damit die Beispieldaten einfacher verwendet werden können.  Die Datensätze wurden ebenso auf Stichproben reduziert, um nur 1 % der ursprünglichen Anzahl der Datensätze zu erhalten. Der auf Stichproben reduzierte Datensatz hat 1.703.957 Zeilen und 23 Spalten.

**Taxi-IDs**

- Die Spalte _medallion_ stellt die eindeutige ID-Nummer des Taxis dar.
- Die Spalte _hack_license_ enthält die (anonymisierte) Lizenznummer des Taxifahrers.

**Datensätze von Fahrten und Fahrpreisen**

- Jeder Datensatz für Fahrten enthält den genauen Abhol- und Zielort und die Zeit sowie die Fahrstrecke.
- Jeder Fahrpreisdatensatz enthält die Zahlungsinformationen wie die Zahlungsart, der Gesamtbetrag und den Fahrtpreis.
- Die letzten drei Spalten können für verschiedene Machine Learning-Tasks verwendet werden.  Die Spalte _tip_amount_ enthält fortlaufende numerische Werte und kann als die **label** -Spalte für die Regressionsanalyse verwendet werden. Die Spalte _tipped_ verfügt nur über Ja/Nein-Werte und wird für die binäre Klassifikation verwendet. Die _tip_class_ -Spalte weist mehrere **Klassenbezeichnungen** auf und kann deshalb als Bezeichnung für mehrklassige Klassifizierungsaufgaben verwendet werden.
- Die Werte für die Bezeichnungsspalten basieren alle auf der _tip_amount_ -Spalte und verwenden folgende Geschäftsregeln:
  
    |Name der abgeleiteten Spalte|Rule|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-python-in-t-sql"></a>Erstellen von Darstellungen, die mithilfe von Python in T-SQL

Da Visualisierung ein leistungsstarkes Tool für die Verteilung der Daten und Ausreißer ist, stellt Python viele Pakete für die visuelle Darstellung der Daten bereit. Die **Matplotlib** -Modul ist eine beliebte Bibliothek, die viele Funktionen zum Erstellen von Histogrammen, Punktdiagrammen Feld Zeichnungen und anderen Daten zum Durchsuchen von Diagramme enthält.

In diesem Abschnitt erfahren Sie, wie zur Bearbeitung der Darstellungen, die mithilfe von gespeicherten Prozeduren. Speichern Sie die `plot` Python-Objekt als eine **Varbinary** Daten geben, und speichern Sie die auf dem Server generierten Darstellungen.

### <a name="storing-plots-as-varbinary-data-type"></a>Speichern von Diagrammen als varbinary-Datentyp

Die **Revoscalepy** Lieferumfang von SQL Server 2017 Machine Learning-Services-Modul enthält analog zu den R-Bibliotheken in der "revoscaler"-Paket Bibliotheken. In diesem Beispiel verwenden Sie die Python-Entsprechung des `rxHistogram` , zeichnen ein Histogramm, das basierend auf Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage. Um es zu vereinfachen, werden Sie es in einer gespeicherten Prozedur umschließen _PlotHistogram_.

Die gespeicherte Prozedur gibt eine serialisierten Python `figure` Objekt als Datenstrom von **Varbinary** Daten. Sie können die Binärdaten direkt, sondern Sie können mithilfe von Python-Code auf dem Client zum Deserialisieren und die Zahlen anzeigen und speichern Sie die Bilddatei auf einem Clientcomputer.

### <a name="create-the-stored-procedure-plotspython"></a>Erstellen Sie die gespeicherte Prozedur Plots_Python

1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], öffnen Sie ein neues **Abfrage** Fenster.

2.  Wählen Sie die Datenbank für die exemplarische Vorgehensweise aus, und erstellen Sie die Prozedur mit dieser Anweisung. Achten Sie darauf, dass Sie den Code bei Bedarf ändern, um den richtigen Tabellennamen zu verwenden.
  
    ```SQL
    
    CREATE PROCEDURE [dbo].[SerializePlots]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
      EXECUTE sp_execute_external_script
      @language = N'Python',
      @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
                                     @input_data_1 = @query
      WITH RESULT SETS ((plot varbinary(max)))
    END

    GO
  
    ```
**Hinweise:**

- Die Variable `@query` definiert den Text der Abfrage (`'SELECT tipped FROM nyctaxi_sample'`), die an die Python-Code-Block übergeben wird, als Argument für das Skript Eingabevariable `@input_data_1`.
- Python-Skript ist recht einfach: **Matplotlib** `figure` Objekte werden verwendet, um die Zeichnung Histogramm und Punktdiagrammen vornehmen und diese Objekte werden dann mit serialisiert die `pickle` Bibliothek.
- Python-Grafikobjekt in einem Python serialisiert wird **Pandas** Datenrahmen für die Ausgabe.

### <a name="output-varbinary-data-to-viewable-graphics-file"></a>Varbinary Ausgabedaten auf sichtbare Grafikdatei

1.  Führen Sie die folgende Anweisung in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aus:
  
    ```
    EXEC [dbo].[SerializePlots]
    ```
  
    **Ergebnisse**
  
    *Zeichnungsfläche*
    *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649...*

  
2.  Führen Sie auf dem Clientcomputer der folgenden Python-Codes, und Ersetzen Sie dabei den Servernamen, den Datenbanknamen und die Anmeldeinformationen nach Bedarf.
  
    **Für SQL Server-Authentifizierung:**
    
        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSOWRD}')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```  
    **Für Windows-Authentifizierung:**

        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=yes;')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```

    > [!NOTE]
    > Stellen Sie sicher, dass die Python-Version auf dem Client und dem Server identisch ist. Stellen Sie außerdem sicher, dass die Python-Bibliotheken, die Sie auf dem Client (z. B. Matplotlib) verwenden die gleiche oder eine höhere Version relativ zu den Bibliotheken, die auf dem Server installiert sind.


3.  Wenn die Verbindung erfolgreich ist, wird die folgenden Ergebnisse angezeigt werden.
  
    *Die Darstellungen werden im Verzeichnis gespeichert: Xxxx*
  
4.  Die Ausgabedatei wird im Arbeitsverzeichnis Python erstellt werden. Öffnen Sie einfach die Python-Arbeitsverzeichnis, zum Anzeigen des Diagramms. Die folgende Abbildung zeigt ein Beispiel-Darstellung, die auf dem Clientcomputer gespeichert.
  
    ![Tipp Betrag Vs Fahrpreis Betrag](media/sqldev-python-sample-plot.png "Tipp Betrag Vs Fahrpreis Menge") 

## <a name="next-step"></a>Nächster Schritt

[Schritt 4: Erstellen von Datenfunktionen mit T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)

