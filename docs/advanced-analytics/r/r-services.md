---
title: Microsoft-Machine Learning-Dienste | Microsoft Docs
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: "23"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: bc3d80c01bc16d6d89bbf3e97ddf88089e9379fd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="microsoft-machine-learning-services"></a>Microsoft Machine Learning Services

Das Ziel von Microsoft Machine Learning-Services ist eine erweiterbare, skalierbare Plattform für das Integrieren von Machine Learning-Aufgaben und Tools in die Anwendungen, die Machine Learning-Dienste zu nutzen bereitstellen. Die Plattform muss die Anforderungen aller Benutzer Entwicklungs- und das Data Analytics-Prozess Beteiligten aus Datenanalysten, Architekten und Datenbankadministratoren dienen.

Wichtige Vorteile:

+ Skalierbare analytics
+ Mehrere Plattformen und rechenkontexte für Lösungen für "code einmal, überall bereitstellen"
+ Verschieben von Daten und Daten Risiko vermeidet durch das Kombinieren von Analysen an den Daten
+ Datenanalysten können ihre eigenen Tools und Sprachen auswählen.
+ Microsofts Unternehmensfunktionen integriert die besten Funktionen der open-source
+ Vereinfachte administration
+ Einfach bereitgestellt und Nutzen von Vorhersagemodellen

## <a name="in-database-analytics-with-sql-server"></a>In der Datenbank-Analysen mit SQL Server

In SQL Server 2016 gestartet Microsoft zwei Serverplattformen für Geschäftsanwendungen Integrieren der beliebten open Source-R-Sprache:

+ **SQL Server R Services (In-Database)**, für die Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ **Microsoft R Server**, für Bereitstellungen für Großunternehmen R auf Windows- und Linux-Servern

In SQL Server 2017 wurde der Name entsprechend der Unterstützung für die Sprache der beliebten Python geändert.

+ **SQL Server Machine Learning-Services (Datenbankintern)** unterstützt R und Python für die Analyse in der Datenbank.
+ **Microsoft Machine Learning-Server** R und Python-Bereitstellungen auf Windows, Linux und HDInsight Spark und Hadoop-Clustern unterstützt.

### <a name="benefits"></a>Vorteile

Microsoft Machine Learning Services bringt der COMPUTE-Klausel auf die Daten können R auf dem gleichen Computer wie die Datenbank ausgeführt. Es enthält den Launchpad-Dienst, der außerhalb ausgeführt wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verarbeiten und sicher mit R oder Python-Laufzeit kommuniziert.

Verwenden SQL Server-Machine Learning-Services, Sie können Modelle zu trainieren, generieren Plots bewerten und sicher verschieben Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und R oder Python.

Datenanalysten, testen und Entwickeln von Lösungen, können Skripts von einem Remotecomputer aus zum Entwickeln Computer senden und ihren Code auf dem Server ausführen, ohne Daten zu verschieben. Entwickler können vollständige Lösungen durch Einbetten von Machine Learning-Code in gespeicherten Prozeduren von SQL mit SQL Server bereitstellen.

Bei der Installation von Machine Learning für SQL Server erhalten Sie eine Verteilung der open Source-R oder Python-Sprache sowie die skalierbare R und Python-Bibliotheken von Microsoft bereitgestellt. Das SQL Server-Datenbankmodul enthält auch neue Komponenten, die Konnektivität untermauern und vergewissern Sie sich schneller, sichereren Kommunikation mit externen Sprachen wie R oder Python.

### <a name="where-to-get-it"></a>Bezugsquelle

Finden Sie hier, um zu beginnen:

+ [SQL Server R Services](sql-server-r-services.md)
+ [SQL Server Python Services](../python/sql-server-python-services.md)
+ [Machine Learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> Unterstützung für Python wird nur in SQL Server-2017 bereitgestellt. 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>Machine Learning-Server (eigenständig) und Microsoft R Server (eigenständig)

Dieses eigenständige Serversystem unterstützt verteilte, skalierbare R-Lösungen auf mehreren Plattformen und verwendet mehrere Enterprise-Datenquellen, z. B. Linux und HDInsight. Wenn Sie benötigen, um SQL Server zu integrieren, können Sie R-Server zum Aktivieren von schnelle Entwicklung, Bereitstellung und operationalisierung von Machine learning-Lösungen installieren. Sie können auch die Installationsprogramme R Server für ein upgrade einer SQL Server-Instanz zugeordneten R-Komponenten und die neueste Version von r

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

Wenn Sie Ihren eigenen Arbeitsbereich in Azure Machine Learning Studio erstellen, erhalten Sie Zugriff auf mehr als 400 vorab geladene R-Pakete. Sie können auch auswählen, wenn einem Experiment zu, mit dem R erstellen, R, die mit einem Standardverteilungspunkt CRAN R oder Microsoft R Open bereitstellen. Sie können auch eigene R-Pakete erstellen und Hochladen in Azure können Sie als benutzerdefinierte Module auszuführen.

Viele der in Azure ML bereitgestellten Algorithmen sind jetzt im Microsoft Machine Learning Services als Teil des Pakets MicrosoftML enthalten. Weitere Informationen finden Sie unter [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).

Azure Machine Learning ist eine andere ideale Plattform Datenanalysten und Entwickler, die zum Erstellen, Trainieren und Bereitstellen von Modellen mithilfe von Webdiensten erforderlich. Sie können Lösungen zum Veröffentlichen der [Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning).

Weitere Informationen zu aufregend Änderungen im Azure Machine Learning-Dienst zur Unterstützung von Experten Datenanalysten finden Sie in diese Ressourcen zu:

+ [Was ist Azure Machine Learning?](https://docs.microsoft.com/azure/machine-learning/preview/overview-what-is-azure-ml)
+ [Modell-Management-Funktionen](https://docs.microsoft.com/azure/machine-learning/preview/model-management-overview)

### <a name="data-science-virtual-machines"></a>Data Science Virtual Machines

Sie können eine vorinstallierte und vorkonfigurierte Version von [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] in Microsoft Azure bereitstellen. Dies erleichtert die ersten Schritte beim Auswerten und Modellieren von Daten in der Cloud, ohne ein vollständig konfiguriertes System lokal einrichten zu müssen.

Azure Marketplace enthält mehrere virtuelle Maschinen, die Data Science unterstützen.

+ Die **Microsoft Data Science Virtual Machine** mit Machine Learning-Servers konfiguriert ist, sowie Python (Anaconda-Verteilung), einem Jupyter Notebook-Server, Visual Studio Community Edition, Power BI Desktop, das Azure SDK und SQL Server.

    Die neue [Data Science VM für Windows Server 2016](http://aka.ms/dsvm/win2016) GPU-Versionen der beliebten umfassenden lernen Frameworks wie z. B. CNTK enthält. Vorinstallierte Tools umfassen die NVIDIA GPU-Treiber, CUDA Toolkit 8.0 und die NVIDIA CuDNN-Bibliothek für GPU-Arbeitslasten. In wenigen Minuten können Sie eine vollständige Umgebung zum Erstellen von Modellen umfassenden lernen, die auf der CPU oder CPU und GPU ausgeführt werden können.

+ Für R-Server oder Machine Learning-Server empfehlen wir die Microsoft Machine Learning Server 2017, für Linux oder für 2016 WindowsServer.

+ Um ein Azure-Image mit SQL Server-Machine Learning zu erhalten, sollten alle von der virtuellen Maschine angeboten, die implizit enthalten **SQL Server-2017**. Wenn Sie das Bild auswählen, befolgen Sie die zusätzlichen Empfehlungen zu Ebene für Ebene und Dienst, um sicherzustellen, dass die VM Machine Learning-Arbeitslasten unterstützen kann.

## <a name="next-steps"></a>Nächste Schritte

[Erste Schritte mit Machine Learning-Dienste](getting-started-with-sql-server-r-services.md)

[Erste Schritte mit Machine Learning-Server](getting-started-with-microsoft-r-server-standalone.md)

[Installieren Sie das SQL Server-Datenbankmodul](../../database-engine/install-windows/install-sql-server-database-engine.md)
