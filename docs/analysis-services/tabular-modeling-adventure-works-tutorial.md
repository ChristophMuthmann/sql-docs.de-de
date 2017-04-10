---
title: "Tabellenmodellierung (Adventure Works-Lernprogramm) | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
keywords: 
  - "Analysis Services"
  - "tabellarisches Modell"
  - "Lernprogramm"
  - "SSAS"
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# Tabellenmodellierung (Adventure Works-Lernprogramm)
Dieses Tutorial enthält Lektionen zum Erstellen eines tabellarischen [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services-Modells unter Verwendung von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
  
## Ihre Lernziele  
Im Rahmen dieses Lernprogramms führen Sie die folgenden Aufgaben aus:  
  
-   Erstellen eines neuen Tabellenmodellprojekts in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Importieren von Daten von einer relationalen SQL Server-Datenbank in ein Tabellenmodellprojekt.  
  
-   Erstellen und Verwalten von Beziehungen zwischen Tabellen im Modell.  
  
-   Erstellen und Verwalten von Berechnungen, Measures und Key Performance Indicators, mit denen Benutzer Modelldaten analysieren können.  
  
-   Erstellen und Verwalten von Perspektiven und Hierarchien, mit denen Benutzer durch die Bereitstellung von geschäfts- und anwendungsspezifischen Blickpunkten einfacher Modelldaten durchsuchen können.  
  
-   Erstellen von Partitionen, mit denen sich Tabellendaten in kleinere logische Teile aufteilen lassen, die unabhängig von anderen Partitionen verarbeitet werden können.  
  
-   Sichern von Modellobjekten und -daten durch die Erstellung von Rollen mit Benutzerelementen.  
  
-   Bereitstellen eines tabellarischen Models für einen Sandkasten oder eine Produktionsinstanz von Analysis Services im tabellarischen Modus.  
  
## Szenario  
Dieses Lernprogramm basiert auf [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], einem fiktiven Unternehmen. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ist ein großes, multinationales Herstellungsunternehmen, das Fahrräder aus Metall und Verbundwerkstoffen für kommerzielle Märkte in Nordamerika, Europa und Asien produziert und vertreibt. Die Zentrale von [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] befindet sich in Bothell, Washington (USA), wo das Unternehmen 500 Arbeiter beschäftigt. Zusätzlich beschäftigt [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] eine Reihe von regionalen Verkaufsteams für die gesamte Marktbasis.  
  
Um die Datenanalyseanforderungen von Verkaufs- und Marketingteams sowie des Senior Managements besser zu unterstützen, werden Sie damit beauftragt, ein Tabellenmodell für Benutzer zu erstellen, um Internetumsatzdaten in der AdventureWorksDW-Beispieldatenbank zu analysieren.  
  
Um das Lernprogramm und das Tabellenmodell für die Adventure Works-Internetverkäufe abzuschließen, ist eine Reihe von Lektionen auszuführen. Jede Lektion umfasst eine Reihe von Aufgaben, und das Abschließen jeder Aufgabe ist zum Abschließen der jeweiligen Lektion erforderlich. In einer bestimmten Lektion können mehrere Aufgaben enthalten sein, die zu einem ähnlichen Ergebnis führen. Die Ausführung der jeweiligen Aufgabe unterscheidet sich jedoch leicht. Dadurch soll vermittelt werden, dass oftmals mehrere Möglichkeiten zum Ausführen einer bestimmten Aufgabe bestehen. Zudem soll dies für Sie eine Herausforderung darstellen, indem Sie in vorherigen Aufgaben erlernte Fähigkeiten einsetzen.  
  
In den Lektionen werden Sie durch die Erstellung eines grundlegenden tabellarischen Modells, das im InMemory-Modus ausgeführt wird, unter Verwendung zahlreicher in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] enthaltener Funktionen geführt. Da jede Lektion auf der jeweils vorherigen Lektion aufbaut, sollten Sie die Lektionen in der entsprechenden Reihenfolge bearbeiten. Nach dem Abschließen aller Lektionen haben Sie das Beispieltabellenmodell für die Adventure Works-Internetverkäufe auf einem Analysis Services-Server erstellt und bereitgestellt.  
  
