---
title: Microsoft-Machine Learning-Dienste | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 10/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 23
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 246ea9f306c7d99b835c933c9feec695850a861b
ms.openlocfilehash: ddc9b3f17afe1f9d4c811e4a5871f48a3a08de7f
ms.contentlocale: de-de
ms.lasthandoff: 10/13/2017

---
# <a name="microsoft-machine-learning-services"></a>Microsoft Machine Learning-Dienste

Das Ziel von Microsoft Machine Learning-Services ist eine erweiterbare, skalierbare Plattform für das Integrieren von Machine Learning-Aufgaben und Tools in die Anwendungen, die Machine Learning-Dienste zur Nutzung bereitstellen. Die Plattform muss den Anforderungen aller Benutzer, die am Entwicklungs- und Data Analytics-Prozess beteiligt sind, vom Datenanalysten, bis zum Architekten und Datenbankadministrator, dienen.

Wesntliche Vorteile:

+ Skalierbare analytics
+ Mehrere Plattformen und rechenkontexte für Lösungen für "einmal schreiben, überall bereitstellen"
+ Verschieben von Daten und Daten Risiko vermeidet durch das Kombinieren von Analysen an den Daten
+ Datenanalysten können ihre eigenen Tools und Sprachen auswählen.
+ Microsofts Unternehmensfunktionen integriert die besten Funktionen der open-source
+ Vereinfachte administration
+ Einfacherer Einsatz und Nutzung von Vorhersagemodellen

## <a name="in-database-analytics-with-sql-server"></a>In der Datenbank-Analysen mit SQL Server

Mit SQL Server 2016 veröffentlichte Microsoft zwei Serverplattformen für Geschäftsanwendungen, welche die beliebte Open-Source Sprache R in sich integrieren:

+ **SQL Server R Services (In-Database)**, für die Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ **Microsoft R Server**, für Bereitstellungen für Großunternehmen R auf Windows- und Linux-Servern

Mit SQL Server 2017 wurden die Namen entsprechend geändert um der zusätzlichen Unterstützung der beliebten Sprache Python genüge zu tun. 

+ **SQL Server Machine Learning-Services (Datenbankintern)** unterstützt R und Python für Analysen in der Datenbank.
+ **Microsoft Machine Learning-Server** unterstützt R und Python-Bereitstellungen auf Windows-Servern mit Erweiterung auf anderen unterstützten Plattformen für spät 2017 geplant.

### <a name="benefits"></a>Vorteile

Microsoft Machine Learning Services bringt der COMPUTE-Klausel auf die Daten können R auf dem gleichen Computer wie die Datenbank ausgeführt. Es enthält den vertrauenswürdigen Launchpad-Dienst, der außerhalb ausgeführt wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verarbeiten und sicher mit R oder Python-Laufzeit kommuniziert.

Verwenden SQL Server-Machine Learning-Services, Sie können Modelle zu trainieren, generieren Plots bewerten und problemlos verschieben Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und R oder Python.

Datenanalysten, testen und Entwickeln von Lösungen, können Skripts senden, aus einer remote-Entwicklungscomputer Code sicher auf dem Server ausgeführt, oder sie können vollständige Lösungen mit SQL Server bereitstellen, durch das Einbetten von Machine Learning-Code in gespeicherten Prozeduren von SQL.

Bei der Installation von Machine Learning für SQL Server erhalten Sie eine Verteilung der open Source-R oder Python-Sprache sowie die skalierbare R und Python-Bibliotheken von Microsoft bereitgestellt. Das SQL Server-Datenbankmodul enthält auch neue Komponenten, die Konnektivität untermauern und vergewissern Sie sich schneller, sichereren Kommunikation mit externen Sprachen wie R oder Python.

### <a name="where-to-get-it"></a>Bezugsquelle

Finden Sie hier, um zu beginnen:

