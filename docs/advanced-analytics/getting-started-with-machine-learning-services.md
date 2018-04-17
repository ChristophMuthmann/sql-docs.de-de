---
title: Erste Schritte mit Machine Learning in der SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 94f95b1a2ddaee32896d3a370338e53aded3ab99
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="getting-started-with-machine-learning-in-sql-server"></a>Erste Schritte mit Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft bietet einen integrierten, skalierbare Satz von Machine Learning-Lösungen für auf lokaler Ebene und in der Cloud:

+ **Integrierte**, da R oder Python in SQL Server ausgeführt werden können. Dadurch können Sie problemlos Enterprise Mergeprozesse für ETL und Berichterstattung in Data Science-Aufgaben wie das Feature engineering, Modellerstellung, und bewerten.
+ **Skalierbare**, weil der Data Scientist entwickeln und Testen Sie eine Lösung auf einem Laptop, und klicken Sie dann auf mehreren Plattformen für verteilte bereitstellen kann, oder die parallele Verarbeitung der Schlüsselvorgänge wie z. B. Modell trainieren und bewerten. Unterstützte Plattformen enthalten SQL Server unter Windows, Hadoop und Spark.

Dieser Artikel enthält Links zu Ressourcen für jedes Produkt in der Microsoft Machine Learning-Plattform.

## <a name="machine-learning-in-sql-server"></a>Machine learning-in SQL Server

+ SQL Server 2017

  Ab SQL Server 2017, können Sie jetzt Python-Code in SQL Server verwenden. Entsprechend die umfassendere Unterstützung für Lösungen in mehreren Sprachen (mit Weitere folgen!) und der Name wurde geändert in [!INCLUDE[rsql-productnamenew-md](../includes/rsql-productnamenew-md.md)]. Jetzt können Sie Machine Learning-Aufgaben automatisieren, mithilfe von SQL-Tools, R oder Python-Code auszuführen. Oder verwenden Sie die SQL Server-Computer als dem _computekontext_ für Aufträge, die von einem remote-Entwicklungsumgebung gestartet.

    + [Übersicht über die Architektur für Python in SQLServer](../advanced-analytics/python/architecture-overview-sql-server-python.md)
    + [Installieren von SQL Server 2017 Machine Learning-Services](install/sql-machine-learning-services-windows-install.md)

+ SQL Server 2016

  SQL Server 2016 unterstützt ausgeführten R-Code in SQL Server mithilfe von gespeicherten Prozeduren. Dies vereinfacht die Machine Learning-Aufgaben zu automatisieren, indem Sie mithilfe von SQL-Tools. Oder Sie können R-Code und eine remote Laptop oder R-Entwicklungsumgebung ausführen, bei der Verwendung von SQL Server-Computers als der _computekontext_.

  Diese Integration bietet Sicherheit für Ihre Daten und können Sie verwalten und Verteilen von r verwendete Ressourcen

    + [Getting Started Angebote SQL Server R Services](r/getting-started-with-sql-server-r-services.md)
    + [Installieren von SQL Server 2016 R Services](install/sql-r-services-windows-install.md)

## <a name="microsoft-machine-learning-server-microsoft-r-server"></a>Microsoft-Machine Learning-Server (Microsoft R Server)

Die Option zur Installation [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] finden Sie im SQL Server-2017 zur Unterstützung von Enterprise-Kunden, die verteilte, skalierbare-Machine learning-Aufträge ausgeführt werden soll, jedoch nicht, die die Integration mit dem SQL Server-Datenbankmodul, z. B. zur Verwendung von SQL Server benötigen. Kontexte.

Verwenden Sie die Option zum Installieren, in SQL Server 2016 [!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)].
  
  + [Willkommen Sie beim Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)
  
Sie können auch installieren [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)] oder [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] über plattformspezifische Installationsprogramme:

  + [Unter Windows installieren](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
  + [Unter Linux installieren](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-linux-install)
  + [Installieren Sie auf Hadoop](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-hadoop-install)

> [!IMPORTANT]
> Wenn Sie Python mithilfe von R-Server ausführen möchten, achten Sie auf die neueste Version installieren [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)], steht nur über [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)] Setup:
> 
>    + [Installieren von SQL Server 2017 Machine Learning-Server (eigenständig)](install/sql-machine-learning-standalone-windows-install.md) oder [Installieren von SQL Server 2016 R Server (eigenständig)](install/sql-r-standalone-windows-install.md).

