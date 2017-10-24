---
title: 'Schritt 3: Durchsuchen und Visualisieren von Daten | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
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
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 31fa666c98948dc18f7aad988de795809594d2dd
ms.contentlocale: de-de
ms.lasthandoff: 10/18/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>Schritt 3: Durchsuchen und Visualisieren von Daten

Dieser Artikel ist Teil eines Lernprogramms [In Datenbank-Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md). 

In diesem Schritt Untersuchen der Beispieldaten und einige Darstellungen zu generieren. Später erfahren Sie, wie Grafikobjekten in Python, serialisieren und Deserialisieren von diesen Objekten und stellen grafische Darstellungen.

## <a name="review-the-data"></a>Überprüfen Sie die Daten

Zuerst, nehmen Sie sich zum Durchsuchen des Datenschemas haben wir einige Änderungen erleichtern die NYC Taxi Daten verwenden

+ Das ursprüngliche Dataset verwendet separate Dateien für die Taxi Bezeichner und Reise Datensätze. Wir haben die beiden ursprünglichen Datasets verknüpft, auf die Spalten _Medallion_, _Hack_license_, und _Pickup_datetime_.  
+ Das ursprüngliche Dataset umfasst viele Dateien auf und war sehr groß. Wir haben die abzurufenden nur 1 % der ursprünglichen Anzahl von Datensätzen aus. Die aktuellen Datentabelle hat 1,703,957 Zeilen und Spalten 23.

**Taxi-IDs**

Die _Medallion_ Spalte dar, die Taxi eindeutige ID-Nummer.

Die _Hack_license_ Spalte enthält den Taxi Treiber Lizenznummer (anonymisiert).

**Datensätze von Fahrten und Fahrpreisen**

Jeder Datensatz für Fahrten enthält den genauen Abhol- und Zielort und die Zeit sowie die Fahrstrecke.

Jeder Fahrpreisdatensatz enthält die Zahlungsinformationen wie die Zahlungsart, der Gesamtbetrag und den Fahrtpreis.

Die letzten drei Spalten können für verschiedene Machine Learning-Tasks verwendet werden.  Die Spalte _tip_amount_ enthält fortlaufende numerische Werte und kann als die **label** -Spalte für die Regressionsanalyse verwendet werden. Die Spalte _tipped_ verfügt nur über Ja/Nein-Werte und wird für die binäre Klassifikation verwendet. Die _tip_class_ -Spalte weist mehrere **Klassenbezeichnungen** auf und kann deshalb als Bezeichnung für mehrklassige Klassifizierungsaufgaben verwendet werden.

Die Werte für die Bezeichnungsspalte basieren auf der `tip_amount` Spalte mithilfe dieser Geschäftsregeln:

+ Bezeichnungsspalte `tipped` verfügt über die möglichen Werte 0 und 1

    Wenn `tip_amount` > 0, `tipped` = 1; andernfalls `tipped` = 0

+ Bezeichnungsspalte `tip_class` verfügt über mögliche Klassenwerte 0 – 4

    Klasse 0: `tip_amount` = $0

    Klasse 1: `tip_amount` > $0 und `tip_amount` < = 5 $
    
    Klasse 2: `tip_amount` > 5 $ und `tip_amount` < = $10
    
    Klasse 3: `tip_amount` > $10 und `tip_amount` < = $20
    
    Klasse 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Erstellen von Darstellungen, die mithilfe von Python in T-SQL

Das Entwickeln einer Data Science-Lösung bringt normalerweise die intensive Untersuchung und Visualisierung von Daten mit sich. Da Visualisierung ein leistungsstarkes Tool für die Verteilung der Daten und Ausreißer ist, stellt Python viele Pakete für die visuelle Darstellung der Daten bereit. Die **Matplotlib** Modul ist eine der gängigeren Bibliotheken für Visualisierung und beinhaltet zahlreiche Funktionen zum Erstellen von Histogrammen, Punktdiagrammen Feld Zeichnungen und andere Daten zum Durchsuchen von Diagrammen.

