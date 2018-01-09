---
title: 'Lektion 2: Importieren von Daten in SQL Server mit PowerShell | Microsoft Docs'
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 720ef1ea70566b2b18febef3146aab9755a7ac5c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-2-import-data-to-sql-server-using-powershell"></a>Lektion 2: Importieren von Daten in SQL Server mit PowerShell

Dieser Artikel ist Teil eines Lernprogramms für SQL-Entwicklern zum Verwenden von R in SQL Server.

In diesem Skript führen Sie eines der heruntergeladenen Skripts aus, um das Datenbankobjekt zu erstellen, das für die exemplarische Vorgehensweise erforderlich ist. Das Skript erstellt außerdem die meisten der gespeicherten Prozeduren, die Sie verwenden werden, und lädt die Beispieldaten in eine Tabelle in der von Ihnen angegebenen Datenbank hoch.

## <a name="run-the-scripts-to-create-sql-objects"></a>Führen Sie die Skripts zum Erstellen von SQL-Objekte

Zwischen den heruntergeladenen Dateien sehen Sie ein PowerShell-Skript, das zum Vorbereiten der Umgebung für die exemplarische Vorgehensweise ausgeführt werden kann. Die vom Skript ausgeführten Aktionen beinhalten:

- Installieren von SQL Native Client und Befehlszeilen-Hilfsprogrammen von SQL, falls diese noch nicht installiert sind. Diese Hilfsprogramme werden für das Massenladen der Daten in die Datenbank mithilfe von **bcp**benötigt.

- Erstellen einer Datenbank und einer Tabelle für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz und Masseneinfügen von Daten in die Tabelle

- Erstellen mehrerer SQL-Funktionen und gespeicherter Prozeduren.

### <a name="run-the-script"></a>Führen Sie das Skript

1.  Öffnen Sie ein PowerShell-Eingabeaufforderungsfenster als Administrator, und führen Sie den folgenden Befehl aus.
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```
  
    Sie werden aufgefordert, die folgenden Informationen einzugeben:
  
    - Den Namen oder die Adresse einer [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz, auf der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert wurde
  
    - Den Benutzernamen und das Kennwort für ein Konto auf der Instanz. Das Konto muss Berechtigungen zum Erstellen von Datenbanken, Tabellen und gespeicherte Prozeduren erstellen und Hochladen von Daten in Tabellen verfügen. Wenn Sie nicht den Benutzernamen und das Kennwort angeben, wird Ihre Windows-Identität verwendet SQL Server anzumelden.
  
    - Der Pfad und der Dateiname der Beispieldatendatei, die Sie zuvor heruntergeladen haben. Beispiel:
  
        `C:\tempRSQL\nyctaxi1pct.csv`
  
2.  Als Teil dieses Schritts werden auch alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts geändert, um Platzhalter mit dem Datenbanknamen und Benutzernamen zu ersetzen, die Sie als Skripteingaben bereitgestellt haben.
  
    Nehmen Sie sich ein paar Minuten Zeit, um die gespeicherten Prozeduren und die vom Skript erstellten Funktionen zu überprüfen.
  
    |**Name der SQL-Skriptdatei**|**Funktion**|
    |-|-|
    |create-db-tb-upload-data.sql|Erstellt eine Datenbank und zwei Tabellen:<br /><br />nyctaxi_sample: enthält das Hauptdataset von NYC Taxi Einer Tabelle wird ein gruppierter Columnstore-Index hinzugefügt, um den Speicher und die Abfrageleistung zu verbessern. Das 1 %-Beispiel des Hauptdataset von NYC Taxi wird in diese Tabelle eingefügt.<br /><br />nyc_taxi_models: wird verwendet, um das trainierte Modell für die erweiterte Analyse zu speichern|
    |fnCalculateDistance.sql|Erstellt eine Skalarwertfunktion, die die direkte Entfernung zwischen Abhol-und Zielorten berechnet|
    |fnEngineerFeatures.sql|Erstellt eine Tabellenwertfunktion, die neue Datenfunktionen für das Modelltraining erstellt|
    |PersistModel.sql|Erstellt eine gespeicherte Prozedur, die aufgerufen werden kann, um ein Modell zu speichern. Die gespeicherte Prozedur schreibt ein Modell, das in einen varbinary-Datentyp serialisiert wurde, in die bestimmte Tabelle.|
    |PredictTipBatchMode.sql|Erstellt eine gespeicherte Prozedur, die das trainierte Modell zum Erstellen von Vorhersagen mit dem Modell aufruft. Die gespeicherte Prozedur akzeptiert eine Abfrage als Eingabeparameter und gibt eine Spalte mit numerischen Werten zurück, die die Bewertungen für die Eingabezeilen enthält.|
    |PredictTipSingleMode.sql|Erstellt eine gespeicherte Prozedur, die das trainierte Modell zum Erstellen von Vorhersagen mit dem Modell aufruft. Diese gespeicherte Prozedur akzeptiert als Eingabe eine neue Beobachtung mit einzelnen Funktionswerten, die als Inlineparameter übergeben werden, und gibt einen Wert zurück, der das Ergebnis für die neue Beobachtung vorhersagt.|
  
    Im letzten Teil dieser exemplarischen Vorgehensweise erstellen Sie einige zusätzliche gespeicherte Prozeduren:
  
    |**Name der SQL-Skriptdatei**|**Funktion**|
    |------|------|
    |PlotHistogram.sql|Erstellt eine gespeicherte Prozedur zum Durchsuchen von Daten. Diese gespeicherte Prozedur ruft eine R-Funktion auf, um das Histogramm einer Variablen zu zeichnen und gibt anschließend das Diagramm als binäres Objekt zurück.|
    |PlotInOutputFiles.sql|Erstellt eine gespeicherte Prozedur zum Durchsuchen von Daten. Diese gespeicherte Prozedur erstellt eine Grafik mithilfe einer R-Funktion und speichert die Ausgabe anschließend als lokale PDF-Datei.|
    |TrainTipPredictionModel.sql|Erstellt eine gespeicherte Prozedur, die ein logistisches Regressionsmodell trainiert, indem ein R-Paket aufgerufen wird. Das Modell sagt den Wert der tipped-Spalte voraus und wird mithilfe von zufällig ausgewählten 70 % der Daten trainiert. Die Ausgabe der gespeicherten Prozedur ist das trainierte Modell, das in der Tabelle nyc_taxi_models gespeichert wird.|
  
3.  Melden Sie sich bei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und dem von Ihnen angegebenen Anmeldenamen an, um zu überprüfen, ob Sie die Datenbank, die Tabellen, die Funktionen und die gespeicherten Prozeduren anzeigen können, die erstellt wurden.
  
    ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")
  
    > [!NOTE]
    > Wenn das Datenbankprojekt schon vorhanden ist, dann kann es nicht noch einmal erstellt werden.
    >   
    > Wenn die Tabelle bereits vorhanden ist, werden die Daten angefügt, nicht überschrieben. Achten Sie daher darauf, vorhandene Objekte zu löschen, bevor Sie das Skript ausführen.

## <a name="next-lesson"></a>Nächste Lektion

[Lektion 3: Durchsuchen und Visualisieren von Daten](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Lektion 1: Herunterladen der Beispieldaten](../tutorials/sqldev-download-the-sample-data.md)
