---
title: SQLServer Machine Learning und R Services (Datenbankintern) | Microsoft Docs
ms.date: 03/16/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Active
ms.openlocfilehash: 0d5bb56717eefa50a219db051eb611a82974a0bc
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQLServer Machine Learning und R Services (Datenbankintern)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Eine Installation in der Datenbank von Machine Learning operiert innerhalb des Kontexts von einer SQL Server-Datenbank-Modulinstanz Bereitstellen von R und Python externes Skript-Unterstützung für Residente Daten in der SQL Server-Instanz. Machine Learning in integriert ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie Analysen in der Nähe der Daten und beseitigen Sie die Kosten und Sicherheitsrisiken durch Verschieben von Daten.

Da das Datenbankmodul mit mehreren Instanzen handelt, können Sie mehrere Instanzen von Analysen in der Datenbank, oder sogar älteren und neueren Versionen Seite-an-Seite installieren. Optionen sind entweder [SQL Server 2017 Machine Learning Services (Datenbankintern)](../install/sql-machine-learning-standalone-windows-install.md) mit R und Python oder [SQL Server 2016 R Services (In ändern)](../install/sql-r-standalone-windows-install.md) mit nur R. 

Machine Learning-Komponenten können ebenfalls als Unabhängigkeit von der Instanz installiert werden [eigenständigen Servern](r-server-standalone.md). Im Allgemeinen empfohlen, dass Sie zu behandeln (eigenständig) und (In-Database) Installationen als sich gegenseitig exklusiven zur Vermeidung von Ressourcenkonflikten, wenn Sie jedoch genügend Ressourcen stehen keine verboten für beide auf demselben physischen Computer installieren.

## <a name="choosing-between-in-database-and-standalone-analytics"></a>Entscheidung zwischen in-Database und eigenständige Analysen

Grundlegendes zu Ihrer entwicklungsanforderungen, können Sie entscheiden (In-Database) und (eigenständig) fast erreicht wird. Ein eigenständiger Server ist einfacher, konfigurieren und verwalten, wenn maximale Flexibilität wie diese verwendet werden soll, oder wenn Sie auch eine Verbindung mit einer Vielzahl von Datenquellen außerhalb von SQL Server herstellen möchten. 

In der Datenbank Analytics sind für umfassende Integration in den Daten in SQL Server vorgesehen. Sie können die T-SQL-Abfragen schreiben, die R oder Python-Funktionen aufrufen, und führen Sie das Skript in SQL Server Management Studio oder beliebige Tools oder die app für externe oder eingebettete T-SQL verwendet. Wenn Sie für die Ausführung von R oder Python-Code im müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entweder mit gespeicherten Prozeduren oder mithilfe von SQL Server-Instanz als der [computekontext](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context), müssen Sie in der Datenbank Analytics installieren. Diese Option bietet maximale Sicherheit und Integration in SQL Server-Tools.

Sowohl in der Datenbank und eigenständige Server können die Arbeitsspeicher und Verarbeitung Einschränkungen von Open Source-R und Python verringern. Beide Optionen werden die gleichen Pakete und Tools, mit der Möglichkeit zum Laden und verarbeiten große Datenmengen auf mehrere Kerne und Aggregieren der Ergebnisse in einer einzigen konsolidierten Ausgabe enthalten. Die Funktionen und Algorithmen werden für Skalierung und Nützlichkeit Kundenszenarien entwickelt: Übermittlung von Vorhersageanalysen, statistischen Modellierung, datenvisualisierungen und führenden Algorithmen für maschinelles lernen in einer kommerziellen Serverprodukt entwickelt und unterstützt durch Microsoft. 

## <a name="components-of-an-in-database-installation"></a>Komponenten einer in-Database-installation

SQL Server 2016 ist nur in R. SQL Server-2017 unterstützt R und Python. Die folgende Tabelle beschreibt die Funktionen in den einzelnen Versionen. Mit Ausnahme von der SQL Server Launchpad-Dienst diese Tabelle ist identisch mit dem Kennwort gemäß der [eigenständige Server-Artikel](r-server-standalone.md).

| Komponente | Description |
|-----------|-------------|
| SQL Server Launchpad-Dienst | Ein Dienst, der Kommunikation zwischen den externen R und Python-Laufzeiten verwaltet und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz. |
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

