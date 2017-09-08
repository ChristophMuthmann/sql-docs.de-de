---
title: 'Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell | Microsoft-Dokumentation'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-vnext-ctp2
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
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
ms.openlocfilehash: 62a06d6c442428132f84b3f8e5a665e872a8d361
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell

In diesem Skript führen Sie eines der heruntergeladenen Skripts aus, um das Datenbankobjekt zu erstellen, das für die exemplarische Vorgehensweise erforderlich ist. Das Skript erstellt außerdem die meisten der gespeicherten Prozeduren, die Sie verwenden werden, und lädt die Beispieldaten in eine Tabelle in der von Ihnen angegebenen Datenbank hoch.

## <a name="create-sql-objects-and-data"></a>Erstellen von SQL-Objekte und Daten

Unter den heruntergeladenen Dateien sollte ein PowerShell-Skript angezeigt werden. Führen Sie dieses Skript aus, um die Umgebung für die exemplarische Vorgehensweise vorzubereiten.  Das Skript führt folgende Aktionen aus:

- Der SQL Native Client und SQL-Befehlszeilen-Hilfsprogramme, installiert werden, sofern nicht bereits installiert. Diese Hilfsprogramme werden für das Massenladen der Daten in die Datenbank mithilfe von **bcp**benötigt.

- Erstellt eine Datenbank und eine Tabelle für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz und masseneinfügungen Daten in der Tabelle.

- Mehrere SQL-Funktionen und gespeicherten Prozeduren erstellt.

### <a name="run-the-script"></a>Führen Sie das Skript

1. Öffnen Sie ein PowerShell-Eingabeaufforderungsfenster als Administrator, und führen Sie den folgenden Befehl aus.
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  

    Sie werden aufgefordert, die folgenden Informationen einzugeben:
    - Der Name oder die Adresse des eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Instanz, in denen Machine learning-Dienste mit Python installiert wurde,
    - Den Benutzernamen und das Kennwort für ein Konto auf der Instanz. Das Konto, das Sie verwenden, muss Datenbanken, Tabellen und gespeicherte Prozeduren erstellen können und Daten in Tabellen hochladen können. Wenn Sie nicht den Benutzernamen und das Kennwort angeben, wird Ihre Windows-Identität verwendet SQL Server anzumelden.
    - Der Pfad und der Dateiname der Beispieldatendatei, die Sie zuvor heruntergeladen haben. Beispielsweise `C:\tempRSQL\nyctaxi1pct.csv`

    > [!NOTE]
    > Stellen Sie sicher, dass Ihre "xmlrw.dll" im gleichen Ordner wie die bcp.exe ist. Wenn dies nicht der Fall ist, kopieren Sie diese über.

2.  Als Teil dieses Schritts werden auch alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts geändert, um Platzhalter mit dem Datenbanknamen und Benutzernamen zu ersetzen, die Sie als Skripteingaben bereitgestellt haben.
  
