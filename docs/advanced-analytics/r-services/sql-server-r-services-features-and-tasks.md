---
title: "SQL Server R Services – Features und Aufgaben | Microsoft Docs"
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
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server R Services – Features und Aufgaben
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] kombiniert die Leistungsfähigkeit und Flexibilität von der open-Source-Sprache R mit Unternehmenstools für Datenspeicher und Management, Workflow-Entwicklung und Berichte und Visualisierung. Die Anforderungen von vier verschiedenen Data-Experten und Szenarien unterstützt.  
  
## Data Scientists: Analysieren, Modellieren und Bewerten mittels R und SQL Server  
 Data Scientists haben Zugriff auf eine Vielzahl von Tools für die Analyse und Machine Learning, die vom vertrauten Excel und Open-Source-Plattformen bis hin zu kostspieligen statistischen Programmsuites reichen, die fundierte technische Kenntnisse erfordern. Zwischen diesen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet einzigartige Vorteile, da dadurch die Datenanalyse auf Push Berechnungen für die Datenbank Verschieben von Daten zu vermeiden und die Einhaltung der Sicherheitsrichtlinien der Unternehmen. Darüber hinaus der R-Code erstellt, indem die Datenanalyse kann problemlos werden für die Produktion bereitgestellt und wird von vertrauten Unternehmenstools und Lösungen: Applikationen basierend auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken, BI-Berichtstools und Dashboards. Mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], die Datenanalysten kann bereitstellen und Aktualisierung eine analytische Lösung während der Besprechung standardanforderungen für die Verwaltung von Unternehmensdaten, einschließlich Sicherheit, einfache Bereitstellung, Verwaltung und Überwachung, und Zugriff auf Überwachung.  
  
-   **Vertraute Benutzeroberfläche.**  Entwickeln Sie und Testen Sie Ihre Lösungen mit der R-Entwicklungsumgebung Ihrer Wahl.  
  
-   **Datenbankinterne Verarbeitung.**  Führen Sie R-Code und die Berechnungen, die auf dem Computer, der als Host erfolgen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz. Hierdurch entfällt die Notwendigkeit zum Verschieben von Daten.  
  
-   **Leistung und Skalierung.**  Skalierbare R-Pakete und APIs, enthält, damit Sie nicht mehr durch die Singlethread-arbeitsspeichergebundenem Architektur von r beschränkt werden Sie können mit großen Datasets und Multi-Thread, mehrere Prozesse mit mehreren Kernen Berechnungen arbeiten.  
    
