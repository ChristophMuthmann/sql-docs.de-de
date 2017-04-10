---
title: "Operationalisieren Ihres R-Codes | Microsoft Docs"
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
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Operationalisieren Ihres R-Codes
  Datenbankentwickler stehen vor der Aufgabe, zahlreiche Technologien integrieren und die Ergebnisse zusammenführen zu müssen, sodass diese im gesamten Unternehmen gemeinsam genutzt werden können. Ein Datenbankentwickler arbeitet zusammen mit Anwendungsentwicklern, SQL-Entwicklern und Data Scientists am Entwurf von Lösungen, an Empfehlungen für Datenverwaltungsmethoden und der Gestaltung und Bereitstellung von Lösungen. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet viele Vorteile für Entwickler, die mit Datenanalysten arbeiten.  
  
-   **Interagieren mit R-Skripts, die mit [!INCLUDE[tsql](../../includes/tsql-md.md)].** Anwendung und Datenbank-Entwicklern sowie Analysten, die Erstellen von Berichten, können ein R-Skript durch Aufrufen von gespeicherten Systemprozeduren aufrufen.  
  
     Weitere Informationen zur grundlegenden Syntax finden Sie unter [Sp_execute_external_script & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) und [mit R-Code in T-SQL-](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md).  
 
    Ein erweitertes Beispiel zum R operationalisieren von code mithilfe von gespeicherten Prozeduren, finden Sie unter [In der Datenbank-Analysen für SQL-Entwickler](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md).
  
     Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch bedeutet, dass Sie R ausführen können Skripts, die [!INCLUDE[tsql](../../includes/tsql-md.md)] und die Ergebnisse in der Anwendung einbetten. Sie können z. B. Erstellen einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Bericht führt ein R Skript und dann die Elemente zusammen mit den Vorhersagen des Berichts anzuzeigen.  
  
-   **Leistung und Skalierung.** Obwohl die open-Source-R-Sprache begrenzt ist bekannt ist, das Paket RevoScaleR APIs von bereitgestellten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Arbeiten mit großen Datasets und Multi-threaded, Multi-Core, mit mehreren Prozessen in der Datenbank Berechnungen profitieren können.  
  
     Wenn Ihre R-Lösung komplexe Aggregationen verwendet oder große Datasets enthält, können Sie die hocheffizienten In-Memory Aggregationen und den Columnstore-Index von SQL nutzen und den R-Code die statistischen Berechnungen und Bewertungen verarbeiten lassen.  
  
-   **Standardmäßige Entwicklung und Toolverwaltung.** Es sind keine weiteren Tools für die Verwaltung oder die Bereitstellung erforderlich – alle R-Aufträge können durch den Aufruf einer gespeicherten Prozedur aufgerufen werden.  
  
     Darüber hinaus die gleiche R-Codes, die Sie ausführen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten mit anderen Datenquellen, wie z. B. Hadoop verwendet werden können.  
  
 Dieser Abschnitt beschreibt die Konzepte, müssen Sie verstehen können erfolgreich R-Lösungen zu konvertieren und dann mit der Produktion bereitstellen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
## In diesem Abschnitt

[Arbeiten mit R-Datentypen](../../advanced-analytics/r-services/working-with-r-data-types.md)

[Konvertieren von R-Code für die Verwendung in R-Dienste](../../advanced-analytics/r-services/converting-r-code-for-use-in-r-services.md)

##  <a name="bkmk_RelatedTasks"></a> Verwandte Aufgaben  
  
[Performance-Optimierung für SQLServer-R-Dienste](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
## Siehe auch  
 [SQL Server R Services – Features und Aufgaben](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 [Sp_execute_external_script & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  
  