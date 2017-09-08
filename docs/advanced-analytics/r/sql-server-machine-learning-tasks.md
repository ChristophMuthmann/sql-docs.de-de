---
title: SQL Server-Machine LEarning-Aufgaben | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 04/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: c0e7a0929d5caa84df1a1fb02894db08313a36bd
ms.contentlocale: de-de
ms.lasthandoff: 09/06/2017

---
# <a name="sql-server-machine-learning-tasks"></a>SQL Server-Machine Learning-Aufgaben

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] kombiniert die Leistungsfähigkeit und Flexibilität der Open-Source-Sprache R mit Unternehmenstools für Datenspeicherung und -verwaltung, Workflowentwicklung, Berichte und Visualisierung. Dieses Thema beschreibt die Machine learning-Lebenszyklus und wie SQL Server die Bedürfnisse vier unterschiedlicher datenexperten unterstützt, die beim Machine Learning Enagged sind.

## <a name="machine-learning-life-cycle"></a>Machine Learning-Lebenszyklus

Machine Learning ist nicht an eine kurzfristige Aufgabe jedoch eher einen langfristigen Prozess, der alle Aspekte der Daten im Unternehmen berührt. Machine Learning beginnt mit der Kennung der Unternehmensziele und Regeln und Sammeln von Daten von Sensoren und Geschäftsanwendungen. Machine Learning ist stark von Prozessen zum Extrahieren, verarbeiten und Speichern von Daten und wird zunehmend wichtig, wenn Richtlinien für das Speichern, extrahieren und Überwachungsdaten in Betracht gezogen. Machine Learning wird jetzt eine wichtige Component von Strategien für die Berichterstattung und Analyse, als auch kundenengagement und Feedback.



SQL Server ist Ideal für Machine Learning, da der Großteil der Lücken in Machine learning-Prozesses Brücke:

+ Funktioniert lokal oder in der Cloud
+ In jeder Phase des Enterprise-Datenverarbeitung, einschließlich Business Intelligence integriert
+ Unterstützt die verbesserte Sicherheit
+ Stellt die Ressourcenkontrolle und Überwachung

## <a name="data-professionals-and-how-they-use-machine-learning"></a>Daten-Experten und wie sie verwenden Machine Learning

### <a name="data-scientists"></a>Datenanalysten

Data haben Scientists Zugriff auf eine Vielzahl von Tools für die Analyse und Machine learning, die von Excel oder kostenlose Open Source-Plattformen bis hin zu kostspieligen statistischen Programmsuites, die fundierte technische Kenntnisse erfordern. Integration mit SQL Server bietet jedoch besondere Vorteile:

+ Entwickeln und testen Sie Ihre Lösungen mithilfe der R-Entwicklungsumgebung Ihrer Wahl.
+ Drücken Sie Berechnungen mit der Datenbank, die datenverschiebungen bei gleichzeitiger Einhaltung von Sicherheitsrichtlinien des Unternehmens zu vermeiden.
+ Leistung und Skalierung über spezielle R-Pakete und APIs verbessert. Sie sind nicht mehr von der Singlethread-, arbeitsspeichergebundenem Architektur von R beschränkt und können mit mehreren Threads, Kernen und Prozessen Berechnungen mit großen Datasets arbeiten.
+ R-Code kann problemlos für die Produktion bereitgestellt und von Unternehmenstools, Anwendungen, andere Datenbanken und Dashboards aufgerufen werden.
+ Datenanalysten können bereitstellen und aktualisieren eine analyselösung standardanforderungen für die Verwaltung von Unternehmensdaten, einschließlich Sicherheit und Überwachung des Benutzerzugriffs
+ Codeportabilität: R-Code erneut problemlos für andere Datenquellen, wie z.B. Hadoop verwenden

### <a name="application-and-database-developers"></a>Anwendungs- und Datenbankentwickler

Datenbankentwickler stehen vor der Aufgabe, zahlreiche Technologien integrieren und die Ergebnisse zusammenführen zu müssen, sodass diese im gesamten Unternehmen gemeinsam genutzt werden können. Ein Datenbankentwickler arbeitet zusammen mit Anwendungsentwicklern, SQL-Entwicklern und Datenspezialisten an dem Entwurf und der Bereitstellung von Lösungen und an empfohlenen Datenverwaltungsmodellen. 

Integration mit SQL Server bietet folgende Vorteile für Data-Entwickler, die Arbeiten mit Machine Learning:

