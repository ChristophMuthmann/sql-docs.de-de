---
title: SQL Server-Machine Learning-Dienste | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8c384b7fba553175767aaf7c439207771b31e6b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-machine-learning-services"></a>SQL Server-Machine Learning-Dienste

  SQL Server 2017 Machine Learning Dienste (zuvor SQL Server 2016 R Services) bietet eine Plattform zum Entwickeln und Bereitstellen von intelligenten Anwendungen, die neue Einblicke zu gewinnen. Sie können die umfassende und leistungsfähige Sprache „R“ und die zahlreichen Pakete aus der Community zum Erstellen von Modellen und Generieren von Vorhersagen mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten verwenden.
  
  Machine Learning in integriert ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie Analysen in der Nähe der Daten und beseitigen Sie die Kosten und Sicherheitsrisiken durch Verschieben von Daten.
  
SQL Server unterstützt die open Source-R-Sprache und einem umfassenden Satz von Tools und Technologien, die eine höhere Leistung, Sicherheit, Zuverlässigkeit und verwaltbarkeit bieten. Sie können R-Lösungen mithilfe der geeigneten, vertrauten SQL Tools bereitstellen und Ihre Produktionsanwendungen können die R-Laufzeitversion aufrufen und Abrufen von Vorhersagen und visuelle Elemente mit [!INCLUDE[tsql](../../includes/tsql-md.md)]. Erhalten Sie zudem die [Microsoft R](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) Bibliotheken für die Skalierung und Leistung von R-Lösungen, einschließlich "revoscaler", Revoscalepy und MicrososftML zu verbessern.
  
Über das SQL Server-Setup können Sie Server- und Clientkomponenten installieren.
  
## <a name="machine-learning-in-sql-server-2017"></a>Machine learning-in SQL Server-2017

+ Installieren Sie **Machine Learning-Services (Datenbankintern)** während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup So aktivieren Sie die sichere Ausführung von R oder Python-Skripts auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
    Wenn Sie diese Funktion auswählen, werden Erweiterungen im Datenbankmodul um die Ausführung von Code, in R oder Python unterstützen installiert. Ein neuer Dienst erstellt, die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], um die Verwaltung der Kommunikation zwischen den externen Laufzeiten und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.
  
+ Installieren Sie **Microsoft Machine Learning-Server (eigenständig)** auf einem separaten Computer, wenn Sie keine SQL Server als computekontext verwenden müssen. Machine Learning-Server enthält die gleichen Machine learning-Komponenten sowie das Paket Mrsdeploy für skalierbarer, verteilter Ausführung von Machine Learning-Aufträgen als Webdienst.
  
+    Installieren Sie [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client) auf Remotecomputern zum Entwickeln von Lösungen, die in SQL Server oder auf Machine Learning-Server unter Windows, Linux oder Hadoop bereitgestellt werden kann.

## <a name="machine-learning-in-sql-server-2016"></a>Machine learning-in SQL Server 2016

+ Installieren Sie **R Services (Datenbankintern)** während des Setups von SQL Server 2016, um sichere Ausführung von R-Skripts auf ermöglichen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
    Wenn Sie dieses Feature auswählen, erhalten Sie die Möglichkeit, die beim Ausführen von R-Skript mithilfe des SQL Servers als computekontext oder zum Ausführen von R-Skripts in einer gespeicherten Prozedur.
  
+   Installieren Sie **Microsoft R Server (eigenständig)** aus SQL Server 2016-Setup, um die R-Komponenten auf separaten Computern einrichten, die Sie für Developin R-Lösungen verwenden.


## <a name="which-type-of-machine-learning-service-do-i-need"></a>Welche Art von Machine Learning-Dienst benötige ich?

+ Wenn Sie zum Ausführen von R-Code in müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entweder mit gespeicherten Prozeduren oder mithilfe von SQL Server-Instanz als computekontext, müssen Sie installieren [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] beschriebenen [hier](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

+ Microsoft Machine Learning-Server (eigenständig) ist eine separate Option konzipiert, die für die Verwendung der [Microsoft R](https://docs.microsoft.com/r-server/r-reference/introducing-r-server-r-package-reference) und [Python-Bibliotheken verknüpft](../python/what-is-revoscalepy.md) auf einem Windows-Computer, die SQL Server nicht ausgeführt wird. Es ist, jedoch eine Enterprise Edition-Lizenz für SQL Server erforderlich.
    
    Es wird empfohlen, dass Sie Microsoft Machine Learning-Server (eigenständig) auf einem Laptop oder einem anderen Remotecomputer für die Entwicklung verwendet installieren und verwenden diesen Computer erstellen und Testen von Machine Learning-Lösungen, die mit einer Instanz von auf einfache Weise bereitgestellt werden können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Machine Learning Services ausgeführt wird \(In-Database\) oder einer anderen unterstützten Kontext zu berechnen.
  
    Sie können auch die **Mrsdeploy** Paket, das mit Machine Learning-Server zum Veröffentlichen und Verteilen von R und Python-Projekte als Webdienst installiert ist.

## <a name="additional-resources"></a>Weitere Ressourcen

+ [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    Beschreibt häufige Szenarios für die Verwendung von R mit SQL Server

+ [Einrichten von SQL Server R Services (In-Database)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    Installieren von R und die zugehörigen Datenbankkomponenten als Teil des SQL Server-setup
  
+ [Lernprogramme für SQL Server R](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Erfahren Sie, wie Sie SQL Server-Datenquellen in Ihrem R-Code erstellen und Remote Compute-Kontexte verwenden. Andere Tutorials für SQL-Entwickler veranschaulichen das Trainieren und Bereitstellen eines R-Modells in SQL Server.