Dieses Lernprogramm enthält keine Lektionen oder Informationen zum Verwalten einer Datenbank für Tabellenmodelle unter Verwendung von SQL Server Management Studio oder das Verwenden einer Berichterstellungs-Clientanwendung zur Herstellung einer Verbindung mit einem bereitgestellten Modell zum Durchsuchen von Modelldaten.  
  
## Erforderliche Komponenten  
Um dieses Lernprogramm abzuschließen, müssen die folgenden Komponenten installiert sein:  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Im tabellarischen Modus ausgeführte Analysis Services-Instanz.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. [Laden Sie die neueste Version herunter.](https://msdn.microsoft.com/library/mt204009.aspx)  
  
-   Adventure Works DW 2014-Beispieldatenbank. Diese Beispieldatenbank beinhaltet die für das Abschließen des Lernprogramms notwendigen Daten. Informationen zum Herunterladen der Beispieldatenbank finden Sie unter [http://go.microsoft.com/fwlink/?LinkID=335807](http://go.microsoft.com/fwlink/?LinkID=335807).  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 oder höher (zur Verwendung mit der Funktion „In Excel analysieren“ in Lektion 11).  
  
## Lektionen  
Dieses Tutorial umfasst die folgenden Lektionen:  
  
|Lektion|Für den Abschluss voraussichtlich benötigte Zeit|  
|----------|------------------------------|  
|[Lektion 1: Erstellen eines neuen Tabellenmodellprojekts](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 Minuten|  
|[Lektion 2: Hinzufügen von Daten](../analysis-services/lesson-2-add-data.md)|20 Minuten|  
|[Lektion 3: Umbenennen von Spalten](../analysis-services/lesson-3-rename-columns.md)|20 Minuten|  
|[Lektion 4: Markieren als Datumstabelle](../analysis-services/lesson-4-mark-as-date-table.md)|3 Minuten|  
|[Lektion 5: Erstellen von Beziehungen](../analysis-services/lesson-5-create-relationships.md)|10 Minuten|  
|[Lektion 6: Erstellen von berechneten Spalten](../analysis-services/lesson-6-create-calculated-columns.md)|15 Minuten|  
|[Lektion 7: Erstellen von Measures](../analysis-services/lesson-7-create-measures.md)|30 Minuten|  
|[Lektion 8: Erstellen von Leistungskennzahlen](../analysis-services/lesson-8-create-key-performance-indicators.md)|15 Minuten|  
|[Lektion 9: Erstellen von Perspektiven](../Topic/Lesson%209:%20Create%20Perspectives.md)|5 Minuten|  
|[Lektion 10: Erstellen von Hierarchien](../analysis-services/lesson-10-create-hierarchies.md)|20 Minuten|  
|[Lektion 11: Erstellen von Partitionen](../analysis-services/lesson-11-create-partitions.md)|15 Minuten|  
|[Lektion 12: Erstellen von Rollen](../analysis-services/lesson-12-create-roles.md)|15 Minuten|  
|[Lektion 13: Analysieren in Excel](../analysis-services/lesson-13-analyze-in-excel.md)|20 Minuten|  
|[Lektion 14: Bereitstellen](../analysis-services/lesson-14-deploy.md)|5 Minuten|  
  
## Ergänzende Lektionen  
Dieses Tutorial umfasst außerdem [ergänzende Lektionen](../Topic/Supplemental%20Lessons.md). Die Themen in diesem Abschnitt sind nicht erforderlich, um das Lernprogramm abzuschließen, aber sie können das Verständnis der erweiterten Funktionen zum Erstellen eines Tabellenmodells erleichtern.  
  
|Lektion|Für den Abschluss voraussichtlich benötigte Zeit|  
|----------|------------------------------|  
|[Implementieren von dynamischer Sicherheit mithilfe von Zeilenfiltern](../analysis-services/implement-dynamic-security-by-using-row-filters.md)|30 Minuten|  
|[Konfigurieren von Berichterstellungseigenschaften für Power View-Berichte](../analysis-services/configure-reporting-properties-for-power-view-reports.md)|30 Minuten|  
  
## Nächster Schritt  
Um das Tutorial zu starten, gehen Sie zur ersten Lektion über: [Lektion 1: Erstellen eines neuen Tabellenmodellprojekts](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
  
  
