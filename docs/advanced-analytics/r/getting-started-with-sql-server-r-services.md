---
title: Erste Schritte mit SQLServer Machine Learning | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 12/07/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: "34"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8a6e15767282d347fc92b7decf2963d85827cf6f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="getting-started-with-sql-server-machine-learning"></a>Erste Schritte mit SQLServer Machine Learning

Machine Learning Services in SQL Server dient zur Installation ohne Verfügbarmachen der Daten zu Sicherheitsrisiken oder gleitenden Daten Unnecesarily Data Science-Aufgaben unterstützen.

+ In SQL Server 2016 können Sie mit Ihren bevorzugten R-Tools arbeiten, aber skalieren Ihre Analyse auf Milliarden Datensätze beim und die Leistung erheblich steigert. Integrieren von SQL Server in Machine Learning bedeutet auch, dass R-Code in der Produktion verwendet werden können, ohne code neu.

+ SQL Server-2017 fügt Unterstützung für Python-Code, mit dem gleichen Extensibility Framework.

In diesem Thema wird beschrieben, die wichtigsten Szenarien für die Verwendung von R oder Python in der Datenbank und Ressourcen helfen Ihnen beim Einstieg in Ihren eigenen Lösungen bietet.

Gilt für: SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Services (Datenbankintern)

> [!NOTE]
> SQL Server 2016 unterstützt nur die Sprache "R". Unterstützung für Python-Sprache ist SQL Server 2017 CTP 2.0 erforderlich.

## <a name="step-1-set-up-sql-server-machine-learning-services"></a>Schritt 1: Einrichten von SQL Server-Machine Learning-Services

1. Führen Sie SQL Server-Setup aus, und installieren Sie mindestens eine Instanz des SQL Server-Datenbankmoduls.
2. Fügen Sie das Feature, das Ausführung von externen Laufzeiten unterstützt.
3. R ist in SQL Server 2016 wird standardmäßig hinzugefügt. In SQL Server-2017 müssen Sie eine Sprache hinzufügen auswählen. Sie können wählen, R oder Python oder beides aktivieren.
4. Wenn Setup abgeschlossen ist, führen Sie einige zusätzliche Schritte zum Aktivieren der externen skriptausführung, und starten Sie den Server neu.

**Ressourcen**

+ [Einrichten von SQL Server mit Machine Learning](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

> [!TIP]  
> Möchten Sie einen Server für R-Aufträge mit einem anderen Betriebssystem als SQL Server erstellen? Versuchen Sie es mit [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx).  

## <a name="step-2-develop-your-r-or-python-solutions"></a>Schritt 2: Entwickeln Sie Ihre R oder Python-Lösungen

Datenanalysten verwenden R oder Python in der Regel auf ihren eigenen Arbeitsstationen Laptop oder Entwicklungscomputer zum Durchsuchen von Daten, und erstellen und Optimieren von Vorhersagemodellen, bis ein geeignetes Vorhersagemodell erreicht ist. 

Machine Learning Services in SQL Server ist es nicht erforderlich, um diesen Prozess zu ändern. Nach Abschluss der Installation können Sie R oder Python-Code ausführen, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entweder lokal oder Remote:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **Die IDE gewünscht**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] -Clientkomponenten stellen für Datenanalysten sämtliche Tools bereit, die zum Experimentieren und Entwickeln erforderlich sind. Zu diesen Tools zählen die R-Laufzeitversion, die mathematische Kernelbibliothek von Intel zur Leistungssteigerung von R-Standardfunktionen sowie eine Reihe von erweiterten R-Paketen, die das Ausführen von R-Code in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützen.  

+ **Arbeiten Sie Remote oder lokal**. Datenanalysten können eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und dem Client die Daten wie gewohnt zur lokalen Analyse vorlegen. Die Verwendung der **ScaleR** -APIs zum Verlagern von Berechnungen mittels Push auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer, um kostenintensive und unsichere Datenbewegungen zu vermeiden, ist jedoch die bessere Lösung.

