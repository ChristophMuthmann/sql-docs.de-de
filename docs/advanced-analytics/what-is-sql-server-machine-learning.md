---
title: Was ist SQL Server-Machine Learning-Services? | Microsoft Docs
ms.date: 03/07/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: 
ms.openlocfilehash: ccba60d0a3e0fe45f82215a045e53a265d6c0a92
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="what-is-sql-server-machine-learning-services"></a>Was ist SQL Server-Machine Learning-Services?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server-Machine Learning-Services ist eine eingebettete predictive Analyse- und Data Science-Engine, die R und Python-Code in einer SQL Server-Datenbank als gespeicherte Prozeduren, als T-SQL-Skript, die mit R oder Python-Anweisungen oder R oder Python enthält Code ausgeführt werden kann T-SQL. 

Der Schlüssel des wertbeitrags von Machine Learning Services ist die Leistungsfähigkeit des zugehörigen proprietären Pakete zum Übermitteln von erweiterter Analysen mit Skalierung und die Möglichkeit, schalten Sie Berechnungen und Verarbeitung an, in dem sich die Daten befinden, Hierdurch entfällt die Notwendigkeit zum Abruf von Daten über die Netzwerk.

Es gibt zwei Optionen für die Verwendung von Machine Learning-Funktionen in SQL Server: 

