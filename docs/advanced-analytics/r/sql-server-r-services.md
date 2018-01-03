---
title: SQL Server-Machine Learning-Dienste | Microsoft Docs
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 136df79ded4c86a183d78ecc39821550ca9c24c9
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="sql-server-machine-learning-services"></a>SQL Server-Machine Learning-Dienste

SQL Server 2017 Machine Learning Dienste (zuvor SQL Server 2016 R Services) bietet eine Plattform zum Entwickeln und Bereitstellen von intelligenten Anwendungen, die neue Einblicke zu gewinnen. Machine Learning in integriert ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie Analysen in der Nähe der Daten und beseitigen Sie die Kosten und Sicherheitsrisiken durch Verschieben von Daten.
  
+ In SQL Server 2016 können Sie einfache Weise entwickeln und Bereitstellen von Lösungen basierend auf der die beliebte Sprache R Data Science. 

    Merkmale der [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) Bibliotheken, die für Ihre R-Lösungen und die Art der Algorithmen in neue Skalierbarkeit und Leistung bieten [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).
+ In SQL Server-2017 können Sie R und Python zu entwickeln und zu operationalisieren Data Science-Lösungen. 

    Die [Revoscalepy](../python/what-is-revoscalepy.md) Library für Python bietet remote rechenkontexte und Skalierbarkeit vergleichbar sein, um diese im "revoscaler".

SQL Server unterstützt verbesserte Leistung, Sicherheit und verwaltbarkeit für Machine Learning-arbeitsauslastungen durch einen umfassenden Satz von Tools und Technologien. Sie können R oder Python-Lösungen mit geeigneten, vertrauten SQL-Methoden und Tools bereitstellen. Verwenden Sie einfach [!INCLUDE[tsql](../../includes/tsql-md.md)] R oder Python-Laufzeiten aus der Produktionsanwendungen, Modelle zu erstellen oder Abrufen von visuellen Elementen aufrufen. Wenn Sie bereits ein Modell trainiert haben, können Sie vorhersagen generieren, daraus über nur T-SQL, [native Bewertung](../sql-native-scoring.md).

## <a name="machine-learning-in-sql-server-2017"></a>Machine learning-in SQL Server-2017

+ Installieren Sie **Machine Learning-Services (Datenbankintern)** während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup So aktivieren Sie die sichere Ausführung von R oder Python-Skripts auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
    Wenn Sie diese Funktion auswählen, werden Erweiterungen im Datenbankmodul um die Ausführung von Code, in R oder Python unterstützen installiert. Ein neuer Dienst erstellt, die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], um die Verwaltung der Kommunikation zwischen den externen Laufzeiten und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.
  
+ Installieren Sie **Microsoft Machine Learning-Server (eigenständig)** auf einem separaten Computer, wenn Sie keine SQL Server als computekontext verwenden müssen. Machine Learning-Server sind die gleichen Machine Learning-Komponenten, sowie die Möglichkeit, skalierbarer, verteilter Machine Learning Aufträge als Webdienst auszuführen.
  
+ Installieren Sie [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) auf Remotecomputern zum Entwickeln von Lösungen, die in SQL Server oder auf Machine Learning-Server unter Windows, Linux oder Hadoop bereitgestellt werden kann.

## <a name="machine-learning-in-sql-server-2016"></a>Machine learning-in SQL Server 2016

+ Installieren Sie **R Services (Datenbankintern)** während des Setups von SQL Server 2016, um sichere Ausführung von R-Skripts auf ermöglichen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
    Wenn Sie dieses Feature auswählen, erhalten Sie die Möglichkeit, die beim Ausführen von R-Skript mithilfe des SQL Servers als computekontext oder zum Ausführen von R-Skripts in einer gespeicherten Prozedur.
  
+ Installieren Sie **Microsoft R Server (eigenständig)** aus SQL Server 2016-Setup aus, um die R-Komponenten auf einem separaten Computer installieren, die für die Entwicklung und Bereitstellung von R-Lösungen verwendet werden können.

## <a name="how-to-get-started"></a>Erste Schritte

SQL Server-Setup bietet zwei Optionen:

+ Installieren der in der Datenbank Analytics feature, das in SQL Server, integriert oder
+ Installieren Sie die eigenständige Version des Machine Learning-Server (oder Microsoft R Server), die in unterschiedlichem Umfang Machine Learning ohne eine Instanz von SQL Server unterstützt.

Wenn Sie zum Ausführen von R-Code in müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entweder mit gespeicherten Prozeduren oder mithilfe von SQL Server-Instanz als computekontext, müssen Sie installieren [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] wie beschrieben in der [-Installationshandbuch für](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md). Diese Option bietet maximale Sicherheit und Integration in SQL Server-Tools.

Microsoft Machine Learning-Server (eigenständig) ist eine separate Option konzipiert, die für die Verwendung der [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) und [Python-Bibliotheken verknüpft](../python/what-is-revoscalepy.md) auf einem Windows-Computer, die SQL Server nicht ausgeführt wird. Diese Option erfordert eine Enterprise Edition-Lizenz für SQL Server.
    
Es wird empfohlen, dass Sie Machine Learning-Server (eigenständig) auf einem Laptop oder einem anderen Remotecomputer für die Entwicklung verwendet installieren und verwenden diesen Computer erstellen und Testen von Machine Learning-Lösungen, die mit einer Instanz von auf einfache Weise bereitgestellt werden können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] also Ausführen von Machine Learning Services \(In der Datenbank\) oder einer anderen unterstützten Kontext zu berechnen.
  
Sie können auch die **Mrsdeploy** Paket, das mit Machine Learning-Server zum Veröffentlichen und Verteilen von R und Python-Projekte als Webdienst installiert ist.

## <a name="additional-resources"></a>Weitere Ressourcen

+ [Erste Schritte mit SQL Server-Machine Learning-Services](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    Beschreibt häufige Szenarios für die Verwendung von R mit SQL Server

+ [Einrichten von SQL Server-Machine Learning-Services oder R Services In der Datenbank](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    Installieren von R und die zugehörigen Datenbankkomponenten als Teil des SQL Server-setup
  
+ [SQL Server und R-Lernprogramme](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Erfahren Sie, wie Sie SQL Server-Datenquellen in Ihrem R-Code erstellen und Remote Compute-Kontexte verwenden. Andere Tutorials für SQL-Entwickler veranschaulichen das Trainieren und Bereitstellen eines R-Modells in SQL Server.
