---
title: 'Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete | Microsoft-Dokumentation'
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: dcd06bcdf2fbfbb4aaa405c77429c4bd1ffb2448
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete

Dieses Lernprogramm veranschaulicht, wie verbesserten R-Pakete, die in bereitgestellten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zum Arbeiten mit SQL Server-Daten und skalierbare R-Lösungen unter Verwendung des Servers als computekontext für leistungsstarke big Data-Analysen erstellen.

Sie erfahren, wie einen remote-computekontext erstellen, verschieben Sie Daten zwischen lokalen und Remotecomputern rechenkontexte und R-Code auf einem Remotecomputer mit SQL Server ausführen. Sie erfahren außerdem, analysieren und Zeichnen von Daten, sowohl lokal als auch auf dem Remoteserver sowie zum Erstellen und Bereitstellen von Modellen.

> [!NOTE]
> 
> Dieses Lernprogramm funktioniert speziell mit SQL Server-Daten unter Windows und rechenkontexte in der Datenbank verwendet. Zur Verwendung von R in anderen Kontexten, z. B. Teradata, Linux oder Hadoop, finden Sie diese Lernprogramme für Microsoft R Server: 
> + [Verwenden Sie R-Server mit sparklyr](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [Explore R and ScaleR in 25 Functions (Erkunden von R und ScaleR in 25 Funktionen)](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler)
> + [Erste Schritte mit ScaleR auf Hadoop MapReduce](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + ["Revoscaler" Teradata erste Schritte](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>Übersicht

Um die Flexibilität und Verarbeitungsleistung von ScaleR-Paketen darzustellen, verschieben Sie in diesem Tutorial häufig Daten und tauschen Computekontexte aus.

+ Zuerst werden die Daten aus CSV-Dateien oder XDF-Dateien abgerufen. Sie importieren die Daten mithilfe der Funktionen im RevoScaleR-Paket in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
+ Das Modelltraining und die Bewertung erfolgen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computekontext.
    Sie erstellen neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen mithilfe der **rx** -Funktionen, um die Bewertungsergebnisse zu sichern.
+ Sie erstellen Plots auf dem Server und im lokalen Computekontext.
+ Zum Trainieren des Modells verwenden Sie Daten, die bereits in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank gespeichert sind. Alle Berechnungen erfolgen auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz.
+ Sie extrahieren eine Teilmenge der Daten und speichern sie als XDF-Datei für die erneute Verwendung zur Analyse auf Ihrer lokalen Arbeitsstation.
+ Neue Daten, die bei der Bewertung verwendet werden, werden aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank mithilfe einer ODBC-Verbindung extrahiert. Alle Berechnungen werden auf der lokalen Arbeitsstation ausgeführt.
+ Abschließend führen Sie eine Simulation basierend auf einer benutzerdefinierten R-Funktion aus, indem Sie den Server-Computekontext verwenden.

### <a name="get-started-now"></a>Fangen wir an

In diesem Lernprogramm dauert ca. 75 Minuten, einschließlich nicht einrichten.

1. [Arbeiten Sie mit SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [Fragen Sie ab und ändern Sie die SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [Definieren Sie und verwenden Sie Rechenkontexte](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [Visualisieren von SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [Erstellen Sie R-Modelle](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [Neue Bewertungsdaten](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [Transformieren von Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [Laden von Daten in den Arbeitsspeicher mit rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [Erstellen Sie neue SQL Server-Tabelle mit rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [Führen Sie die Segmentierung Analysen mit RxDataStep aus](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [Analysieren von Daten im lokalen Computekontext;](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [Verschieben von Daten zwischen SQLServer und XDF-Datei](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [Erstellen Sie eine einfache Simulation](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>Zielgruppe

Dieses Tutorial richtet sich an Datenanalysten oder andere Personen, die bereits ein wenig mit R und anderen Data Science-Aufgaben vertraut sind, darunter Durchsuchungsvorgänge, statistische Analysen und Modelloptimierungen.  Allerdings wird der gesamte Code bereitgestellt, dadurch auch, wenn Sie R vertraut sind, können Sie problemlos führen Sie den Code und nachvollziehen, vorausgesetzt, dass Sie die erforderlichen Server- und Clientumgebungen haben.

Sie sollten auch mit [!INCLUDE[tsql](../../includes/tsql-md.md)] Syntax vertraut sein und wissen, wie der Zugriff auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder anderen Tools, z.B. Visual Studio erfolgt.
  
> [!TIP]
> Speichern Sie Ihren R-Arbeitsbereich zwischen den Lektionen, sodass Sie nach einer Unterbrechung problemlos weitermachen können.

### <a name="prerequisites"></a>Erforderliche Komponenten

- **SQL Server mit Unterstützung für R**
  
    Installieren Sie SQL Server 2016, und aktivieren Sie R Services (Datenbankintern). Oder installieren Sie SQL Server-2017 und aktivieren Sie Machine Learning Services, und wählen Sie die Sprache "R". Setup wird beschrieben, wie [SQL Server 2016-Onlinedokumentation](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx).
  
-  **Datenbankberechtigungen**
  
    Für die Durchführung der Abfragen zum Trainieren des Modells benötigen Sie **db_datareader** -Berechtigungen für die Datenbank, in der die Daten gespeichert ist. Zum Ausführen von R benötigen Ihre Benutzer die Berechtigung EXECUTE ANY EXTERNAL SCRIPT.

-   **Data Science-Entwicklungscomputer**
  
    Sie müssen auch die "revoscaler"-Pakete und zugehörige Anbieter in der R-Entwicklungsumgebung installieren. Die einfachste Möglichkeit hierzu ist zum Installieren von Microsoft R-Client oder Microsoft R Server (eigenständig). Weitere Informationen finden Sie unter [Einrichten eines Data Science-Client](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx).
      
    > [!NOTE] 
    > Andere Versionen von Revolution R Enterprise oder Revolution R Open werden nicht unterstützt.
    > 
    > Open Source-Verteilung von R, z. B. R 3.2.2 verwenden, funktionieren nicht in diesem Lernprogramm, da remote rechenkontexte RevoScaleR-Funktionen verwendet werden können.
  
-   **Zusätzliche R-Pakete**
  
    Für dieses Tutorial müssen Sie die folgenden Pakete installieren: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, and **e1071**. Anweisungen sind im Tutorial enthalten.
  
    Alle Pakete müssen an zwei Orten installiert werden: auf dem Computer, die Sie verwenden, für die Entwicklung von R-Projektmappe, und klicken Sie auf dem SQL Server-Computer, in der R-Skripts ausgeführt werden. Bitten Sie einen Administrator, wenn Sie keine Berechtigung zum Installieren von Paketen auf dem Servercomputer. **Installieren Sie die Pakete nicht in einer Benutzerbibliothek.** Es ist wichtig, dass die Pakete in der Bibliothek der R-Paket installiert werden, die von der SQL Server-Instanz verwendet wird.

Weitere Informationen finden Sie unter [erforderlichen Komponenten für Data Science Exemplarische Vorgehensweisen](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).



## <a name="next-step"></a>Nächster Schritt

[Arbeiten Sie mit SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

