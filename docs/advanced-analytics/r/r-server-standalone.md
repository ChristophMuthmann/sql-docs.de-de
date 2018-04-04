---
title: SQL Server Machine Learning-Server (eigenständig) und R-Server (eigenständig) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 3f6bb60e639517e458684486f36123d47a68dbf9
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server Machine Learning-Server (eigenständig) und R-Server (eigenständig)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Ein eigenständiger Server ist eine Installation von Machine Learning-Komponenten formuliert als R und Python-Funktionen, die unabhängig von SQL Server-Datenbankmodul-Instanzen ausgeführt. Sie können einen eigenständigen Server alleine ohne Abhängigkeiten auf SQL Server installieren. Da ein eigenständiger Server unabhängig von SQL Server, Konfiguration und Verwaltung von Aufgaben wird und Tools-Zeichenfolgen einander ähnlicher auf eine nicht-SQL-Version von Machine Learning Server, auf dem Sie sich in vertraut machen können [in diesem Artikel](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server).

Das Ziel eines eigenständigen Machine Learning-Servers ist eine umfangreiche Entwicklungsumgebung mit verteilten und parallele Verarbeitung von R und Python-Arbeitslasten kleinen zu großen Datasets, mit dem proprietären Pakete und die Berechnung Module angeben mit dem Server installiert. Die R und Python-Pakete auf einem eigenständigen Server sind dieselben wie in einer Installation von SQL Server (In-Database) ermöglicht Codeportabilität und [Compute-Kontextwechsel](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

Der Hauptgrund für die Entwickler wählen Sie sich an ein eigenständigen Machine Learning-Server über den Arbeitsspeicher und Verarbeitung Einschränkungen von Open Source-R und Python hinaus verschoben. Eigenständige Server können laden und verarbeiten große Datenmengen auf mehrere Kerne und Aggregieren der Ergebnisse in einer einzigen konsolidierten Ausgabe. Die Funktionen und Algorithmen werden für Skalierung und Nützlichkeit Kundenszenarien entwickelt: Übermittlung von Vorhersageanalysen, statistischen Modellierung, datenvisualisierungen und führenden Algorithmen für maschinelles lernen in einer kommerziellen Serverprodukt entwickelt und unterstützt durch Microsoft.

Im Allgemeinen empfohlen, dass Sie zu behandeln (eigenständig) und (In-Database) Installationen als sich gegenseitig exklusiven zur Vermeidung von Ressourcenkonflikten, wenn Sie jedoch genügend Ressourcen, besteht keine Verbot für beide auf demselben physischen Computer installieren.

Sie können nur ein eigenständiger Server auf dem Computer haben: entweder [SQL Server 2017 Machine Learning-Server (eigenständig)](../install/sql-machine-learning-standalone-windows-install.md) oder [SQL Server 2016 R Server (eigenständig)](../install/sql-r-standalone-windows-install.md). Sie müssen eine Version manuell deinstallieren, bevor Sie eine andere Version installieren.

## <a name="components-of-a-standalone-server"></a>Komponenten von einem eigenständigen server

SQL Server 2016 ist nur in R. SQL Server-2017 unterstützt R und Python. Die folgende Tabelle beschreibt die Funktionen in den einzelnen Versionen.

| Komponente | Description |
|-----------|-------------|
| R-Pakete | ["Revoscaler"](revoscaler-overview.md) ist die primäre Bibliothek für skalierbare R mit Funktionen zur Bearbeitung von Daten, Transformation, Visualzation und Analyse.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) Machine Learning-Algorithmen zum Erstellen benutzerdefinierter Modelle für Textanalyse, bildanalysen und stimmungsanalyse hinzugefügt. <br/>[Mrsdeploy](operationalization-with-mrsdeploy.md) bietet web Service-Bereitstellung (in nur SQL Server 2017). <br/>[OlapR](how-to-create-mdx-queries-using-olapr.md) wird zum Angeben von MDX-Abfragen in R.|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open) ist Microsofts Open Source-Verteilung von r Das Paket und ein Interpreter sind enthalten. Verwenden Sie immer die Version des MRO im Setup-Programm gebündelt. |
| R-tools | R-Konsolenfensters und eingabeaufforderungen sind in einer Verteilung von R-Standardtools. Suchen sie im Ordner \Programme\Microsoft SQL Server\140\R_SERVER\bin\x64. |
| R-Beispiele und Skripts |  Open-Source-R und "revoscaler"-Pakete enthalten vordefinierte Datasets, damit Sie erstellen und Ausführen von Skript vorinstallierte Daten verwenden können. Suchen Sie unter \Programme\Microsoft SQL Server\140\R_SERVER\library\datasets und \library\RevoScaleR. |
| Python-Pakete | [Revoscalepy](../python/what-is-revoscalepy.md) ist die primäre Bibliothek für skalierbare Python mit Funktionen zur Bearbeitung von Daten, Transformation, Visualzation und Analyse. <br/>[Microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) Machine Learning-Algorithmen zum Erstellen benutzerdefinierter Modelle für Textanalyse, bildanalysen und stimmungsanalyse hinzugefügt.  |
| Python-tools | Das integrierte Python-Befehlszeilentool eignet sich für ad-hoc-Tests und Aufgaben. Suchen Sie das Tool im Verzeichnis \Programme\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | Anaconda ist eine Open-Source-Verteilung von Python und wichtige Pakete. |
| Python-Beispiele und Skripts | Wie bei R, umfasst Python integrierte Datasets und Skripts. Suchen Sie die Revoscalepy Daten im Verzeichnis \Programme\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-Packages\revoscalepy\data\sample-Daten. |
| Pre-tained Modelle in R und Python | Vorab trainierten Modelle werden unterstützt und auf einem eigenständigen Server verwendet werden kann, aber sie kann nicht mithilfe von SQL Server-Setup installiert werden. Das Setupprogramm für Microsoft Machine Learning-Server bietet die Modelle, die Sie installieren können kostenlos. Weitere Informationen finden Sie unter [Installation pretrained Machine Learning-Modellen in SQL Server](install-pretrained-models-sql-server.md). |

