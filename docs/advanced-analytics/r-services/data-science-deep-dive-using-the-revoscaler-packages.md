---
title: "Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete | Microsoft Docs"
ms.custom: ""
ms.date: "09/27/2016"
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
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete
Dieses Tutorial bietet eine Einführung in erweiterte R-Pakete, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bereitgestellt werden. Lernen Sie, wie Sie das skalierbare Enterprise-Framework für die Ausführung von R-Paketen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwenden können.   Mithilfe dieser skalierbaren R-Funktionen können Datenanalysten benutzerdefinierte R-Lösungen für lokale oder Serverkontexte erstellen, um leistungsstarke Analysen großer Datenmengen („Big Data“) zu ermöglichen.  
  
In diesem Tutorial erfahren Sie, wie man Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Ihrer R-Arbeitsstation verschiebt, Daten analysiert und zeichnet, sowie Modelle erstellt und bereitstellt.  
    
## Übersicht 
 
Um die Flexibilität und Verarbeitungsleistung von ScaleR-Paketen darzustellen, verschieben Sie in diesem Tutorial häufig Daten und tauschen Computekontexte aus.

+ Zuerst werden die Daten aus CSV-Dateien oder XDF-Dateien abgerufen. Sie importieren die Daten mithilfe der Funktionen im RevoScaleR-Paket in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
+ Das Modelltraining und die Bewertung erfolgen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computekontext. 
    Sie erstellen neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabellen mithilfe der **rx**-Funktionen, um die Bewertungsergebnisse zu sichern.    
+ Sie erstellen Plots auf dem Server und im lokalen Computekontext.  
+ Zum Trainieren des Modells verwenden Sie Daten, die bereits in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank gespeichert sind. Alle Berechnungen erfolgen auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.    
+ Sie extrahieren eine Teilmenge der Daten und speichern sie als XDF-Datei für die erneute Verwendung zur Analyse auf Ihrer lokalen Arbeitsstation.    
+ Neue Daten, die bei der Bewertung verwendet werden, werden aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank mithilfe einer ODBC-Verbindung extrahiert. Alle Berechnungen werden auf der lokalen Arbeitsstation ausgeführt. 
+ Abschließend führen Sie eine Simulation basierend auf einer benutzerdefinierten R-Funktion aus, indem Sie den Server-Computekontext verwenden.

### Fangen wir an  

Dieses Tutorial dauert etwa eine Stunde, ohne Installation.  