## <a name="related-products"></a>Verwandte Produkte

+ [Einrichten eines Data Science-Clients](../advanced-analytics/r/set-up-a-data-science-client.md)

  Wenn Sie bereits eine des Machine learning-Server-Produkte installiert haben, bietet dieses Artikels finden Sie Informationen zum Einrichten von eines separaten Computers zum Entwickeln und Testen von Projektmappen, einschließlich Tools und erforderlichen Bibliotheken.

+ [Data Science Virtual Machines](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

  Schnelleinstieg Ihrer Eintragung in Machine learning-durch Abrufen dieser vollständige computerlernverfahren-Lösung über Azure Marketplace. Die Data Science-VM (häufig als "DSVM") umfasst SQL Server, Microsoft Machine Learning-Server und alle Entwicklungstools.
  
  Die neueste Version von Data Science Virtual Machine (DSVM) ausgeführt wird, auf Windows 2016 Preview Edition das Cleanup anpassbare Aussehen von Windows 10 bereitstellen. Es geht mit NVIDIA Treiber, CUDA Toolkit 8.0 und die NVIDIA CuDNN-Bibliothek für GPU-Arbeitslasten vorkonfiguriert.

## <a name="resources-for-learning"></a>Lernressourcen

+ [Machine Learning-Lernprogramme](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)

  Beginnen Sie hier eine Liste aller Ressourcen für den Einstieg in Machine Learning-Lösungen, die mit SQL Server 2016 und SQL Server-2017 gefunden.

### <a name="r-tutorials"></a>R-Lernprogramme

+ [SQL Server-R-Lernprogramme](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

   Erfahren Sie, wie R in SQL Server ausführen, erstellen und verwenden remote rechenkontexte oder Ausführen von Simulationen in R Verwendung von SQL Server.
   
   Enthält Lernprogramme für "alle bereitgestellten Code", damit Sie eine vollständige R-Lösung von SQL Server Management Studio ausführen können, ohne jemals eine R-IDE öffnen!

+ [Untersuchen von R und ScaleR in 25 kurzen Funktionen](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

   Haben Sie noch keine Erfahrung mit R? Fragen Sie sich, wie Microsoft R (oder "revoscaler"), standard R vergleicht? R Server und Machine Learning-Server finden Sie unter dieser Quick-beginnt.

### <a name="python-tutorials"></a>Python-Lernprogramme

+ [SQL Server-Python-Lernprogramme](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

  Weitere Informationen zum Ausführen von Python in [!INCLUDE[ssnoversion](../includes/ssnoversion.md)]. Erstellen eines Modells mithilfe von Python und verwenden sie zum Bewerten von SQL Server-Daten.

   Eine End-to-End-Lösung für SQL-Entwickler bietet gesamten Code, den Sie Python in SQL Server Management Studio ausführen müssen.


### <a name="product-samples-with-code"></a>Produktbeispiele mit code

Diese Lösungen aus der SQL Server-Entwicklungsteam in R oder Python ausgeführt, und veranschaulichen allgemeine Szenarien zum Integrieren von Machine Learning in Geschäftsanwendungen.

+ [Erstellen Sie eine intelligente Anwendung mit SQL Server und R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

+ [Erstellen Sie eine intelligente Anwendung mit SQL Server und Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

### <a name="data-science-solution-templates"></a>Data Science-Projektmappenvorlagen

Die Lösungsvorlagen aus dem Microsoft Data Science-Team darstellen vollständige Beispielprojektmappen für bestimmte Branchen oder Szenarien zugeschnitten sind. Sie sollen dienen als Bausteine können Sie eine schnelle Lösung zu implementieren oder um bewährte Methoden zu veranschaulichen. Jede Vorlage enthält Beispieldaten und anpassbare Code.

+ [Projektmappenvorlagen](../advanced-analytics/tutorials/data-science-scenarios-and-solution-templates.md)

## <a name="next-steps"></a>Nächste Schritte

[Erste Schritte mit SQL Server-Machine Learning-Services](../advanced-analytics/r/getting-started-with-sql-server-r-services.md)

[Erste Schritte mit Microsoft-Machine Learning-Server](../advanced-analytics/r/getting-started-with-microsoft-r-server-standalone.md)
