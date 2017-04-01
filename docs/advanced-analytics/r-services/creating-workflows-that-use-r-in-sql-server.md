---
title: "Erstellen von Workflows, die R in SQL Server verwenden | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Erstellen von Workflows, die R in SQL Server verwenden
  Eine relationale Datenbank ist eine hochgradig optimierte Technologie für die Bereitstellung von skalierbaren Lösungen für die Transaktion, Verarbeitung, Speicherung und Abfragen von Daten. Allerdings haben bisher R-Lösungen im Allgemeinen verlassen zum Importieren von Daten aus verschiedenen Quellen, häufig im CSV-Format weiter Durchsuchen von Daten und Modellierung ausführen. Solche Methoden sind nicht nur ineffizient, sondern auch unsicher.  
  
 Mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet mehrere Vorteile:  
  
-   Sicherheit der Daten. Die Leistungsfähigkeit von R fällt in die Datenbank, die Quelle der Daten an. Vermeidet unnötig oder unsichere Datentransfer.  
  
-   Geschwindigkeit. Datenbanken sind für satzbasierte Vorgänge optimiert. Wie in-Memory-Tabellen und Einspaltig Datenspeicher weiter steigern Innovationen in Datenbanken Data Science darüber hinaus, da Aggregationen, die besonders schnell erfolgen.  
  
-   Integration. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist der zentrale Punkt von Vorgängen für viele andere Aufgaben und Anwendungen, die Unternehmen nutzen. Bereits mit Daten in der Datenbank wird sichergestellt, dass die Daten konsistent und auf dem neuesten Stand sind. Anstatt Verarbeiten von Daten in R Sie beruhen, einschließlich Enterprise-Datenpipelines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Azure Data Factory. Von Ergebnissen oder Analysen Reporting ist einfach über Power BI oder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Durch die Verwendung der richtigen Kombination von SQL und R für verschiedene Datenverarbeitungstasks und analytische Tasks, können Datenanalysten und Entwickler produktiver sein. In diesem Abschnitt wird beschrieben, wie Sie R mit anderen Unternehmenslösungen für die Datentransformation, Analyse und Berichterstattung integrieren können.  
  
##  <a name="bkmk_ssis"></a> Erstellen von effizienten Workflows, die R und die Datenbank umfassen  
 Data Science-Workflows sind hoch iterativ und umfassen eine Menge Transformation von Daten, einschließlich Skalierung, Aggregationen, die Berechnung der Wahrscheinlichkeiten, sowie das Umbenennen und Zusammenführen von Attributen. Datenanalysten sind daran gewöhnt, wie viele dieser Aufgaben in R, Python oder einer anderen Sprache. Allerdings erfordert die Ausführung von solche Workflows auf Unternehmensdaten, nahtlose Integration mit ETL-Tools und Prozesse.  
  
 Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ermöglicht es Ihnen, komplexe Operationen in R über Transact-SQL und gespeicherte Prozeduren ausführen R-spezifische Aufgaben mit vorhandenen ETL-Prozesse ohne minimale erneute integriert werden kann. Stattdessen als eine Kette von Speicher-Ntensive Aufgaben in R ausführen, die Vorbereitung der Daten optimiert werden mit den effizientesten Tools wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Sie können z. B. R mit kombinieren [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in folgenden Szenarien:  
  
-   Verwendung [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Aufgaben zum Erstellen der erforderlichen Objekte in der SQL-Datenbank  
  
-   Verwenden von bedingter Verzweigung, um Computekontext für R-Aufträge zu wechseln  
  
-   Ausführung von R-Aufträgen, die ihre Daten selbst generieren  
  
-   Verwendung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrufen, ein R-Skript in einer Text-Variablen gespeichert  
  
### Beispiele und Ressourcen  
 [Nehmen Sie Machine Learning Projekt mithilfe von SQL Server 2016 SSIS und R-Dienste in Betrieb](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  
  
 In diesem Blogbeitrag lernen Sie Gewusst wie:  
  
-   Verwenden Sie zum Generieren von Daten und speichern Sie ihn in R im Task SQL ausführen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Verwenden einer gespeicherten Prozedur zum Trainieren eines R-Modells, und speichern es in der Datenbank  
  
-   Führen Sie die Bewertung auf das Modell mit dem Skripttask und der Task SQL ausführen  
  
##  <a name="bkmk_ssrs"></a> Erstellen von Visualisierungen, die Tools für R und Unternehmensberichte umfassen  
 Obwohl R Diagramme und interessante Visualisierungen erstellen kann, ist es nicht gut mit externen Datenquellen integriert, was bedeutet, dass jedes Diagramm oder jeder Graph einzeln erstellt werden muss. Gemeinsame Nutzung kann auch schwierig sein.  
  
 Mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], Sie können komplexe Vorgänge ausführen, in R über [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozeduren, die von einer Vielzahl von Enterprise reporting Tools, einschließlich problemlos genutzt werden können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und Power BI.  
  
-   Visualisieren von Graphics-Objekten, die von einem R-Skript zurückgegeben   
    Verwendung [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Verwenden Sie die Tabelle in Power BI  
  
## Beispiele und Ressourcen  
 [R-Grafikgerät für Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/)  
  
 CodePlex-Projekt enthält der Code können Sie ein benutzerdefiniertes Berichtselement erstellen, stellt die Grafikausgabe r als Bild die verwendet werden können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Berichte.  Verwenden Sie das benutzerdefinierte Berichtselement, können Sie folgende Aktionen ausführen:  
  
-   Veröffentlichen von Diagrammen und mit dem R-Grafikgerät zu erstellte Plots [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Dashboards  
  
-   Übergeben Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Parameter für R Plots  
  
> [!NOTE]  
>  Beachten Sie, dass der Code, der dem R-Grafikgerät für Reporting Services unterstützt sowohl auf dem Reporting Services-Server als auch in Visual Studio installiert werden muss. Manuelle Kompilierung und Konfiguration ist ebenfalls erforderlich.  
  
  