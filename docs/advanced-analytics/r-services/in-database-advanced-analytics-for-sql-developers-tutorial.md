---
title: "Datenbankinterne Advanced Analytics f&#252;r SQL-Entwickler (Tutorial) | Microsoft Docs"
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
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Datenbankinterne Advanced Analytics f&#252;r SQL-Entwickler (Tutorial)
Mit dieser exemplarischen Vorgehensweise sollen SQL-Programmierer eigene Erfahrungen im Erstellen einer erweiterten Analyselösung mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] sammeln. In dieser exemplarischen Vorgehensweise erfahren Sie, wie Sie R durch das Wrapping von R-Code in gespeicherten Prozeduren in eine Anwendung oder eine BI-Lösung integrieren.  
  
## Übersicht  
Das Erstellen einer Ende-zu-Ende-Lösung besteht in der Regel aus Abrufen und Bereinigen von Daten, Durchsuchen von Daten und Verarbeiten von Funktionen, Modelltraining und Optimieren und schließlich Bereitstellung des Modells in der Produktion. Entwicklung und Tests von R-Code wird am besten in einer Umgebung durchgeführt, die für R vorgesehen ist, z.B. RStudio oder [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Nachdem die Lösung erstellt wurde, können Sie sie jedoch problemlos für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [!INCLUDE[tsql](../../includes/tsql-md.md)]-gespeicherten Prozeduren in der vertrauten Umgebung von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] bereitstellen.  
  
Daher gehen wir in dieser exemplarischen Vorgehensweise davon aus, dass der gesamte für die Lösung erforderliche R-Code übergeben worden ist und Sie sich auf die Erstellung und Bereitstellung einer erweiterten analytischen Lösung konzentrieren, die bereits in R codiert wurde.  
  
-   [Schritt 1: Herunterladen der Beispieldaten](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md).    Laden Sie das Beispieldataset und die Beispiel-SQL-Skriptdateien auf einen lokalen Computer herunter.  
  
-   [Schritt 2: Importieren von Daten zu SQL Server mithilfe von PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md).  Führen Sie ein PowerShell-Skript aus, das eine Datenbank und eine Tabelle auf der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz erstellt und die Beispieldaten in die Tabelle lädt.  
  
-   [Schritt 3: Untersuchen und Visualisieren von Daten](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md).   Führen Sie grundlegendes Durchsuchen und Visualisieren von Daten durch, indem Sie R-Pakete und Funktionen von [!INCLUDE[tsql](../../includes/tsql-md.md)]-gespeicherten Prozeduren aufrufen.  
  
-   [Schritt 4: Erstellen von Datenfunktionen mit T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md).  Erstellen Sie neue Features mit benutzerdefinierten SQL-Funktionen.  
  
-   [Schritt 5: Trainieren und Speichern eines Modells mit T-SQL](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md).  Erstellen und speichern Sie das Machine Learning-Modell mithilfe von gespeicherten Prozeduren.  
  
-   [Schritt 6: Operationalisieren des Modells](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md).  Nachdem das Modell in der Datenbank gespeichert wurde, rufen Sie das Modell für die Vorhersage von [!INCLUDE[tsql](../../includes/tsql-md.md)] mit gespeicherten Prozeduren auf.  
  
> [!NOTE]  
> Es wird empfohlen, dass Sie nicht [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden, um R-Code zu schreiben. Wenn der R-Code, den Sie in einer gespeicherten Prozedur einbetten, Probleme aufweist, lässt sich aus den Informationen, die von der gespeicherten Prozedur zurückgegeben werden, in der Regel nicht die Ursache des Fehlers erkennen.   
>   
> Für das Debuggen empfehlen wir Tools wie RStudio oder [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Die in diesem Tutorial bereitgestellten R-Skripts wurden bereits mit herkömmlichen R-Tools entwickelt und debuggt.  
>   
> Wenn Sie lernen möchten, R-Skripts zu entwickeln, die in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ausgeführt werden können, finden Sie dies in diesem Tutorial: [Exemplarische Data Science-Ende-zu-Ende-Vorgehensweise](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md))  
  
### Szenario  
In dieser exemplarischen Vorgehensweise wird das bekannte NYC Taxi-Dataset verwendet. Dieses öffentliche Dataset enthält 20 GB komprimierter CSV-Dateien (~ 48 GB unkomprimiert), die die Details von mehr als 173 Millionen einzelnen Taxifahrten im Jahr 2013 umfassen, samt den pro Fahrt bezahlten Fahrpreisen. Um diese exemplarische Vorgehensweise einfach und schnell zu machen, haben wir einen repräsentativen Querschnitt der Daten erstellt: 1 % der Daten, oder 1.703.957 Zeilen und 23 Spalten. In dieser exemplarischen Vorgehensweise verwenden Sie diese Daten zur Erstellung eines binären Klassifizierungsmodells, das voraussagt, ob bei einer bestimmten Fahrt wahrscheinlich Trinkgeld gegeben wird oder nicht, basierend auf den Spalten, wie Tag, Entfernung und Einstiegsort.  
  
  
### Anforderungen  
Diese exemplarische Vorgehensweise ist für Benutzer gedacht, die bereits mit grundlegenden Datenbank-Vorgängen vertraut sind, z.B. Erstellen von Datenbanken und Tabellen, Importieren von Daten in Tabellen und Erstellen von SQL-Abfragen. Der gesamte R-Code wird bereitgestellt, damit keine R-Entwicklungsumgebung erforderlich ist. Ein erfahrener SQL-Programmierer sollte in der Lage sein, diese exemplarische Vorgehensweise mit [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder durch Ausführen der bereitgestellten PowerShell-Skripts abzuschließen.  
  
Vor Beginn der exemplarischen Vorgehensweise müssen Sie jedoch diese Vorbereitungen treffen:  
  
-   Verbinden mit einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz mit SQL Server R Services aktiviert (CTP 3 oder höher erforderlich). Weitere Informationen finden Sie bei den Installationshinweisen: [Einrichten von SQL Server R Services (datenbankintern)](https://msdn.microsoft.com/library/mt696069.aspx)  
  
 -   Die Anmeldung, die Sie für diese exemplarische Vorgehensweise verwenden, muss über Berechtigungen zum Erstellen von Datenbanken und anderer Objekte, zum Hochladen von Daten, Auswählen von Daten und Ausführen von gespeicherten Prozeduren verfügen.  
  
## Nächster Schritt  
[Schritt 1: Herunterladen der Beispieldateien](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## Siehe auch  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  