## <a name="get-started-step-by-step"></a>Erste Schritte schrittweise

Mit dem Setup starten Sie, fügen Sie die Binärdateien an Ihrem bevorzugten Entwicklungstool und Schreiben Sie das erste Skript.

### <a name="step-1-install-the-software"></a>Schritt 1: Installieren der software

Installieren Sie entweder eine dieser Versionen:

+ [SQL Server 2017 Machine Learning-Server (eigenständig)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016-R-Server (eigenständig) - nur R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Schritt 2: Konfigurieren Sie ein Entwicklungstool

Konfigurieren Sie Ihre Entwicklungstools, um die Machine Learning-Binärdateien zu verwenden. Weitere Informationen zu den Python, finden Sie unter [Link Python-Binärdateien](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Anweisungen zum Herstellen von Verbindungen in R Studio, finden Sie unter [verwenden unterschiedliche Versionen von R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) und zeigen Sie das Tool auf C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. Sie können auch versuchen, [R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

### <a name="step-3-write-your-first-script"></a>Schritt 3: Schreiben Sie das erste Skript.

R oder Python-Skript, die mithilfe von Funktionen aus "revoscaler" Revoscalepy und die Algorithmen für maschinelles lernen zu schreiben.
  
  + [Untersuchen Sie R und "revoscaler" in 25 Funktionen](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): beginnen mit grundlegenden R-Befehle und dann ausgeführt, der die verteilbaren RevoScaleR-Analysefunktionen, die hohen Leistung bereitstellen und Skalieren auf die R-Lösungen. Enthält parallelisierbare Versionen von vielen der beliebtesten R-Modellierpakete wie K-Means-Clustering, Entscheidungsstrukturen, Entscheidungswälder und Tools für die Datenbearbeitung.

  + [Schnellstart: Ein Beispiel der binären Klassifikation mit dem Microsoftml Python-Paket](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): erstellen ein binären klassifizierungsmodells des Typs mit den Funktionen von Microsoftml und das bekannte Breast Cancer Dataset.

Wählen Sie die beste Sprache für den Task aus. R ist am besten für statistische Berechnungen, die schwierig zu implementieren, verwenden SQL sind. Für setbasierte Vorgänge für Daten, nutzen die Leistungsfähigkeit des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um optimale Leistung zu erzielen. Verwenden Sie das in-Memory-Datenbankmodul für sehr schnelle Berechnungen über Spalten.

### <a name="step-4-operationalize-your-solution"></a>Schritt 4: Operationalisieren der Projektmappe

Eigenständige Server können die [operationalisierung](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) Funktionalität von der nicht-SQL-Branding [Microsoft Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Sie können konfigurieren, dass einen eigenständigen Server für operationalisierung, die Ihnen folgende Vorteile bietet: Bereitstellung und Hosting von Code, wie Webdienste, führen Sie die Diagnose "," Web Servicekapazität testen.

## <a name="see-also"></a>Siehe auch

 [SQL Server-Machine Learning-Services (Datenbankintern)](sql-server-r-services.md)

