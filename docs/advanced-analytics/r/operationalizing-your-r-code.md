---
title: Operationalisieren von R-Code (Machine Learning-Dienste) | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c8f745a943104fbf4589b2929aad9f018196fdb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="operationalize-r-code-machine-learning-services"></a>Operationalisieren von R-Code (Machine Learning-Services)

Datenbankentwickler stehen vor der Aufgabe, zahlreiche Technologien integrieren und die Ergebnisse zusammenführen zu müssen, sodass diese im gesamten Unternehmen gemeinsam genutzt werden können. Ein Datenbankentwickler arbeitet zusammen mit Anwendungsentwicklern, SQL-Entwickler und Datenanalysten entwerfen und Bereitstellen von Lösungen.

Dieser Artikel beschreibt die wichtigsten Punkte für die Datenbankentwickler beim operationalisieren von R-Code mithilfe von SQL Server berücksichtigt werden.

## <a name="get-started-with-r-code-in-sql-server"></a>Erste Schritte mit R-Code in SQL Server

Bisher hat die Integration von Machine Learning-Lösungen bedeutet eine umfangreiche kann zur Unterstützung von Leistung und Integration. Allerdings-Prozeduren Verschieben von R und Python-Code in einer produktionsumgebung ist viel einfacher, im Microsoft Machine Learning-Services, da der Code in SQL Server ausgeführt werden kann und mithilfe von aufgerufen. Sie können weiterhin Zugriff auf vertraute Tools zu verwenden und müssen keine R-Entwicklungsumgebung installieren. 

Weitere Informationen zur grundlegenden Syntax finden Sie unter:

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Verwenden von R-Code in SQL](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Ein Beispiel dafür, wie Sie R-Code in die Produktion bereitstellen können, mithilfe von gespeicherten Prozeduren finden Sie unter:

+ [In der Datenbank Analytics für SQL-Entwickler](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="optimize-your-r-code"></a>Optimieren Sie Ihre R-code

Konvertieren von R-Code in SQL ist natürlich einfacher, wenn einige Optimierungen in R oder Python-Code im Vorfeld durchgeführt werden. Dazu gehören das Vermeiden von Datentypen, die Probleme verursachen, Eliminierung unnötiger datenkonvertierungen vermeiden und den R-Code umschreiben, als einen einzigen Funktionsaufruf, der leicht parametrisiert werden können. Weitere Informationen finden Sie in den folgenden Themen:

+ [R-Bibliotheken und -Datentypen](r-libraries-and-data-types.md)

+ [Konvertieren von R-Code für die Verwendung in R Services](converting-r-code-for-use-in-sql-server.md)

+ [Generieren eine R gespeicherte Prozedur mithilfe von sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>Integration von R und Python mit Anwendungen

Da Sie von einer gespeicherten Prozedur Machine Learning-Dienste beginnen können, können Sie R oder Python-Skripts aus einer beliebigen Anwendung ausführen, die Senden einer T-SQL-Anweisung und die Ergebnisse verarbeiten können.

Beispielsweise könnten Sie erneutes Trainieren eines Modells nach einem Zeitplan mit dem Task T-SQL-Task in Integration Services oder mit einem anderen Auftragsplaner, die eine gespeicherte Prozedur ausgeführt werden kann.

Bewerten ist eine wichtige Aufgabe, die kann einfach automatisierte oder aus externen Anwendungen gestartet. Sie trainieren das Modell im Vorfeld mithilfe des R, Python oder einer gespeicherten Prozedur, und speichern Sie das Modell im Binärformat zu einer Tabelle. Das Modell kann dann in eine Variable im Rahmen der Aufruf einer gespeicherten Prozedur, verwenden eine der folgenden Optionen für die Bewertung von T-SQL geladen werden:

+ [Echtzeit](../real-time-scoring.md) Bewertung, optimiert für kleine Batches
+ Einzeiliges Bewertung, für das Aufrufen von einer Anwendung
+ [Bewerten von systemeigenen](../sql-native-scoring.md), für die schnelle Batch Vorhersage von SQL Server ohne Aufruf von R

Diese exemplarische Vorgehensweise enthält Beispiele für bewerteten mithilfe einer gespeicherten Prozedur in Batches und einzeiliges Modi:

+ [End-to-end Data sience-Vorgehensweise für R in SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Finden Sie unter dieser Projektmappenvorlagen für Beispiele zur Bewertung in einer Anwendung zu integrieren:

+ [Retail forecasting](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Unterbindung](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [Kunden, die clustering](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Hoher Leistung und Skalierung

Obwohl die open Source-R-Sprache Einschränkungen aufweist bekanntermaßen, die "revoscaler"-Paket APIs können großen Datasets ausgeführt werden und davon profitieren mit mehreren Threads, Kernen und Prozessen datenbankinternen Berechnungen.

Wenn Ihre R-Lösung komplexe Aggregationen verwendet oder große Datasets, können Sie SQL-Server möglichst effizient in-Memory Aggregationen und columnstore-Indizes nutzen und lassen Sie die R-Code behandeln die statistischen Berechnungen und Bewertungen.

Weitere Informationen zum Verbessern der Leistung in SQL Server-Machine Learning finden Sie unter:

+ [Optimieren der Leistung für SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Tipps zur Optimierung der Leistung und tricks](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>R-Code für andere Plattformen anpassen oder remotecomputekontexten

Derselbe R-Code, die Sie für ausgeführt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten mit anderen Datenquellen wie z.B. Hadoop, verwendet werden können und in anderen Kontexten zu berechnen.

Weitere Informationen zu den von Microsoft R unterstützten Plattformen finden Sie unter:

+ [Einführung in Microsoft R](https://docs.microsoft.com/r-server/)

+ [Untersuchen von "revoscaler"](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

Weitere Informationen dazu, wie Sie die Microsoft-R-Lösungen auf große Datenmengen oder mehrere Plattformen ausgeführt optimieren können finden Sie unter:

+ [Schreiben Sie die Aufteilung Algorithmen](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Berechnen mit umfangreichen Daten in R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Entwickeln Sie eine eigene parallele Algorithmen](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

