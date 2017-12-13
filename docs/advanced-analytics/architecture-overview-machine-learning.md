---
title: "Übersicht über die Architektur für SQL Server-Machine Learning-Services | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-non-specified
ms.prod_service: r-services
ms.service: 
ms.component: advanced-analytics
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 6904c963c6178db530248f6189906e71df25308a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="architecture-overview-for-sql-server-machine-learning-services"></a>Übersicht über die Architektur für SQL Server-Machine Learning-Services 

In diesem Thema wird beschrieben, die Ziele der Extensibility Framework, die Ausführung von Python und R-Skript in SQL Server unterstützt.

Es bietet auch einen Überblick darüber, wie die Architektur, zur Erreichung dieser Ziele konzipiert ist wie R und Python unterstützt und von SQL Server und die Vorteile der Integration ausgeführt werden.

Insgesamt ist das Extensibility Framework für R und Python mit einigen kleineren Unterschieden in den Details der Startprogramme, die aufgerufen werden, die Konfigurationsoptionen usw. nahezu identisch. Weitere Informationen zur Implementierung für eine bestimmte Sprache finden Sie unter folgenden Themen:

- [Übersicht über die Architektur für SQL Server R Services](r/architecture-overview-sql-server-r.md)
- [Übersicht über die Architektur für Python in SQLServer](python/architecture-overview-sql-server-python.md)


## <a name="background"></a>Hintergrund

In SQL Server 2016 eingeführt wurden zahlreiche Änderungen mit dem Datenbankmodul, um die Ausführung von R-Skripts, die mithilfe von SQL Server unterstützen. In SQL Server 2017 wurde diese zugrunde liegenden Infrastruktur verbessert, zum Hinzufügen der Unterstützung für die Sprache Python.

Das Ziel das Extensibility Framework wurde zum Erstellen von zwischen SQL Server- und Data Science-Sprachen wie R und Python, um die Unstimmigkeiten zu reduzieren, die auftritt, wenn Data Science-Lösungen in die produktionsumgebung verschoben werden und zum Schutz von Daten, die möglicherweise einer bessere-Schnittstelle zur Verfügung gestellt, während des Entwicklungsprozesses für Data Science.

Führen Sie eine vertrauenswürdige Skriptsprache in einem sicheren Framework von SQL Server verwaltet werden, kann der Datenbankentwickler Aufrechterhaltung der Sicherheit und lässt datenspezialisten und Enterprise-Daten verwenden.

  ![Ziele der Integration mit SQL Server](media/ml-service-value-add.png "Machine Learning Services Wert hinzufügen")

- Derzeitige Benutzer von R oder Python sollte können ihren Code portieren, und führen Sie es mit geringfügigen Änderungen in SQL Server.
- Das Sicherheitsmodell von Daten in SQL Server wird auf Daten von externen Skriptsprachen verlängert. Das heißt, sollten jemand R oder Python-Skript ausführen nicht in der Lage, Daten verwenden, die von diesem Benutzer in einer SQL-Abfrage konnte nicht zugegriffen werden.
- Der Datenbankadministrator muss vom externer Skripts, die verwendeten Ressourcen zu verwalten, Verwalten von Benutzern, und verwalten und Überwachen von externen Codebibliotheken.
- Das System muss Projektmappen auf Grundlage vollständig open Source-Verteilung von R und Python jedoch verwenden, proprietäre Komponenten entwickelt, von Microsoft für die Erhöhung der Sicherheit und Leistung zu bieten, unterstützen.

## <a name="architecture-core-concepts"></a>Kernkonzepte Architektur

Um diese Ziele zu erreichen, wird diese kernbegriffe die Architektur des SQL Server 2016 R Services und SQL Server 2017 Machine Learning Services für R und Python davon:

+ **Architektur von Prozessen**

  Sind Open Source-Sprachen mit umfangreichem und Begeisterte Communityunterstützung R und Python. Aus diesem Grund ist es wichtig, vollständigen Interoperabilität mit open Source-R und Python zu verwalten.

  Open-Source-Verteilung von R und Python können unter Lizenz mit SQL Server installiert sind, und unabhängig von SQL Server bei Bedarf.

   Darüber hinaus bietet Microsoft einen Satz von proprietären Bibliotheken, die Integration mit SQL Server, einschließlich Daten Übersetzung, Komprimierung und Optimierung richtet sich an jede unterstützte Sprache bereitstellen.

+ **Sicherheit**

   Steigerung der Sicherheit bedeutet für integrierte Windows-Authentifizierung und SQL-Anmeldungen Kennwort-basierte als auch als sichere Handhabung von Anmeldeinformationen, die Abhängigkeit von SQL Server für den Schutz von Daten und Verwenden der SQL Server vertrauenswürdige Launchpad, um externe Skripts zu verwalten, unterstützen die Ausführung und sichere Daten in Skripts verwendet.