+ Verwenden von vertrauten Tools für die Interaktion mit R-Skripts. Ermöglichen der Data Scientist RStudio verwenden, während die Daten die Lösung mit SQL Server Management Studio bereitstellen. Keine weiteren kann von R oder Python-Lösungen.
+ Optimieren Sie, indem Sie mischen und Anpassen von SQL "und" R "oder" SQL "und" Python. In vielen Fällen können mithilfe von SQL Server-Funktionen, z. B. in-Memory-Columnstoreindexes oder sehr schnell Aggregate wesentlich effizienter in T-SQL komplexe Vorgänge für große Datasets ausgeführt werden. Verwenden Sie ein Machine learning-Sprache, in denen es sinnvoll, und verwenden Sie SQL verschieben und Daten zu verarbeiten.
+ Analyseergebnisse Automatisieren von Tasks, die für große Mengen an Daten, z. B. Generieren von vorhersagebewertungen für Produktionsdaten wiederholt ausgeführt werden müssen.
+ Führen Sie R oder Python-Skript aus einer beliebigen Anwendung, die verwendet [!INCLUDE[tsql](../../includes/tsql-md.md)]. Rufen Sie einfach eine gespeicherte Prozedur zum Erstellen einer parametrisierten Modell, generieren eine komplexe grafische Ausgabe oder Vorhersagen ausgeben.
+ Die **"revoscaler"** und **Revoscalepy** APIs großen Datasets ausgeführt werden und mit mehreren Threads, Kernen und Prozessen datenbankinternen Berechnungen profitieren können.

Informationen zu Aufgaben finden Sie unter:
+ [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Datenbankadministratoren

Datenbankadministratoren müssen konkurrierende Projekte und Prioritäten in einen zentralen Kontaktpunkt integrieren: den Datenbankserver. Sie müssen jedoch nicht nur Datenanalysten den Zugriff auf die Daten ermöglichen, sondern einer Vielzahl von Berichtsentwicklern, Business Analysts und Business-Daten-Consumern. Gleichzeitig müssen sie die Integrität der Betriebs- und Berichtsdatenspeicher aufrecht erhalten. Im Unternehmen spielt der Datenbankadministrator eine wichtige Rolle bei der Erstellung und Bereitstellung einer effektiven Data Science-Infrastruktur. 

SQL Server bietet die besonderen Funktionen für den Datenbankadministrator, der die Data Science-Rolle unterstützt werden muss:

+ Sicherheit von SQL Server: der Architektur des [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] gewährleistet die Sicherheit Ihrer Datenbanken und isoliert die Ausführung von externen Skript-Sitzungen vom Betrieb der Datenbankinstanz. Sie können angeben, wer über die Berechtigung zum Ausführen von Machine Learning-Skripts verfügt, und wer können neue R-Pakete installieren, der mithilfe von Datenbankrollen.

+ R und Python-Sitzungen werden ausgeführt, in einem separaten Prozess, um sicherzustellen, dass der Server wie gewohnt ausgeführt wird weiterhin, auch wenn die externe Skript Probleme auftreten.

+ Die Ressourcenkontrolle mithilfe von SQL Server können Sie steuern, die Speicher und Prozesse, die auf externen Laufzeiten zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die gesamtleistung des Servers gefährden.

Informationen zu Aufgaben finden Sie unter:
+ [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

### <a name="architects-and-etl-designers"></a>Architekten und ETL-Entwickler

Architekten entwerfen integrierte Workflows, die alle Aspekte des Lebenszyklus von Machine Learning umfassen. Data Engineers entwerfen und erstellen ETL-Lösungen und zu bestimmen, wie namens Feature Engineering optimieren Verknüpfung Aufgaben werden im Rahmen des Machine learning-Prozesses. Die gesamte Plattform muss häufig entworfen werden, um konkurrierende und ergänzende geschäftliche Anforderungen zu verteilen.

Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] eng in andere Microsoft-Tools integriert ist, z.B. in den Business Intelligence- und Data Warehouse-Stapel, die Enterprise Cloud- und Mobilitätstools sowie Hadoop, gibt es zahlreiche Vorteile für Datentechniker und Systemarchitekten, die erweiterte Analysen ausführen möchten.

+ Vertraute Entwicklungstools für die Entwicklung von R und Python-Lösungen. Sie können eine beliebige Python oder R-Skript mithilfe von gespeicherten Systemprozeduren zum Auffüllen von Datasets, generieren Grafiken oder Abrufen von Vorhersagen aufrufen. Keine weitere parallele Workflows von entwerfen in Data Science und ETL-Tools. Unterstützung für Azure Data Factory und Azure SQL-Datenbank erleichtert es, Transformieren und Verwalten von Daten und Cloud-Datenquellen in Machine learning-Workflows verwenden.

+ Planung und Verwaltung mithilfe von operationalisierung-Funktionen in Microsoft R Server.

Informationen zu Aufgaben finden Sie unter:

+ [Erstellen von Workflows, die R in SQL Server verwenden](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)


