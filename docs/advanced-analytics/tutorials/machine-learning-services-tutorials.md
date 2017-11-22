---
title: SQL Server-Machine Learning-Lernprogramme | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: Python
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: "32"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c0547d809e73e13b7bedcc8ac960b00c7c8a9706
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-machine-learning-tutorials"></a>SQL Server Machine Learning-Lernprogramme

Dieser Artikel bietet eine umfassende Liste der Lernprogramme, Demos und Beispielanwendungen, die Machine Learning-Funktionen in SQL Server 2016 oder SQL Server-2017 verwenden. Beginnen Sie hier, um zu erfahren, zum Ausführen von R oder Python von T-SQL, wie remote und lokalen rechenkontexten verwenden und den R und Python-Code für eine SQL-produktionsumgebung zu optimieren.

## <a name="start-here"></a>Beginnen Sie hier

+ [Python-Tutorials](../tutorials/sql-server-python-tutorials.md)

+ [R-Lernprogramme](../tutorials/sql-server-r-tutorials.md)

Weitere Informationen zu Anforderungen und zu ersten Schritten finden Sie unter [Voraussetzungen](#bkmk_prerequisites).

## <a name="samples-and-solutions"></a>Beispiele und -Lösungen

+ [Beispiele](#bkmk_samples) 

    Diese praktische Szenarien aus der SQL Server-Entwicklungsteam veranschaulichen, wie Machine Learning in Anwendungen eingebettet werden sollen. Alle Beispiele enthalten Code, die Sie herunterladen, ändern und verwenden können, in der Produktion.

+ [Lösungen](#bkmk_solutions) 

    Vorlagen für das Microsoft Data Science-Team können angepasst werden, um Machine Learning lässt sich schnell und Ihnen den Einstieg. Jede Lösung wird auf einen bestimmten Task oder Branche Problem zugeschnitten; Darüber hinaus sind die meisten Lösungen zum Ausführen von in SQL Server oder in eine Cloudumgebung wie Azure Machine Learning ausgelegt. Mithilfe von Microsoft R Server "oder" Machine Learning-Server können andere Lösungen unter Linux oder Spark oder im Hadoop-Cluster ausführen.

### <a name ="bkmk_samples"></a>SQL Server-Produktbeispiele

Markieren Sie diese Beispiele und Demos, die von der SQL Server und R-Server-Entwicklungsteam bereitgestellte Methoden, mit denen Sie eingebettete Analytics in echten Anwendungen verwenden können.

+ [Ausführen von Kunden mithilfe von R und SQL Server-clustering](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  Verwenden Sie Segment Kunden auf Grundlage der Umsatzdaten unüberwachtes lernen. In diesem Beispiel verwendet den Algorithmus skalierbare RxKmeans von Microsoft R zum clustering-Modell zu erstellen. 
  
  Gilt für: SQLServer 2016 oder SQLServer 2017

+ [NEU! Ausführen von Kunden über Python- und SQL Server-clustering](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Erfahren Sie, wie die Kmeans-Algorithmus verwenden, um nicht überwachten Gruppieren von Kunden ausführen. In diesem Beispiel wird die Python-Sprachdatenbank verwendet. 
    
    Gilt für: SQLServer 2017

+ [Erstellen eines Vorhersagemodells mittels R und SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Erfahren Sie, wie eine Ski Vermietung Business Machine learning-zukünftige Vermietung Vorhersagen verwenden kann dadurch die Business-Plan und die Mitarbeiter, zukünftige Bedarf zu decken. In diesem Beispiel verwendet die Microsoft-Algorithmen zum Erstellen von logistischen Regression und entscheidungsstrukturmodelle. 
  
  Gilt für: SQLServer 2016 oder SQLServer 2017

+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

   Erstellen der Ski Vermietung Analyse-Anwendung mithilfe von Python, zukünftige Bedarf planen. Dieses Beispiel verwendet die neue Python-Clientbibliothek **Revoscalepy**, um ein lineares Regressionsmodell zu erstellen.
   
   Gilt für: SQLServer 2017

### <a name="bkmk_solutions"></a>Projektmappenvorlagen

Das Microsoft Data Science-Team hat Lösungsvorlagen bereitgestellt, die verwendet werden kann, Lösungen für häufige Szenarien sind. Der gesamte Code wird zusammen mit Anweisungen zum Trainieren und Bereitstellen eines Modells für die Bewertung mithilfe von SQL Server gespeicherte Prozeduren bereitgestellt.

+ [Betrugserkennung](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Vorhersage der Kundenabwanderung](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Vorbeugende Wartung](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Krankenhaus Dauer der Vorhersagen](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

Weitere Informationen finden Sie unter [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) (Machine Learning-Vorlagen mit SQL Server 2016 R Services).

## <a name="more-resources-and-reading"></a>Weitere Ressourcen und Lesen von Daten

+ [Warum erstellen wir es?](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    Was verbirgt sich hinter R Services? Lesen Sie diesen Artikel aus der Entwicklungs- und PM-Team, das den Ursprung und die Ziele des SQL Server R Services erläutert.

+ [Lernprogramme und Beispieldaten für Microsoft R](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    In dieser Lektion erfahren Sie, Microsoft R und den in dieser Auflistung schnelle Lernprogramme die RevoScaleR-Paket bietet. Erfahren Sie, wie R-Code einmal schreiben und eine beliebige Stelle, bereitstellen, die mit "revoscaler"-Datenquellen und remote rechenkontexte.

+ [Erste Schritte mit MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  Erfahren Sie, wie neuen Algorithmen im MicrosoftML-Paket für erweiterte Modellierung und skalierbare Datentransformationen, die für mehrere rechenkontexte optimiert zu verwenden.

## <a name="bkmk_Prerequisites"></a>Voraussetzungen

Wenn diese Lernprogramme ausführen möchten, müssen Sie herunterladen und Installieren der SQL Server-Machine learning-Komponenten, wie hier beschrieben:

+ [Einrichten von SQL Server 2017 Machine Learning Services oder SQL Server 2016 R Services](../r/set-up-sql-server-r-services-in-database.md)
+ [Einrichten von SQL Server 2017 Python-Dienste](../python/setup-python-machine-learning-services.md)

Mit SQL Server-2017 können Sie R oder Python oder beides installieren. Andernfalls werden die gesamte Setupvorgang, Architektur und Anforderungen identisch.

Nach dem Ausführen von SQL Server-Setup, vergessen Sie nicht folgenden wichtigen Schritte aus:

1. Die externen Skript Ausführung-Funktion aktivieren, indem ausgeführt `sp_configure 'external scripts enabled', 1`. Befolgen Sie die Anweisungen neu konfigurieren und starten Sie SQL Server neu.
2. Stellen Sie sicher, dass das Launchpad-Dienst ausgeführt wird, und der Arbeitsthread es verwendet Konten eine mit der SQL Server-Instanz Verbindung kann.
3. Überprüfen Sie die Berechtigungen für den Benutzer möglich, die r oder Python-Skripts ausführen müssen. Unabhängig davon, ob Sie SQL-Anmeldungen oder Windows-Benutzerkonten verwenden wird der Benutzer muss über die Berechtigung zum Ausführen von R oder Python-Skripts und muss in der Lage, mit der Instanz herstellen. Je nach im Lernprogramm der Benutzer auch benötigen die Berechtigung zum Schreiben von Daten, Erstellen von Datenbankobjekten oder führen Sie eine Bulk Import von Daten.

Einzelheiten finden Sie in diesem Artikel finden Sie einige allgemeine Setup- und Konfigurationsprobleme: [Problembehandlung Machine Learning-Dienste](../machine-learning-troubleshooting-faq.md)

> [!NOTE]
> Diese Lernprogramme verwenden eine andere open Source-R oder Python-Tool kann nicht ausgeführt werden. Entwicklungsumgebung vorbereiten und die SQL Server-Computer mit Machine Learning benötigen die R oder Python-Bibliotheken von Microsoft, die Integration mit SQL Server und Verwendung von remote rechenkontexte unterstützen.