In diesem Abschnitt erfahren Sie, wie zur Bearbeitung der Darstellungen, die mithilfe von gespeicherten Prozeduren. Stattdessen als das Abbild auf dem Server zu öffnen, speichern Sie die Python-Objekt `plot` als **Varbinary** Daten, und klicken Sie dann schreiben, dass in einer Datei, kann freigegeben oder an anderer Stelle angezeigt.

### <a name="create-a-plot-as-varbinary-data"></a>Erstellen Sie eine grafische Ausgabe als Varbinary-Daten

Die **Revoscalepy** Lieferumfang von SQL Server 2017 Machine Learning-Services-Modul unterstützt Funktionen ähnlich denen in der **"revoscaler"** -Paket für R.  Dieses Beispiel verwendet die Python-Entsprechung des `rxHistogram` , zeichnen ein Histogramm, das basierend auf Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage. 

Die gespeicherte Prozedur gibt eine serialisierten Python `figure` Objekt als Datenstrom von **Varbinary** Daten. Sie können die Binärdaten direkt, sondern Sie können mithilfe von Python-Code auf dem Client zum Deserialisieren und die Zahlen anzeigen und speichern Sie die Bilddatei auf einem Clientcomputer.

1. Erstellen Sie die gespeicherte Prozedur _SerializePlots_, wenn das PowerShell-Skript nicht bereits geschehen ist.

    - Die Variable `@query` definiert den Abfragetext `SELECT tipped FROM nyctaxi_sample`, die an die Python-Code-Block übergeben wird, als Argument für das Skript Eingabevariable `@input_data_1`.
    - Python-Skript ist recht einfach: **Matplotlib** `figure` Objekte werden verwendet, um die Zeichnung Histogramm und Punktdiagrammen vornehmen und diese Objekte werden dann mit serialisiert die `pickle` Bibliothek.
    - Python-Grafikobjekt serialisiert wird, um eine **Pandas** Datenrahmen für die Ausgabe.
  
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

2. Führen Sie die gespeicherte Prozedur jetzt ohne Argumente, um eine grafische Ausgabe aus den Daten, die als Eingabeabfrage hartcodierte zu generieren.

    ```
    EXEC [dbo].[SerializePlots]
    ```

3. Die Ergebnisse sollten etwa wie folgt aussehen:
  
    ```
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Von einem Python-Client können Sie jetzt Herstellen einer Verbindung mit SQL Server-Instanz, die die binäre Darstellung Objekte generiert, und die Darstellungen anzeigen. 

    Führen Sie dazu die folgenden Python-Code, und Ersetzen Sie dabei den Servernamen, den Datenbanknamen und die Anmeldeinformationen nach Bedarf. Stellen Sie sicher, dass die Python-Version auf dem Client und dem Server identisch ist. Stellen Sie außerdem sicher, dass die Python-Bibliotheken auf dem Client (z. B. Matplotlib) die gleiche oder eine höhere Version relativ zu den Bibliotheken, die auf dem Server installiert sind.
  
    **Verwenden von SQL Server-Authentifizierung:**
    
    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Mithilfe der Windows-Authentifizierung:**

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

5.  Wenn die Verbindung erfolgreich ist, sollte eine Meldung wie folgt angezeigt werden:
  
    *Die Darstellungen werden im Verzeichnis gespeichert: Xxxx*
  
6.  Die Ausgabedatei wird in das Arbeitsverzeichnis Python erstellt. Anzeigen des Diagramms, das Python-Arbeitsverzeichnis suchen und öffnen Sie die Datei. Die folgende Abbildung zeigt eine grafische Ausgabe auf dem Clientcomputer gespeichert.
  
    ![Tipp Betrag Vs Fahrpreis Betrag](media/sqldev-python-sample-plot.png "Tipp Betrag Vs Fahrpreis Menge") 

## <a name="next-step"></a>Nächster Schritt

[Schritt 4: Erstellen von Datenfunktionen mit T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Schritt 2: Importieren von Daten nach SQL Server mithilfe von PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)