+ [**SQL Server Machine Learning-Services (Datenbankintern)** ](r/sql-server-r-services.md) innerhalb der Datenbankmodulinstanz, in dem das Berechnungsmodul vollständig in das Datenbankmodul integriert ist. Die meisten Installationen werden diese Option.
+ [**SQL Server Machine Learning-Server (eigenständig)** ](r/r-server-standalone.md) ist eine nicht-SQL-Installation. Obwohl Sie SQL Server-Setup verwenden, um den Server zu installieren, wird diese vollständig aus SQL Server entkoppelt. Ist funktionell äquivalent zu nicht-SQL [Microsoft Machine Learning-Server für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

## <a name="r-and-python-packages"></a>R und Python-Pakete

Unterstützung für jede Sprache ist durch proprietäre Microsoft-Pakete, die zum Erstellen und Trainieren von Modellen verschiedener Typen, Bewerten von Daten und parallele Verarbeitung, die mit der zugrunde liegenden Systemressourcen verwendet.

Da die proprietäre Pakete auf Open Source-R und Python-Verteilungen erstellt werden, Skript oder Code, die Sie in SQL Server ausführen kann auch Basis Funktionen aufrufen und Drittanbieterpakete, die kompatibel mit der Sprachversion, die in SQL Server bereitgestellten (Python 3.5 und aktuelle Versionen von R, derzeit 3.3.3).

| R  | Python | Description |
|-----------|----------------|-------------|
| [RevoScaleR](r/revoscaler-overview.md) | [revoscalepy](python/what-is-revoscalepy.md)   | Funktionen in diesen Bibliotheken gehören zu den am häufigsten verwendeten werden. Datentransformationen und Manipulation, statistische Zusammenfassung, Visualisierung und viele Formen der Modellierung und Analysen sind in diesen Bibliotheken gefunden. Darüber hinaus verteilt Funktionen in diesen Bibliotheken automatisch Workloads auf verfügbaren Kerne für die parallele Verarbeitung, die Möglichkeit, Teile dieser Daten zu arbeiten, die koordiniert und vom Berechnungsmodul verwaltet werden. |
| [MicrosoftML](using-the-microsoftml-package.md) | [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Führende Algorithmen für maschinelles lernen für Image-merkmalbereitstellung, klassifizierungsprobleme und vieles mehr. |
| [olapR](r/how-to-create-mdx-queries-using-olapr.md) | none | Erstellen oder eine MDX-Abfrage in R-Skript ausführen.
| [sqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) | none | Funktionen für das zusammensetzen von R-Skripts in einer T-SQL-Prozedur, eine gespeicherte Prozedur mit einer Datenbank registrieren und Ausführen der gespeicherten Prozedur aus einem R-Entwicklungsumgebung.
| [mrsdeploy](operationalization-with-mrsdeploy.md) | none | Verwendet in erster Linie in einer nicht-SQL-Installation von Machine Learning-Server, z. B. die [(eigenständig) Version](r/r-server-standalone.md). Verwenden Sie dieses Paket bereitstellen und Webdienste hosten, erstellen mit horizontaler Skalierung Topologien mit dedizierten Web und Serverknoten, Umschalten zwischen lokalen und Remotesitzungen, Diagnose und vieles mehr ausführen. Für die Installation (In-Database), verwenden Sie dieses Paket in eine Client-Kapazität: z. B. auf einen Webdienst auf einem Remoteserver zugreifen dedizierte nur Machine Learning-Services-arbeitsauslastungen ausgeführt. |

Portabilität von Ihrem benutzerdefinierten R und Python-Code adressiert ist, über die paketverteilung und Interpreter, die in mehrere Produkte integriert werden. Die gleichen Pakete, die in SQL Server ausgeliefert sind auch verfügbar in verschiedene andere Microsoft-Produkte und Dienste, einschließlich einer nicht-SQL-Version aufgerufen [Microsoft Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/). Kostenlose Clients, die unsere R und Pyton Interpreter enthalten gehören [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) und die [Python-Bibliotheken](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

Pakete und Interpreter stehen auch auf mehreren [virtuellen Azure-Computern](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux), Azure Machine Learning und Azure-Diensten wie [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight). 


## <a name="use-cases"></a>Einsatzgebiete

**In der Datenbank analytics**

Entwickler und Wirtschaftsanalytiker haben häufig Code über eine lokale SQL Server-Instanz ausgeführt wird. Wenn Sie z. B. SQL Server und einer IDE haben [Visual Studio mit R](https://docs.microsoft.com/visualstudio/rtvs/) oder [Visual Studio mit Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio) auf demselben Computer erstellen, Trainieren und lokal Testen von Modellen in beiden Sprachen. Lokaler Zugriff vereinfacht paketverwaltung: als Administrator können Sie zusätzliche Drittanbieter-Pakete, die mithilfe der integrierten Berechtigungen für diese Rolle laden.

Die am häufigsten verwendete Ansatz für die Analyse in der Datenbank ist die Verwendung [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) , R oder Python-Skript auszuführen. Die Lernprogramme in aufgeführten [nächste Schritte](#next-steps) beginnen.

**Client / Server-Konfigurationen**

Über jede Clientarbeitsstation, die eine IDE aufweist, installieren [Microsoft R-Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) oder die [Python-Bibliotheken](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter), und klicken Sie dann Code schreiben, der die Ausführung wird (als bezeichnet eine *remote computekontext*) um Daten und Vorgänge mit einem SQL-Remoteserver. 

Auf ähnliche Weise, wenn Sie die Developer Edition verwenden, Sie erstellen Lösungen auf einer Clientarbeitsstation unter Verwendung des gleichen Bibliotheken und Interpreter, und klicken Sie dann bereitstellen können Produktionscode auf SQL Server Machine Learning-Services (Datenbankintern). 

## <a name="version-history"></a>Verlauf-Version

SQL Server 2017 Machine Learning Services ist die nächste Generation von SQL Server 2016 R Services verbessert, um Python einzuschließen. In der folgenden Tabelle wird eine vollständige Liste aller Versionen, vom Beginn bis auf die aktuelle Version. 

| Produktname | Modulversion | Veröffentlichungsdatum |
|--------------|---------|--------------|
| SQL Server 2017 Machine Learning Services (Datenbankintern) | R Server 9.2.1 <br/> Python Server 9.2 | Oktober 2017 |
| SQL Server 2017 Machine Learning-Server (eigenständig) | R Server 9.2.1 <br/> Python Server 9.2 | Oktober 2017 |
| SQL Server 2016 R Services (Datenbankintern) | R Server 9.1  | Juli 2017  |
| SQL Server 2016-R-Server (eigenständig)  |  R Server 9.1 | Juli 2017 |



## <a name="documentation-for-each-version"></a>Dokumentation für die einzelnen Versionen

Neueren Versionen von SQL Server-Dokumentation werden die Unabhängigkeit von der Version. Für SQL Server Machine Learning-Dienste ist Python nur verfügbar in 2017 und höher, während der R-Unterstützung in allen Versionen ist. Sofern nicht anders angegeben, können Sie davon ausgehen, dass R-Dokumentation 2016 und 2017 Versionen angewendet.


## <a name="related-machine-learning-products"></a>Verwandte Machine learning-Produkte

 +  [Bereitstellen von virtuellen Azure-Computer](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure Marketplace enthält mehrere Images für virtuelle Computer, die Machine Learning-Server oder R Server einschließen. Erstellen einer virtuellen Maschine in Microsoft Azure ist die schnellste Möglichkeit, um Entwicklung und Bereitstellung von Vorhersagemodellen zu erhalten. Bilder verfügen über Funktionen für die Skalierung und Freigabe bereits konfiguriert ist, dem leichter Analytics in Anwendungen eingebettet und Back-End-Systeme integriert werden kann.

+ [Data Science Virtual Machines](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)

  Die neueste Version der Data Science Virtual Machine enthält Machine Learning-Server, SQL Server, und ein Array der beliebtesten Tools für maschinelles lernen, alle vorinstalliert und getestet. Jupyter Notizbüchern erstellen, Entwickeln von Projektmappen in Julia und GPU-aktivierte umfassenden lernen Bibliotheken wie MXNet, CNTK und TensorFlow verwenden.

<a name="next-steps"></a>

## <a name="next-steps"></a>Nächste Schritte

**Schritt 1:** installieren und konfigurieren Sie die Software. 

+ [Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern)](install/sql-machine-learning-services-windows-install.md)

**Schritt 2:** erste Schritte mit Code mit einer der folgenden Lernprogramme:

+ [Lernprogramm: Ausführen von Python in T-SQL](tutorials/run-python-using-t-sql.md)
+ [Lernprogramm: Ausführen von R in T-SQL](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

**Schritt 3:** Ihrer bevorzugten R und Python-Pakete hinzufügen und verwenden sie zusammen mit Paketen, die von Microsoft bereitgestellten

+ [Verwaltung von R-Paket für SQL Server](r/r-package-management-for-sql-server-r-services.md)