+ **Einbetten von R oder Python-Skripts in [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozeduren**. Wenn Ihr Code vollständig optimiert ist, binden Sie diese in einer gespeicherten Prozedur vermeiden unnötige datenbewegungen und Optimieren von Data-Verarbeitungsaufgaben an.


**Ressourcen**

+ Installieren Sie [R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation) oder RStudio.  

## <a name="step-3-optimize"></a>Schritt 3: Optimieren

Wenn das Modell für die Skalierung auf Enterprise-Daten ist, funktioniert der Data Scientist häufig mit dem Datenbankadministrator oder der SQL-Entwickler Prozesse wie z. B. zu optimieren:

+ Featureentwicklung
+ Als "Erfassung" Daten und die Datentransformation
+ Bewertung

Bisher mussten Datenanalysten verwenden R Probleme mit der Leistung und Skalierung, insbesondere wenn Sie große Datasets verwendet. Das liegt daran Implementierung des allgemeinen Laufzeitmoduls nur einen einzelnen Thread und nur die Datasets, die in den verfügbaren Arbeitsspeicher auf dem lokalen Computer entsprechen aufnehmen kann. Integration mit SQl Server-Machine Learning-Services stellt mehrere Funktionen für eine bessere Leistung, mehr Daten bereit:

+ **"Revoscaler"**.: Diese R-Paket enthält die Implementierung einiger der beliebtesten R-Funktionen neu gestaltet, um die Parallelität und Skalierung bereitzustellen. Das Paket enthält auch Funktionen, die die Leistung und Skalierung weiter erhöhen, indem Berechnungen mittels Push auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer übertragen werden, der in der Regel über wesentlich mehr Arbeitsspeicher und Rechenleistung verfügt.

+ **revoscalepy**. Diese Python-Clientbibliothek, neue und nur in SQL Server 2017 CTP 2.0 verfügbar implementiert die am häufigsten verwendeten Funktionen im "revoscaler", z. B. remote rechenkontexte und viele Algorithmen, die unterstützt verteilte Verarbeitung.

+ Wählen Sie die beste Sprache für den Task aus.  R ist am besten für statistische Berechnungen, die schwierig zu implementieren, verwenden SQL sind. Für setbasierte Vorgänge für Daten, nutzen die Leistungsfähigkeit des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um optimale Leistung zu erzielen. Verwenden Sie das in-Memory-Datenbankmodul für sehr schnelle Berechnungen über Spalten.

**Ressourcen**

+ [Fallstudie zur Leistung](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R- und Datenoptimierung](../../advanced-analytics/r/r-and-data-optimization-r-services.md)


## <a name="step-4-deploy-and-consume"></a>Schritt 4. Bereitstellen und nutzen

Nachdem die R-Skript oder das Modell für die Produktion bereit ist, kann ein Datenbankentwickler den Code oder das Modell in einer gespeicherten Prozedur einbetten, sodass die gespeicherte R oder Python-Code aus einer Anwendung aufgerufen werden kann. Das Speichern und Ausführen von R über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet viele Vorteile: Sie können die komfortable [!INCLUDE[tsql](../../includes/tsql-md.md)] -Benutzeroberfläche verwenden. Außerdem erfolgen sämtliche Berechnungen in der Datenbank, wodurch unnötige Datenbewegungen vermieden werden.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **Sichere und erweiterbare**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verwendet eine neue Erweiterbarkeitsarchitektur, die das Datenbankmodul sichert und R-Sitzungen isoliert. Außerdem haben Sie die Kontrolle über Benutzer, die R-Skripts ausführen können, und können angeben, auf welche Datenbanken der R-Code zugreifen darf. Sie können den Umfang der Ressourcen steuern, die der R-Laufzeit zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die Gesamtleistung des Servers gefährden.

+ **Planung und Überwachung**. Bei der Ausführung von externen Skripts für Aufträge im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie steuern und Überwachen der Daten, die von Datenanalysten verwendet. Sie können auch planen, Aufträge und Workflows erstellen, die externe R oder Python-Skripts, wie Sie jede andere T-SQL-Auftrag oder die gespeicherte Prozedur planen möchten.

Um die Vorteile der ressourcenverwaltung und Sicherheitsupdate-Funktionen in SQL Server nutzen zu können, kann der Bereitstellungsprozess diese Aufgaben sind:

+ Konvertieren von R-Code an eine Funktion, die optimal in einer gespeicherten Prozedur ausgeführt werden kann
+ Einrichten der Sicherheit und Pakete, die von einer bestimmten Aufgabe verwendet Sperren
+ Aktivieren der Ressourcenkontrolle

**Ressourcen**

+ [Ressourcenkontrolle für R](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [R-Paketverwaltung für SQLServer](../../advanced-analytics/r/r-package-management-for-sql-server-r-services.md)

## <a name="quick-starts"></a>Schnellstarts

Lesen Sie in dieser exemplarischen Vorgehensweise, um den vollständigen Workflow, von Durchsuchen von Daten zum Erstellen eines Modells und Bereitstellung für SQL Server zu verstehen.

+ [Lückenlose exemplarische Data Science-Vorgehensweise](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Erfahren Sie, wie die RevoScaleR-Paket für die skalierbare und high-Performance-Analyse verwenden.

+ [Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

Insbesondere der Entwickler Daten--aus Gründen der alle R-Code! Informationen Sie zum Einbetten von R in gespeicherten SQL-Prozeduren zum Erstellen oder Modelle zu trainieren und Vorhersagen aus einem gespeicherten Modell abrufen.

+ [Datenbankinterne Advanced Analytics für SQL-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Erfahren Sie, die Syntax für die aufrufende R aus einer gespeicherten Prozedur.

+ [Verwenden von R-Code in Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

## <a name="solutions"></a>Lösungen

Weitere Beispiele, einschließlich der Branche = spezifische Lösung-Vorlagen finden Sie unter [SQL Server-Machine Learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).
