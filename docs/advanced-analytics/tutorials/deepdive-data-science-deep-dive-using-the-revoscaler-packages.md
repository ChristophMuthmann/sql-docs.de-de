---
title: 'Data Science-vertiefenden: verwenden die "revoscaler"-Pakete mit SQL Server | Microsoft Docs'
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 003434a055ab73afb288ea5801130ce1c06aa9c5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages-with-sql-server"></a>Data Science-vertiefenden: verwenden die "revoscaler"-Pakete mit SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieses Lernprogramm veranschaulicht, wie verbesserten R-Pakete, die in bereitgestellten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zum Arbeiten mit SQL Server-Daten und skalierbare R-Lösungen unter Verwendung des Servers als computekontext für leistungsstarke big Data-Analysen erstellen.

Verschieben von Daten zwischen lokalen und Remotecomputern rechenkontexte erfahren Sie, wie einen remote computekontext erstellt, und führen Sie R-Code auf einem Remotecomputer mit SQL Server. Sie erfahren außerdem, wie analysieren und Zeichnen von Daten, sowohl lokal als auch auf dem Remoteserver sowie zum Erstellen und Bereitstellen von Modellen.

> [!NOTE]
> 
> Dieses Lernprogramm funktioniert speziell mit SQL Server-Daten unter Windows und rechenkontexte in der Datenbank verwendet. Zur Verwendung von R in anderen Kontexten, z. B. Teradata, Linux oder Hadoop, finden Sie diese Lernprogramme für Microsoft R Server: 
> + [Verwenden Sie R-Server mit sparklyr](https://docs.microsoft.com/machine-learning-server/r/tutorial-sparklyr-revoscaler)
> + [Explore R and ScaleR in 25 Functions (Erkunden von R und ScaleR in 25 Funktionen)](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)
> + [Erste Schritte mit ScaleR auf Hadoop MapReduce](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-hadoop)

## <a name="overview"></a>Übersicht

Um die Leistungsfähigkeit Flexibilität und Verarbeitung des Pakets "revoscaler" in diesem Lernprogramm auftreten verschieben Sie Daten und Austauschen Kontexten häufig berechnen. Zur Veranschaulichung wird sind hier einige der Aufgaben in diesem Lernprogramm:

+ Zuerst werden die Daten aus CSV-Dateien oder XDF-Dateien abgerufen. Importieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit den Funktionen in die RevoScaleR-Paket.
+ Modell trainieren und Bewertung erfolgt mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computekontext. 
+ Verwenden Sie die RevoScaleR-Funktionen zum Erstellen neuer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabellen, um die bewerteten Ergebnisse zu speichern.
+ Erstellen von Darstellungen, die sowohl auf dem Server und in der lokalen computekontext.
+ Trainieren Sie ein Modell auf Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank, Ausführen von R in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.
+ Extrahieren Sie eine Teilmenge der Daten zu und speichern Sie sie als eine XDF-Datei für die erneute Verwendung in Analysen auf der lokalen Arbeitsstation.
+ Rufen Sie neue Daten für die Bewertung, durch Öffnen des ODBC-Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank. Bewertung erfolgt auf der lokalen Arbeitsstation.
+ Erstellen Sie eine benutzerdefinierte R-Funktion, und führen Sie sie im Server-computekontext eine Simulation ausführen.

### <a name="article-list-and-time-required"></a>Artikelliste und die erforderliche Zeit

In diesem Lernprogramm dauert ca. 75 Minuten, einschließlich nicht einrichten.

1. [Arbeiten Sie mit SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [Abfragen und Ändern der SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [Definieren und Verwenden von Rechenkontexten](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [Visualisieren von SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [Erstellen Sie R-Modelle](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [Neue Bewertungsdaten](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [Umwandeln von Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [Laden von Daten in den Arbeitsspeicher mit rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [Erstellen Sie neue SQL Server-Tabellen mit rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [Blockweises Analysieren mithilfe von rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [Analysieren von Daten in einem lokalen Rechenkontext](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [Verschieben von Daten von SQL Server mithilfe von XDF-Dateien](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [Erstellen einer einfachen Simulation](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>Zielgruppe

Dieses Lernprogramm richtet sich für Datenanalysten oder für Personen, die bereits mit R, und klicken Sie mit Data Science-Aufgaben wie z. B. Zusammenfassungen und Modellerstellung etwas vertraut sind.  Allerdings wird der gesamte Code bereitgestellt, selbst wenn Sie R vertraut sind, führen Sie den Code und nachvollziehen, vorausgesetzt, dass Sie die erforderlichen Server- und Clientumgebungen haben.

Sie sollten auch mit vertraut sein [!INCLUDE[tsql](../../includes/tsql-md.md)] Syntax und wissen, wie den Zugriff auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank mithilfe von Tools wie den folgenden:

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Datenbanktools in Visual Studio 
+ Die kostenlose [Mssql-Erweiterung für Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).
  
> [!TIP]
> Speichern Sie Ihren R-Arbeitsbereich zwischen den Lektionen, sodass Sie nach einer Unterbrechung problemlos weitermachen können.

### <a name="prerequisites"></a>Erforderliche Komponenten

- **SQL Server mit Unterstützung für R**
  
    Installieren Sie SQL Server 2016, und aktivieren Sie R Services (Datenbankintern). Oder installieren Sie SQL Server-2017 und aktivieren Sie Machine Learning Services, und wählen Sie die Sprache "R".
  
-  **Datenbankberechtigungen**
  
    Für die Durchführung der Abfragen zum Trainieren des Modells benötigen Sie **db_datareader** -Berechtigungen für die Datenbank, in der die Daten gespeichert ist. Zum Ausführen von R benötigen Ihre Benutzer die Berechtigung EXECUTE ANY EXTERNAL SCRIPT.

-   **Data Science-Entwicklungscomputer**
  
    Sie müssen auf dem Computer, der als R-Entwicklungsumgebung verwendet die "revoscaler"-Pakete und zugehörige Anbieter installieren. Die einfachste Möglichkeit hierzu ist Microsoft R-Client installiert Microsoft R Server (eigenständig) oder Machine Learning-Server (eigenständig). 
      
    > [!NOTE] 
    > Andere Versionen von Revolution R Enterprise oder Revolution R Open werden nicht unterstützt.
    > 
    > Open Source-Verteilung von R kann nicht in diesem Lernprogramm verwendet werden, da nur die RevoScaleR-Funktionen remote rechenkontexte verwenden können.
  
-   **Zusätzliche R-Pakete**
  
    In diesem Lernprogramm, installieren Sie die folgenden Pakete: **Dplyr**, **ggplot2**, **Ggthemes**, **reshape2**, und **e1071** . Anweisungen sind im Tutorial enthalten.
  
    Alle Pakete müssen an zwei Orten installiert werden: auf dem Computer, die Sie verwenden, für die Entwicklung von R-Projektmappe, und klicken Sie auf dem SQL Server-Computer, auf dem R-Skripts ausgeführt werden. Bitten Sie einen Administrator, wenn Sie keine Berechtigung zum Installieren von Paketen auf dem Servercomputer. 
    
    **Installieren Sie die Pakete nicht in einer Benutzerbibliothek.** In der R-Paket-Bibliothek, die von der SQL Server-Instanz verwendet wird, müssen die Pakete installiert werden.

Weitere Informationen finden Sie unter [erforderlichen Komponenten für Data Science Exemplarische Vorgehensweisen](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

## <a name="next-step"></a>Nächster Schritt

[Arbeiten Sie mit SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