+ [SQL Server R Services](sql-server-r-services.md)
+ [SQL Server-Python-Dienste](../python/sql-server-python-services.md)
+ [Machine Learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> Unterstützung für Python wird nur in SQL Server-2017 bereitgestellt. 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>Machine Learning-Server (eigenständig) und Microsoft R Server (eigenständig)

Dieses eigenständige Serversystem unterstützt verteilte, skalierbare R-Lösungen auf mehreren Plattformen und verwendet mehrere Enterprise-Datenquellen, z. B. Linux und Hdinsight. Wenn Sie benötigen, um SQL Server zu integrieren, können Sie R-Server zum Aktivieren von schnelle Entwicklung, Bereitstellung und operationalisierung von Machine learning-Lösungen installieren. Sie können auch die Installationsprogramme R Server für ein upgrade einer SQL Server-Instanz zugeordneten R-Komponenten und die neueste Version von r

Bei der Installation von Microsoft Machine Learning-Servers mit 2017 von SQL Server-Setup können Sie auch bereitstellen und Nutzen von Python-Anwendungen.

Weitere Informationen finden Sie unter [Microsoft Machine Learning-Server](https://docs.microsoft.com/r-server/index).

## <a name="related-technologies"></a>Verwandte Technologien

Microsoft bietet umfassende Unterstützung für Machine Learning Ökosysteme, einschließlich Tools, Anbieter, verbesserte R und Python-Pakete, einen Cloud-Entwicklung und Dienstplattform und eine integrierte Entwicklungsumgebung.

### <a name="r-tools-for-visual-studio"></a>R-Tools für Visual Studio

Visual Studio stellt eine vollständige Entwicklungsumgebung für die Sprache R bereit. Das Plug-In enthält einen Editor, interaktive Fenster, Zeichnen, Debugger und mehr. Sie können .NET-Sprachen von R verwenden oder R aus .NET durch Open Source-Bibliotheken wie R.NET und rClr aufrufen.

Visual Studio verfügt auch über eine ausgezeichnete Python-Entwicklungsumgebung. Es gibt keine einfacheren Weg Machine Learning-Sprachen arbeiten, während die Verarbeitung fortgesetzt, um den Zugriff auf SQL-Datenbank-Entwicklungstools nutzen zu können.

Weitere Informationen finden Sie in den folgenden Themen:

+ [R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/)
+ [Python - Visual Studio](https://www.visualstudio.com/vs/python/)

### <a name="azure-machine-learning"></a>Azure Machine Learning

Wenn Sie Ihren eigenen Arbeitsbereich in Azure Machine Learning Studio erstellen, müssen Sie den Zugriff auf mehr als 400 vorab geladene R-Pakete. Sie können auch auswählen, wenn einem Experiment zu, mit dem R erstellen, R, die mit einem Standardverteilungspunkt CRAN R oder Microsoft R Open bereitstellen. Sie können auch eigene R-Pakete erstellen und Hochladen in Azure können Sie als benutzerdefinierte Module auszuführen.

Weitere Informationen finden Sie in den folgenden Ressourcen:

+ [Erweitern Ihres Experiments mit R](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)
+ [Benutzerdefinierte R-Module in Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)

Viele der in Azure ML bereitgestellten Algorithmen sind jetzt im Microsoft Machine Learning Services als Teil des Pakets MicrosoftML enthalten. Weitere Informationen finden Sie unter [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).

Azure Machine Learning ist eine andere ideale Plattform Datenanalysten und Entwickler, die zum Erstellen, Trainieren und Bereitstellen von Modellen mithilfe von Webdiensten erforderlich. Sie können Lösungen zum Veröffentlichen der [Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning).

### <a name="data-science-virtual-machines"></a>Data Science Virtual Machines

Sie können eine vorinstallierte und vorkonfigurierte Version von [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] in Microsoft Azure bereitstellen. Dies erleichtert die ersten Schritte beim Auswerten und Modellieren von Daten in der Cloud, ohne ein vollständig konfiguriertes System lokal einrichten zu müssen.

Der Azure Marketplace enthält mehrere virtuelle Computer, die Data Science unterstützen:

+ Die **Microsoft Data Science Virtual Machine** wurde mit Microsoft R Server, Python (Anaconda-Verteilung), einem Jupyter Notebook-Server, Visual Studio Community Edition, Power BI Desktop, dem Azure SDK und SQL Server Express Edition konfiguriert.

+ **Microsoft R Server 2016 für Linux** enthält die neueste Version von R Server (Version 9.0.1). Separate virtuelle Computer sind für CentOS Version 7.2 und Ubuntu Version 16.04 verfügbar.

+ Die **R Server nur SQL Server 2016 Enterprise** virtuelle Computer umfasst, ein eigenständiges Installationsprogramm für R-Server 9.0.1, der das neue Lizenzierungsmodell moderne Softwarelebenszyklus unterstützt.

> [!TIP]
> Die neue [Data Science VM für Windows Server 2016](http://aka.ms/dsvm/win2016) GPU-Versionen der beliebten umfassenden lernen Frameworks wie z. B. CNTK enthält. Vorinstallierte Tools umfassen die NVIDIA GPU-Treiber, CUDA Toolkit 8.0 und die NVIDIA CuDNN-Bibliothek für GPU-Arbeitslasten. In wenigen Minuten können Sie eine vollständige Umgebung zum Erstellen von Modellen umfassenden lernen, die auf der CPU oder CPU und GPU ausgeführt werden können.

## <a name="next-steps"></a>Nächste Schritte

[Erste Schritte mit Machine Learning-Dienste](getting-started-with-sql-server-r-services.md)

[Erste Schritte mit Machine Learning-Server](getting-started-with-microsoft-r-server-standalone.md)

[Installieren Sie das SQL Server-Datenbankmodul](../../database-engine/install-windows/install-sql-server-database-engine.md)