-   [Lektion 1: Arbeiten mit SQL Server-Daten mithilfe von R](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
-   [Lektion 2: Erstellen und Ausführen von R-Skripts](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
-   [Lektion 3: Umwandeln von Daten mithilfe von R](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
-   [Lektion 4: Analysieren von Daten in einem lokalen Computekontext](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
-   [Lektion 5: Erstellen einer einfachen Simulation](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  

      
### Zielgruppe  
  
Dieses Tutorial richtet sich an Datenanalysten oder andere Personen, die bereits ein wenig mit R und anderen Data Science-Aufgaben vertraut sind, darunter Durchsuchungsvorgänge, statistische Analysen und Modelloptimierungen.  Allerdings wird der gesamte Code bereitgestellt, damit Sie ihn ausführen und verfolgen können, vorausgesetzt Sie verfügen über die erforderliche Client-Serverumgebung.  
  
Sie sollten auch mit [!INCLUDE[tsql](../../includes/tsql-md.md)] Syntax vertraut sein und wissen, wie der Zugriff auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder anderen Tools, z.B. Visual Studio erfolgt.  
  
> [!TIP]  
> Speichern Sie Ihren R-Arbeitsbereich zwischen den Lektionen, sodass Sie nach einer Unterbrechung problemlos weitermachen können.  
  
### Erforderliche Komponenten  
  
-   **Datenbankserver mit Unterstützung für R**  
  
    Installieren Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], und aktivieren Sie SQL Server R Services (datenbankintern). Dieser Prozess wird hier beschrieben: [Onlinedokumentation zu SQL Server 2016](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx).  
  
-   **Datenbankberechtigungen**  
  
    Für die Durchführung der Abfragen zum Trainieren des Modells benötigen Sie **db_datareader**-Berechtigungen für die Datenbank, in der die Daten gespeichert ist.  
  
  
-   **Data Science-Arbeitsstation**  
  
    Sie müssen die RevoScaleR-Pakete installieren. Die einfachste Möglichkeit hierzu ist die Installation von Microsoft R Server (eigenständig) oder Microsoft R Client. Weitere Informationen finden Sie unter [Einrichten eines Data Science-Client](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx).
      
    > [!NOTE] 
    > Andere Versionen von Revolution R Enterprise oder Revolution R Open werden nicht unterstützt. 
    > 
    > Eine Open-Source-Distribution von R, zum Beispiel R 3.2.2, funktioniert in diesem Tutorial nicht, da nur die ScaleR-Funktion einen Remotecomputekontext verwenden kann. 
  
-   **Zusätzliche R-Pakete**  
  
    Für dieses Tutorial müssen Sie die folgenden Pakete installieren: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, and **e1071**. Anweisungen sind im Tutorial enthalten.  
  
    Alle Pakete müssen ebenfalls auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz installiert werden, auf der die Schulung ausgeführt wird. Es ist wichtig, dass die Pakete in der R-Paketbibliothek von SQL Server installiert werden. **Installieren Sie die Pakete nicht in einer Benutzerbibliothek.** Wenn Sie nicht über die Berechtigung zum Installieren von Paketen in diesem Ordner verfügen, bitten Sie einen Datenbankadministrator, die Pakete hinzuzufügen.   
  
Weitere Informationen finden Sie unter [Voraussetzungen für die exemplarischen Vorgehensweisen für Data Science &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md).  
  
## Datenstrategien für Distributed R-Lösungen
    
Im Allgemeinen, bevor Sie beginnen, R-Skripts in Ihrer lokale Entwicklungsumgebung zu schreiben und auszuführen, sollten Sie sich immer kurz Zeit nehmen, die Verwendung Ihrer Daten zu planen und zu bestimmen, wo die einzelnen Teile der Lösung für eine optimale Leistung ausgeführt werden.  

In diesem Tutorial machen Sie sich mit den leistungsstarken Funktionen zum Analysieren von Daten, dem Erstellen von Modellen und dem Erstellen von Plots, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten sind, vertraut. Wir werden diese Funktionen in der Regel als ScaleR oder Microsoft R bezeichnen, um diese von Funktionen zu unterscheiden, die aus anderen Open-Source-R-Paketen stammen. Weitere Informationen über die Unterschiede zwischen Microsoft R und Open-Source-R finden Sie im [Getting Started guide (Handbuch Erste Schritte)](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#microsoft-r-products). 

Ein entscheidender Vorteil der ScaleR-Funktionen ist, dass sie die Verwendung lokaler oder serverunterstützter *Datenquellen* und *Lokal- oder Remoteomputekontexte* unterstützen.  Daher sollten Sie beim Durcharbeiten dieses Tutorials überlegen, welche Datenstrategien Sie für Ihre eigenen Lösungen anwenden könnten.
  
-   **Welche Art Analyse möchten Sie durchführen?** Ist es nur für Ihre Verwendung, oder wollen Sie die Modelle, Ergebnisse oder Diagramme mit anderen teilen?
 
    In diesem Tutorial lernen Sie, wie man Ergebnisse zwischen Ihrer Entwicklungsumgebung und dem Server hin- und herschiebt, um das Teilen und Analysieren zu vereinfachen. 
  
-   **Unterstützt das R-Paket, das Sie brauchen, eine Remoteausführung?** Alle Funktionen in ScaleR-Paketen, bereitgestellt von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], können in Remotecomputekontexten ausgeführt werden und können möglicherweise eine parallele Ausführung bieten. Im Gegensatz dazu benötigen Funktionen in Paketen von Drittanbietern möglicherweise zusätzliche Ressourcen für die Singlethread-Ausführung. 
    
    In diesem Tutorial lernen Sie, zwischen lokalen und Remotecomputekontexten zu wechseln, um bei Bedarf Server-Ressourcen zu nutzen. Außerdem erfahren Sie, wie man R-Standardfunktionen mit *rxExec* umschließt, um die Remoteausführung beliebiger R-Funktionen zu unterstützen.
    
  
-   **Wo sind die Daten und was sind die Merkmale?**  Falls Ihre Daten lokal vorliegen, müssen Sie sich entscheiden, ob Sie alle neuen Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hochladen oder lokal trainieren und nur das Modell in der Datenbank speichern. Wenn Sie sie aber für den Produktivbetrieb bereitstellen, kann es nötig sein, von Enterprise-Daten zu trainieren und ETL-Prozesse zu nutzen, um die Daten zu bereinigen und zu laden.  
  
-   Ähnliche Fragen beziehen sich auf die Bewertungsdaten. Erstellen Sie die Datenpipeline zum Bewerten von Daten auf Ihrer Arbeitsstation oder werden Sie Enterprise-Datenquellen verwenden? Sollten die Datenbereinigung und die Vorbereitung als Teil der ETL-Prozesse erfolgen oder führen Sie ein einmaliges Experiment durch?  

    In diesem Tutorial lernen Sie, wie Sie Daten effizient und sicher zwischen Ihrer lokalen R-Umgebung und SQL Server verschieben. 
  
-   **Welchen Computekontext sollten Sie verwenden?** Möglicherweise möchten Sie Ihr Modell lokal an Stichprobendaten trainieren und anschließend Serverdaten für die Tests und Produktion verwenden.

    In diesem Tutorial lernen Sie, wie man Daten zwischen SQL Server und R mithilfe von R verschiebt. Außerdem erfahren Sie, wie man mithilfe von XDF-Dateien mit Daten arbeitet und wie man Daten mithilfe der ScaleR-Funktion in Segmenten verarbeitet.  
  
 
  
## Nächster Schritt  
[Lektion 1: Work with SQL Server Data using R &#40;Data Science Deep Dive&#41; (Arbeiten mit SQL Server-Daten mithilfe von R (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
  
  