3. Nehmen Sie sich ein paar Minuten Zeit, um die gespeicherten Prozeduren und die vom Skript erstellten Funktionen zu überprüfen.
     
    |**Name der SQL-Skriptdatei**|**Funktion**|
    |------|------|
    |create-db-tb-upload-data.sql|Erstellt eine Datenbank und zwei Tabellen:<br /><br />nyctaxi_sample: enthält das Hauptdataset von NYC Taxi Einer Tabelle wird ein gruppierter Columnstore-Index hinzugefügt, um den Speicher und die Abfrageleistung zu verbessern. Das 1 %-Beispiel des Hauptdataset von NYC Taxi wird in diese Tabelle eingefügt.<br /><br />nyc_taxi_models: wird verwendet, um das trainierte Modell für die erweiterte Analyse zu speichern|
    |fnCalculateDistance.sql|Erstellt eine Skalarwertfunktion, die die direkte Entfernung zwischen Abhol-und Zielorten berechnet|
    |fnEngineerFeatures.sql|Erstellt eine Tabellenwertfunktion, die neue Datenfunktionen für das Modelltraining erstellt|
    |TrainingTestingSplit.sql|Die Daten in der Tabelle Nyctaxi_sample in zwei Teile aufzuteilen: Nyctaxi_sample_training und Nyctaxi_sample_testing.|
    |PredictTipSciKitPy.sql|Erstellt eine gespeicherte Prozedur, die das trainierte Modell aufruft (Scikit-Informationen) zum Erstellen von Vorhersagen mit dem Modell. Die gespeicherte Prozedur akzeptiert eine Abfrage als Eingabeparameter und gibt eine Spalte mit numerischen Werten zurück, die die Bewertungen für die Eingabezeilen enthält.|
    |PredictTipRxPy.sql|Erstellt eine gespeicherte Prozedur, die das trainierte Modell (Revoscalepy) zum Erstellen von Vorhersagen mit dem Modell aufruft. Die gespeicherte Prozedur akzeptiert eine Abfrage als Eingabeparameter und gibt eine Spalte mit numerischen Werten zurück, die die Bewertungen für die Eingabezeilen enthält.|
    |PredictTipSingleModeSciKitPy.sql|Erstellt eine gespeicherte Prozedur, die das trainierte Modell aufruft (Scikit-Informationen) zum Erstellen von Vorhersagen mit dem Modell. Diese gespeicherte Prozedur akzeptiert als Eingabe eine neue Beobachtung mit einzelnen Funktionswerten, die als Inlineparameter übergeben werden, und gibt einen Wert zurück, der das Ergebnis für die neue Beobachtung vorhersagt.|
    |PredictTipSingleModeRxPy.sql|Erstellt eine gespeicherte Prozedur, die das trainierte Modell (Revoscalepy) zum Erstellen von Vorhersagen mit dem Modell aufruft. Diese gespeicherte Prozedur akzeptiert als Eingabe eine neue Beobachtung mit einzelnen Funktionswerten, die als Inlineparameter übergeben werden, und gibt einen Wert zurück, der das Ergebnis für die neue Beobachtung vorhersagt.|
  
4. Im letzten Teil dieser exemplarischen Vorgehensweise erstellen Sie einige zusätzliche gespeicherte Prozeduren:
    
    |**Name der SQL-Skriptdatei**|**Funktion**|
    |------|------|
    |SerializePlots.sql|Erstellt eine gespeicherte Prozedur zum Durchsuchen von Daten. Diese gespeicherte Prozedur erstellt eine Grafik, die mithilfe von Python und Serialisieren Sie dann auf die Graph-Objekte.|
    |TrainTipPredictionModelSciKitPy.sql|Erstellt eine gespeicherte Prozedur, die ein Logistisches Regressionsmodell trainiert (Scikit-Informationen). Das Modell sagt für den Wert der Spalte Geneigter und wird mithilfe eines zufällig ausgewähltes 60 % der Daten trainiert. Die Ausgabe der gespeicherten Prozedur ist das trainierte Modell, das in der Tabelle nyc_taxi_models gespeichert wird.|
    |TrainTipPredictionModelRxPy.sql|Erstellt eine gespeicherte Prozedur, die ein Logistisches Regressionsmodell (Revoscalepy) trainiert. Das Modell sagt für den Wert der Spalte Geneigter und wird mithilfe eines zufällig ausgewähltes 60 % der Daten trainiert. Die Ausgabe der gespeicherten Prozedur ist das trainierte Modell, das in der Tabelle nyc_taxi_models gespeichert wird.|
  
3. Melden Sie sich bei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und dem von Ihnen angegebenen Anmeldenamen an, um zu überprüfen, ob Sie die Datenbank, die Tabellen, die Funktionen und die gespeicherten Prozeduren anzeigen können, die erstellt wurden.

    ![Durchsuchen von Tabellen in SSMS](media/sqldev-python-browsetables1.png "Tabellen in SSMS anzeigen")

    > [!NOTE]
    > Wenn das Datenbankprojekt schon vorhanden ist, dann kann es nicht noch einmal erstellt werden. Wenn die Tabelle bereits vorhanden ist, werden die Daten angefügt, nicht überschrieben. Achten Sie daher darauf, vorhandene Objekte zu löschen, bevor Sie das Skript ausführen.
    > Führen Sie die Anweisungen [hier](https://docs.microsoft.com/en-us/sql/advanced-analytics/r/set-up-sql-server-r-services-in-database#bkmk_enableFeature) , externes Skript-Dienste zu aktivieren.
    


## <a name="next-step"></a>Nächster Schritt

[Schritt 3: Untersuchen und Visualisieren von Daten](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Schritt 1: Herunterladen der Beispieldateien](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)