+ **Skalierbarkeit und Leistung**

  Integration mit SQL Server ist entscheidend verbessern die Nützlichkeit von R und Python im Unternehmen. Alle R oder Python-Skript kann durch Aufrufen einer gespeicherten Prozedur ausgeführt werden, und die Ergebnisse werden als tabellarische Ergebnisse direkt in SQL Server zu generieren oder nutzen von Machine Learning aus jeder Anwendung, die eine SQL-Abfrage senden und verarbeiten die Ergebnisse kann vereinfacht zurückgegeben.

  Zur Optimierung der Leistung basiert auf zwei gleichermaßen leistungsstarke Aspekte der Plattform: die Ressourcenkontrolle und parallele Verarbeitung mit SQL Server und verteiltes rechnen von in-Algorithmen bereitgestellte **"revoscaler"** und **Revoscalepy**.

## <a name="solution-development-and-deployment"></a>Entwicklung und Bereitstellung

Zusätzlich zu dieser Core Ziele für die Erweiterbarkeitsplattform dienen die Machine Learning-Dienste in SQL Server zum Bereitstellen von starken Integration mit dem Datenbankmodul und die BI-Stacks mit folgenden Vorteilen:

+ Leistung und Verwaltung über herkömmliche Überwachungstools
+ Einfach mithilfe von Python und R BI Testsammlungen oder einer beliebigen Anwendung, die die Ergebnisse der SQL-Abfrage nutzen können
+ Viel untere Grenze für Enterprise-Entwicklung von Machine Learning-Lösungen

Sehen wir uns an, wie es in der Praxis funktioniert.

  ![ML-Lösung Entwicklungsprozess](media/ml-solution-development-process.png "entwickeln und Bereitstellen von Machine Learning-Dienste verwenden")

1. Daten werden innerhalb der Begrenzung des Kompatibilität beibehalten und Verwendung von Daten verwaltet und von SQL Server überwacht werden kann. In der Zwischenzeit auftritt, hat der Datenbankadministrator vollständige Steuerung, wer Pakete installieren oder Ausführen von Skripts auf dem Server kann. Falls gewünscht, kann der Datenbankadministrator Berechtigungen auf Datenbankebene auf die Datenanalysten oder -Manager auch delegieren.
2. Datenanalysten können erstellen und Testen Lösungen in ihren bevorzugten R oder Python-Umgebungen, vom Server getrennt.
3. Der SQL-Entwickler können vertrauten Tools wie Management Studio oder Visual Studio um R oder Python-Code mit SQL Server zu integrieren. Die enge Integration bedeutet, dass der clevere Entwickler das beste Tool zum Optimieren von jeder Aufgabe auswählen kann. Sie können z. B. SQL für einige Feature engineering-Aufgaben und R für andere verwenden. Sie können in einem Integration Services-Task auszuführenden anspruchsvolle Textanalyse Python-Skript einbetten.
4. Getestet und kann jetzt zum Bereitstellen von Lösungen können mithilfe von SQL Server-Technologien, wie columnstore-Indizes für eine bessere Leistung optimiert werden. Neuere Funktionen ermöglichen das Batch-Train viele kleine Modelle parallel in partitionierten DataSet oder Bewertung von Millionen von Zeilen mithilfe der systemeigenen SQL-Code, die für Machine Learning-Aufgaben optimiert.
5. Heben Sie Installationsbereit? Predictive Projektmappen, die BI-Stack oder externe Anwendungen können problemlos mit gespeicherten Prozeduren verfügbar machen.

## <a name="related-products"></a>Verwandte Produkte

Nicht sicher mit die Machine learning-Lösung Ihre Anforderungen erfüllt? Zusätzlich zu den eingebetteten Analytics in SQL Server 2016 und SQL Server-2017 bietet Microsoft die folgenden Machine learning-Plattformen und Diensten:

+ [Microsoft R Server und Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)

  Ein Multi-Plattform-Umgebung zum Entwickeln, verteilen und Verwalten von Machine Learning-Aufträgen
+ [Data Science Virtual Machines](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview)

  Alle Tools, die für Machine learning, die vorinstalliert werden müssen. Verwenden Sie Jupyter Notebooks, Python oder R.
  
  Wiederholen Sie dann die neue [Windows 2016 Preview Edition](http://aka.ms/dsvm/win2016), dazu zählen auch GPU-Versionen der beliebten umfassenden lernen Frameworks wie z. B. CNTK und MxNet sowie Unterstützung für Windows-Containern!

+ [Azure Cognitive-Dienste](https://azure.microsoft.com/services/cognitive-services/)

  Eine Vielzahl von Clouddiensten zum Hinzufügen von AI und ML in Ihre Anwendungen, einschließlich natürlicher Sprache zu indizieren, video, Gesichtsausdruck Anerkennung Emotionen-Erkennung, Textanalyse Computer Übersetzung und vieles mehr
+ [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)

  Eine Cloud-basierte Drag-and-Drop-Schnittstelle zum Entwerfen von Machine Learning-Workflows, gekoppelt mit der Möglichkeit zum Automatisieren und Integrieren von Anwendungen über Webdienste und PowerShell

## <a name="see-also"></a>Siehe auch

[Vergleichen von Machine Learning-Server und Microsoft R-Produkte](https://docs.microsoft.com/machine-learning-server/what-is-r-server-interoperability)