+ [SQL Server 2017 Machine Learning Services (Datenbankintern)](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016-R Services (Datenbankintern) - nur R](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Schritt 2: Konfigurieren Sie ein Entwicklungstool

Konfigurieren Sie Ihre Entwicklungstools, um die Machine Learning-Binärdateien zu verwenden. Weitere Informationen zu den Python, finden Sie unter [Link Python-Binärdateien](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Anweisungen zum Herstellen von Verbindungen in R Studio, finden Sie unter [verwenden unterschiedliche Versionen von R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) und zeigen Sie das Tool auf C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. Sie können auch versuchen, [R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

Datenanalysten verwenden R oder Python in der Regel auf ihren eigenen Arbeitsstationen Laptop oder Entwicklungscomputer zum Durchsuchen von Daten, und erstellen und Optimieren von Vorhersagemodellen, bis ein geeignetes Vorhersagemodell erreicht ist. 

Analysevorgänge in der Datenbank in SQL Server ist es nicht erforderlich, um diesen Prozess zu ändern. Nach Abschluss der Installation können Sie R oder Python-Code ausführen, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entweder lokal oder Remote:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **Die IDE gewünscht**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] -Clientkomponenten stellen für Datenanalysten sämtliche Tools bereit, die zum Experimentieren und Entwickeln erforderlich sind. Zu diesen Tools zählen die R-Laufzeitversion, die mathematische Kernelbibliothek von Intel zur Leistungssteigerung von R-Standardfunktionen sowie eine Reihe von erweiterten R-Paketen, die das Ausführen von R-Code in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützen.  

+ **Arbeiten Sie Remote oder lokal**. Datenanalysten können eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und dem Client die Daten wie gewohnt zur lokalen Analyse vorlegen. Jedoch eine bessere Lösung ist die Verwendung der **"revoscaler"** oder **Revoscalepy** APIs Push Berechnungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer kostenintensive und unsichere datenbewegungen zu vermeiden.

+ **Einbetten von R oder Python-Skripts in [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozeduren**. Wenn Ihr Code vollständig optimiert ist, binden Sie diese in einer gespeicherten Prozedur vermeiden unnötige datenbewegungen und Optimieren von Data-Verarbeitungsaufgaben an.

### <a name="step-3-write-your-first-script"></a>Schritt 3: Schreiben Sie das erste Skript.

Rufen Sie R oder Python-Funktionen in T-SQL-Skript ein:
  
  + [R: Verwenden des R-Codes in Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R: Datenbankinterne Analysen für SQL-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python: Ausführen von Python mit T-SQL](../tutorials/run-python-using-t-sql.md)
  + [Python: Datenbankinterne Analysen für SQL-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Wählen Sie die beste Sprache für den Task aus. R ist am besten für statistische Berechnungen, die schwierig zu implementieren, verwenden SQL sind. Für setbasierte Vorgänge für Daten, nutzen die Leistungsfähigkeit des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um optimale Leistung zu erzielen. Verwenden Sie das in-Memory-Datenbankmodul für sehr schnelle Berechnungen über Spalten.

### <a name="step-4-optimize-your-solution"></a>Schritt 4: Optimieren Sie Ihre Lösung

Wenn das Modell für die Skalierung auf Enterprise-Daten ist, funktioniert der Data Scientist oft mit dem Datenbankadministrator oder der SQL-Entwickler Prozesse wie z. B. zu optimieren:

+ Featureentwicklung
+ Als "Erfassung" Daten und die Datentransformation
+ Bewertung

Bisher mussten Datenanalysten verwenden R Probleme mit der Leistung und Skalierung, insbesondere wenn Sie große Datasets verwendet. Das liegt daran Implementierung des allgemeinen Laufzeitmoduls nur einen einzelnen Thread und nur die Datasets, die in den verfügbaren Arbeitsspeicher auf dem lokalen Computer entsprechen aufnehmen kann. Integration mit SQl Server-Machine Learning-Services stellt mehrere Funktionen für eine bessere Leistung, mehr Daten bereit:

+ **"Revoscaler"**: Diese R-Paket enthält die Implementierung einiger der beliebtesten R-Funktionen neu gestaltet, um die Parallelität und Skalierung bereitzustellen. Das Paket enthält auch Funktionen, die die Leistung und Skalierung weiter erhöhen, indem Berechnungen mittels Push auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer übertragen werden, der in der Regel über wesentlich mehr Arbeitsspeicher und Rechenleistung verfügt.

+ **revoscalepy**. Diese Python-Clientbibliothek in SQL Server 2017 implementiert die am häufigsten verwendeten Funktionen im "revoscaler", z. B. remote rechenkontexte, und viele Algorithmen, die unterstützt verteilte Verarbeitung.

**Ressourcen**

+ [Fallstudie zur Leistung](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R- und Datenoptimierung](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>Schritt 5: Bereitstellen und nutzen

Nachdem das Skript oder das Modell für die Produktion bereit ist, kann ein Datenbankentwickler den Code oder das Modell in einer gespeicherten Prozedur einbetten, sodass die gespeicherte R oder Python-Code aus einer Anwendung aufgerufen werden kann. Das Speichern und Ausführen von R über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet viele Vorteile: Sie können die komfortable [!INCLUDE[tsql](../../includes/tsql-md.md)] -Benutzeroberfläche verwenden. Außerdem erfolgen sämtliche Berechnungen in der Datenbank, wodurch unnötige Datenbewegungen vermieden werden.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **Sichere und erweiterbare**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verwendet eine neue erweiterbarkeitsarchitektur, die das Datenbankmodul gewährleistet die Sicherheit und R und Python-Sitzungen isoliert. Sie haben auch die Kontrolle über Benutzer, die Skripts ausgeführt werden kann, und Sie können angeben, welche Datenbanken in Code zugegriffen werden können. Sie können den Umfang der Ressourcen, die der Laufzeit zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die gesamtleistung des Servers gefährden steuern.

+ **Planung und Überwachung**. Bei der Ausführung von externen Skripts für Aufträge im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie steuern und Überwachen der Daten, die von Datenanalysten verwendet. Sie können auch planen, Aufträge und Workflows erstellen, die externe R oder Python-Skripts, wie Sie jede andere T-SQL-Auftrag oder die gespeicherte Prozedur planen möchten.

Um die Vorteile der ressourcenverwaltung und Sicherheitsupdate-Funktionen in SQL Server nutzen zu können, kann der Bereitstellungsprozess diese Aufgaben sind:

+ Konvertieren von Yourcode an eine Funktion, die optimal in einer gespeicherten Prozedur ausgeführt werden kann
+ Einrichten der Sicherheit und Pakete, die von einer bestimmten Aufgabe verwendet Sperren
+ Aktivieren der Ressourcenkontrolle (erfordert die Enterprise Edition)

**Ressourcen**

+ [Ressourcenkontrolle für R](resource-governance-for-r-services.md)
+ [R-Paketverwaltung für SQLServer](r-package-management-for-sql-server-r-services.md)

## <a name="see-also"></a>Siehe auch

 [SQLServer Machine Learning und R-Server (eigenständig)](sql-server-r-services.md)