-   **Codeportabilität.**  Der gleiche R-Code, die für ausgeführt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten können mit anderen Datenquellen, wie z. B. Hadoop einfach erneut verwendet werden.  
  
 Ausführliche Informationen zu Aufgaben und Konzepte, finden Sie unter [Durchsuchen von Daten und Predictive Modellierung mit R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
## Anwendungs- und Datenbankentwickler: Bereitstellen von R-Lösungen  
 Datenbankentwickler stehen vor der Aufgabe, zahlreiche Technologien integrieren und die Ergebnisse zusammenführen zu müssen, damit diese im gesamten Unternehmen gemeinsam genutzt werden können. Ein Datenbankentwickler arbeitet zusammen mit Anwendungsentwicklern, SQL-Entwicklern und Data Scientists am Entwurf von Lösungen, an Empfehlungen für Datenverwaltungsmethoden und der Gestaltung und Bereitstellung von Lösungen. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet viele Vorteile für Entwickler, die mit Datenanalysten arbeiten:  
  
-   **Interagieren mit R-Skripts, die mit [!INCLUDE[tsql](../../includes/tsql-md.md)].**  Der Berichts-Entwickler, Analytiker und Datenbankentwickler können R-Skripts durch Aufrufen von gespeicherten Systemprozeduren aufrufen. Wenn Ihre Lösung komplexe Aggregationen verwendet oder große Datasets umfasst, dass Berechnungen in der Datenbank ausführen, oder verwenden Sie eine Mischung aus R und [!INCLUDE[tsql](../../includes/tsql-md.md)], je nachdem, auf die die beste Leistung bietet. Die einfache Integration mit  [!INCLUDE[tsql](../../includes/tsql-md.md)] ist besonders Willkommen, wenn Sie Aufgaben wiederholt für große Mengen an Daten, z. B. Generieren von Vorhersageabfragen Bewertungen für Produktionsdaten ausführen müssen.  
  
     Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bedeutet auch, dass Sie von jeder Anwendung aus R-Skripts ausführen können, verwendet [!INCLUDE[tsql](../../includes/tsql-md.md)]. Angenommen, Sie können einfach Aufrufen einer gespeicherten Prozedur aus einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Bericht R-Skript aufzurufen und einen Zeitraum sowie die Vorhersagen im Bericht zu generieren.  
  
-   **Leistung und Skalierung.**  Obwohl die open-Source-R-Sprache begrenzt ist bekannt ist, das Paket RevoScaleR APIs von bereitgestellten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Arbeiten mit großen Datasets und Multi-threaded, Multi-Core, mit mehreren Prozessen in der Datenbank Berechnungen profitieren können.  
  
-   **Standardmäßige Entwicklungs- und Verwaltungstools.**  Keine weiteren Tools für die Verwaltung oder die Bereitstellung erforderlich sind; Alle R-Aufträge können durch den Aufruf einer gespeicherten Prozedur aufgerufen werden. Darüber hinaus die gleiche R-Codes, die Sie ausführen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten mit anderen Datenquellen, wie z. B. Hadoop verwendet werden können.  
  
 Ausführliche Informationen zu Aufgaben und Konzepte, finden Sie unter [R-Code betrieblichen](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
## Datenbankadministratoren: Verwalten erweiterter Analyselösungen  
 Datenbankadministratoren müssen konkurrierende Projekte und Prioritäten zu einem zentralen Kontaktpunkt integrieren: dem Datenbankserver. Sie müssen jedoch nicht nur Data Scientists den Zugriff auf die Daten ermöglichen, sondern einer Vielzahl von Berichtsentwicklern, Wirtschaftsanalytikern und Nutzern von Geschäftsdaten. Gleichzeitig müssen sie die Integrität der Betriebs- und Berichtsdatenspeicher aufrecht erhalten. Im Unternehmen spielt der Datenbankadministrator eine wichtige Rolle bei der Erstellung und Bereitstellung einer effektiven Data Science-Infrastruktur. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet viele Vorteile an dem Datenbankadministrator, der die Data Science-Rolle unterstützt:  
  
-   **Sicherheit.**  Die Architektur des [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] behält Ihrer Datenbanken sicher und isoliert die Ausführung des R-Sitzungen aus dem Vorgang der Datenbankinstanz ein.  
  
     Sie können angeben, wer über die Berechtigung zum Ausführen von R-Skripts, und stellen Sie sicher, dass die Daten in der R-Aufträge verwaltet werden mit den gleichen Sicherheitsrollen, die in definiert sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Zuverlässigkeit.**  R-Sitzungen werden in einem separaten Prozess ausgeführt, um sicherzustellen, dass der Server weiterhin wie gewohnt ausgeführt wird, auch wenn bei der R-Sitzung Probleme auftreten.  
  
-   **Ressourcenkontrolle.**  Sie können den Umfang der Ressourcen steuern, die dem R-Laufzeitmodul zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die Gesamtleistung des Servers gefährden.  
  
 Ausführliche Informationen zu Aufgaben und Konzepte, finden Sie unter [Verwalten und Überwachen von R-Lösungen](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md).  
  
## Architekten und ETL-Entwickler: Integrierte Workflows unter Einbeziehung von R und SQL Server erstellen  
 Data Engineers entwerfen und erstellen ETL-Lösungen (Extrahieren, Transformieren, Laden). Architekten entwerfen Datenplattformen, die konkurrierende und ergänzende geschäftliche Anforderungen erfüllen. Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ist umfassend integriert mit anderen Microsoft-Tools wie z. B. des Business Intelligence und Datawarehouse-Stapel Enterprise Cloud und Mobilitäts-Tools und Hadoop bietet es eine Reihe von Vorteile, die Daten Techniker oder Systemarchitekten, erweiterte Analyse heraufstufen möchte.  
  
-   **Breite Palette vertrauter Entwicklungstools.**  Wenn Sie R-Lösungen entwickeln, [!INCLUDE[tsql](../../includes/tsql-md.md)] und gespeicherten Systemprozeduren zum Füllen des Datasets, R-Aufträge ausführen oder Abrufen von Vorhersagen. Mehr parallele Workflows Data Science Tools entwerfen; Erstellen Sie Ihren Datenpipelines in der vertrauten Umgebung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Müssen Sie Clouddaten nutzen? Unterstützung für Azure Data Factory und Azure SQL-Datenbank erleichtert es, Transformieren und Verwalten von Daten und Cloud-Datenquellen in Workflows genauso verwendet wie für lokale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten.  
  
-   **Erstellen und Verwalten von Workflows.**  Planen Sie Aufträge und Erstellen von Workflows mit R-Skripts, gespeicherte Systemprozeduren verwenden.  
  
 Ausführliche Informationen zu Aufgaben und Konzepte, finden Sie unter [Erstellen von Workflows mit R in SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
## Siehe auch  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  