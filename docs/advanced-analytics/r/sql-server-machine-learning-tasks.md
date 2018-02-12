---
title: Machine learning-Lebenszyklus und die Teamprozess | Microsoft Docs
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 27a80fa7dddf5066e87a60998a691c07acfb40ab
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="machine-learning-lifecycle-and-personas"></a>Machine Learning-Lebenszyklus und Rollen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Machine Learning-Projekte können komplex sein, da sie die Fähigkeiten und Zusammenarbeit, der einen unterschiedlichen Satz von IT-Experten benötigen. Dieser Artikel beschreibt die principal Aufgaben in Machine Learning Lebenszyklus, der Typ des datenexperten, die im maschinellen lernen und wie die Anforderungen von SQL Server unterstützt beteiligt sind.

> [!TIP]
> 
> Bevor Sie ein Machine Learning-Projekts beginnen, es wird empfohlen, dass die Tools und best Practices, die von bereitgestellt werden, überprüfen Sie die [Microsoft Team Data Science-Prozess](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), oder TDSP. Dieser Prozess der Erstellung von Machine learning-Berater bei Microsoft best Practices für die Planung und Iterationen für Machine learning-Projekte zu konsolidieren. Die TDSP auf der Branchenstandards, z. B. CRISP-DM, enthält jedoch aktuelle Methoden wie die DevOps und visualisieren.

## <a name="machine-learning-life-cycle"></a>Machine Learning-Lebenszyklus

Machine Learning ist ein komplexer Prozess, der alle Aspekte der Daten im Unternehmen berührt und vielen Machine Learning-Projekten enden dauert länger und komplexer als erwartet wird. Hier sind einige der Methoden, durch das Machine Learning Daten Mitarbeiter im Unternehmen erfordert:

+ Machine Learning beginnt mit der ID der Ziele und Geschäftsregeln.
+ Machine Learning-Spezialisten müssen von Richtlinien zum Speichern, extrahieren und Überwachungsdaten bewusst sein.
+ Auflistung von potenziell anwendbaren Daten geht es weiter.  Datenquellen müssen identifiziert werden, und die entsprechenden Daten von Sensoren und Geschäftsanwendungen extrahiert. 
+ Die Qualität der Machine Learning bemühungen ist stark abhängig von nicht nur den Typ der Daten, die verfügbar sind, aber sehr Prozesse zum Extrahieren, verarbeiten und Speichern von Daten verwendet. 
+ Kein Machine Learning-Projekt wäre vollständig ohne eine Strategie für die Berichterstattung und Analyse und möglicherweise kundenengagement und Feedback.

SQL Server unterstützt viele der Lücken zwischen Enterprise-Daten-Experten und Machine Learning-Experten zu überbrücken:

+ Daten können lokal gespeichert werden oder in der Cloud
+ SQL Server ist in jeder Phase des Enterprise-Datenverarbeitung, einschließlich der berichterstellung und ETL integriert.
+ SQL Server unterstützt, datensicherheit, die die Datenredundanz und Überwachung
+ Stellt die Ressourcenkontrolle

## <a name="data-scientists"></a>Datenanalysten

Datenanalysten verwenden eine Vielzahl von Tools für die Analyse und Machine learning, die von Excel oder kostenlose Open Source-Plattformen bis hin zu kostspieligen statistischen Programmsuites, die fundierte technische Kenntnisse erfordern. Verwenden von R oder Python mit SQL Server bietet jedoch einige besondere Vorteile im Vergleich zu diesen herkömmlichen Tools:

+ Sie können die entwickeln und testen eine Lösung, indem Sie mithilfe der Entwicklungsumgebung Ihrer Wahl und anschließend bereitstellen Ihres R oder Python-Codes im Rahmen des T-SQL-Code.
+ Verschieben Sie komplexe Berechnungen aus der Data Scientist Laptop und an den Server, um die Einhaltung von Sicherheitsrichtlinien des Unternehmens datenverschiebungen zu vermeiden.
+ Leistung und Skalierung über spezielle R-Pakete und APIs verbessert. Sie sind nicht mehr von der Singlethread-, arbeitsspeichergebundenem Architektur von R beschränkt und können mit mehreren Threads, Kernen und Prozessen Berechnungen mit großen Datasets arbeiten.
+ Codeportabilität: Lösungen können in SQL Server oder in Hadoop oder Linux ausführen mit [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Code einmal, überall bereitstellen.

## <a name="application-and-database-developers"></a>Anwendungs- und Datenbankentwickler

Datenbankentwickler stehen vor der Aufgabe, zahlreiche Technologien integrieren und die Ergebnisse zusammenführen zu müssen, sodass diese im gesamten Unternehmen gemeinsam genutzt werden können. Ein Datenbankentwickler arbeitet zusammen mit Anwendungsentwicklern, SQL-Entwickler und Datenanalysten Lösungen entwerfen, Datenverwaltungsmethoden, und zu entwickeln oder Bereitstellen von Lösungen.

Integration mit SQL Server bietet viele Vorteile für Entwickler von Data:

+ Der Data Scientist kann RStudio, verwenden, während die Daten die Lösung mit SQL Server Management Studio bereitstellen. Keine weiteren kann von R oder Python-Lösungen.
+ Optimieren Sie Ihre Lösungen, indem das beste aus T-SQL und R, Python verwenden. Komplexe Vorgänge für große Datasets können ausgeführt werden, mithilfe von SQL Server als weit effizienter in r nutzen die Kenntnis der Datenbankexperten zum Verbessern der Leistung der Machine Learning-Lösungen, mit in-Memory-columnstore-Indizes, und Aggregationen mithilfe von SQL-basierten Vorgängen. 
+ Analyseergebnisse Automatisieren von Tasks, die für große Mengen an Daten, z. B. Generieren von vorhersagebewertungen für Produktionsdaten wiederholt ausgeführt werden müssen. 
+ Zugriff parametrisiert R oder Python-Skript aus einer beliebigen Anwendung, die verwendet [!INCLUDE[tsql](../../includes/tsql-md.md)]. Rufen Sie einfach eine gespeicherte Prozedur zum Trainieren eines Modells, eine grafische Ausgabe zu generieren oder Vorhersagen ausgeben.
+ APIs können Streamen von großen Datasets und von mehreren Threads, Kernen und Prozessen datenbankinternen Berechnungen profitieren.

Informationen zu Aufgaben finden Sie unter:
+ [Operationalisieren von R-code](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Datenbankadministratoren

Datenbankadministratoren müssen konkurrierende Projekte und Prioritäten in einen zentralen Kontaktpunkt integrieren: den Datenbankserver. Sie müssen jedoch nicht nur Datenanalysten den Zugriff auf die Daten ermöglichen, sondern einer Vielzahl von Berichtsentwicklern, Business Analysts und Business-Daten-Consumern. Gleichzeitig müssen sie die Integrität der Betriebs- und Berichtsdatenspeicher aufrecht erhalten. Im Unternehmen spielt der Datenbankadministrator eine wichtige Rolle bei der Erstellung und Bereitstellung einer effektiven Data Science-Infrastruktur. 

SQL Server bietet die besonderen Funktionen für den Datenbankadministrator, der die Data Science-Rolle unterstützt werden muss:

+ Sicherheit von SQL Server: der Architektur des [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] gewährleistet die Sicherheit Ihrer Datenbanken und isoliert die Ausführung von externen Skript-Sitzungen vom Betrieb der Datenbankinstanz. Sie können angeben, wer die Berechtigung zum Ausführen von Skripts für Machine Learning und Datenbankrollen verwenden, um Pakete zu verwalten ist.

+ R und Python-Sitzungen werden ausgeführt, in einem separaten Prozess, um sicherzustellen, dass der Server wie gewohnt ausgeführt wird weiterhin, auch wenn die externe Skript Probleme auftreten.

+ Die Ressourcenkontrolle mithilfe von SQL Server können Sie steuern, die Speicher und Prozesse, die auf externen Laufzeiten zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die gesamtleistung des Servers gefährden.

Informationen zu Aufgaben finden Sie unter:
+ [Verwalten und Überwachen von Machine Learning-Lösungen](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>Architekten und Data engineers

Architekten entwerfen integrierte Workflows, die alle Aspekte des Lebenszyklus von Machine Learning umfassen. Data Engineers entwerfen und erstellen ETL-Lösungen und bestimmen, wie Feature engineering-Aufgaben für maschinelles lernen zu optimieren. Konkurrierende geschäftsanforderungen auszugleichen, muss die gesamte Datenplattform entworfen werden.

Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] eng in andere Microsoft-Tools integriert ist, z.B. in den Business Intelligence- und Data Warehouse-Stapel, die Enterprise Cloud- und Mobilitätstools sowie Hadoop, gibt es zahlreiche Vorteile für Datentechniker und Systemarchitekten, die erweiterte Analysen ausführen möchten.

+ Rufen Sie alle Python oder R-Skript mithilfe von gespeicherten Systemprozeduren zum Auffüllen von Datasets, generieren Grafiken oder Abrufen von Vorhersagen. Keine weitere parallele Workflows von entwerfen in Data Science und ETL-Tools. Unterstützung für Azure Data Factory und Azure SQL-Datenbank erleichtert es, Cloud-Datenquellen in Machine learning-Workflows verwendet werden.

+ Verwenden Sie für die Planung und Verwaltung von Machine learning-Aufgaben Automation standard-Workflows in SQL Server, basierend auf Integration Services, SQL-Agent oder Azure Data Factory. Alternativ können Sie verwenden die [operationalisierung Funktionen](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) in Machine Learning-Server.

Informationen zu Aufgaben finden Sie unter:

+ [Erstellen von Machine Learning-Workflows in SQL Server](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

