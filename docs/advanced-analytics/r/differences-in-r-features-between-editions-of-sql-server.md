---
title: "SQL Server Machine Learning-Services - funktionsverfügbarkeit über Editionen | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2018
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
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 16ca6c44b15c9fb7c1983d5a04175ebbade57895
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>Verfügbarkeit von Features für Editionen von SQL Server-Machine Learning-Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Machine Learning-Funktionen sind in SQL Server 2016 und SQL Server-2017 verfügbar. In diesem Artikel listet die Editionen, die die Funktion bereitstellen, werden Einschränkungen, die in bestimmten Editionen gelten und sind Funktionen, die nur in bestimmten Editionen verfügbar.

 > [!NOTE]
 > Im Allgemeinen SQL Server-Machine Learning (In-Database) enthält keine der [operationalisierung](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) Funktionen, die in einer eigenständigen R-Server "oder" Machine Learning-Server-Installation enthalten sind. Operationalisierung Web Service-Bereitstellung und hosting enthält und daher für die gleichen Ressourcen wie andere SQL Server-Vorgängen konkurriert.
 > 
 > Aus diesem Grund wird empfohlen, SQL Server 2016 R Server (eigenständig) oder SQL Server 2017 Machine Learning-Server (eigenständig) auf einem anderen physischen Server zur Unterstützung der Bereitstellung von Vorhersagemodellen als Webdienst installieren. 

## <a name="sql-server-2017-machine-learning-services-in-database-and-standalone"></a>SQL Server 2017 Machine Learning Services (Datenbankintern) und (eigenständig)

Die Developer Edition bietet Leistung entspricht, die Enterprise Edition. Verwenden der Developer Edition wird für produktionsumgebungen nicht unterstützt.

|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------|----------|--------|---|------------------------------|-------|
| R-Interpreter & proprietären Pakete | ja | ja | Nein | Nein | nein | 
| Python-Interpreter & Client-Bibliotheken | ja | ja | Nein | Nein | nein | 
| Daten, die Segmentierung <br/>(verarbeiten Sie große Datenmengen, oberhalb, was in den Arbeitsspeicher passt) | ja | Nein | Nein | Nein | nein |
| Vertikale Skalierung Verarbeitung <br/>(mehr als 2 Prozessoren) | ja | Nein | Nein | Nein | nein |
| Operationalisierung | ja | Nein | Nein | Nein | nein |
| [VORHERSAGEN](../../t-sql/queries/predict-transact-sql.md) Funktion <br/>(führt [native Bewertung](../sql-native-scoring.md) auf ein vortrainiertes Modell, das zuvor in das erforderliche binären Format gespeichert) | ja | ja | ja | ja | ja |
| R-Clientkompatibilität | ja | ja | Nein | Nein | nein | 
| Microsoft R Open | ja | ja | Nein | Nein | nein | 
| Anaconda Python 3.5 | ja | ja | Nein | Nein | nein | 

## <a name="sql-server-2016-r-services-in-database-and-r-server-standalone"></a>SQL Server 2016 R Services (Datenbankintern) und R-Server (eigenständig)

Verfügbarkeit von Features ist identisch mit 2017 minus Python-Unterstützung, die nicht Bestandteil der zunächst 2016 Version war.

## <a name="r-feature-availability-in-azure-sql-database"></a>Verfügbarkeit von R-Funktionen in Azure SQL-Datenbank
  
Nach der Veröffentlichung einer anfänglichen Test-R Services ist zurzeit **nicht** ausstehende weiteren Entwicklung in Azure SQL-Datenbank verfügbar. 

## <a name="performance-expectations-for-enterprise-edition"></a>Leistungserwartungen für die Enterprise Edition

Leistung der Machine Learning-Lösungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird erwartet, dass in der Regel mit konventionellen R, erhält die gleiche Hardware Implementierungen übertreffen. Die liegt daran, dass in SQL Server R-Lösungen mit Serverressourcen ausgeführt werden können und in einigen Fällen mit mehreren Prozessen, die mit distributed der **"revoscaler"** Funktionen. 

Leistung ist nicht für Python-Lösungen bewertet wurde, wie die Funktion befindet sich noch in Entwicklung, aber einige der Vorteile gelten soll.

Benutzer können auch erwartungsgemäß erhebliche Unterschiede in der Leistung und Skalierbarkeit im Hinblick auf dem gleichen Computer Lern-Lösung, wenn in der Enterprise Edition im Vergleich ausgeführt. Standard Edition Ursachen gehören Unterstützung für parallele Verarbeitungsthreads, erhöhte für maschinelles lernen, verfügbar und streaming (oder Segmentierung), die RevoScaleR-Funktionen, mehr Daten als in den Arbeitsspeicher passen können behandeln können. 

Allerdings kann die Leistung auch auf identische Hardware von vielen Faktoren außerhalb der R oder Python-Codes beeinträchtigt werden. Folgende Faktoren konkurrierende Nachfrage nach Serverressourcen, die Art der Abfrageplan, der erstellt wird, schemaänderungen, die Notwendigkeit zum Aktualisieren von Statistiken oder erstellen ein neuer Abfrageplan, Fragmentierung und mehr. Es ist möglich, dass eine gespeicherte Prozedur mit R oder Python-Code in Sekunden unter eine Arbeitslast ausgeführt, aber nehmen, wenn Minuten andere ausgeführte Dienste vorhanden sind.  Aus diesem Grund wird empfohlen, dass Sie mehrere Aspekte der serverleistung, Netzwerk für remote rechenkontexte, einschließlich der beim Machine Learning-leistungsmessung überwachen.

Zudem wird empfohlen, dass Sie konfigurieren [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (verfügbar in der Enterprise Edition) anzupassen, dass externe Skripts für Aufträge priorisiert oder unter starker serverarbeitsauslastungen behandelt. Sie können Klassifizierungsfunktionen Begrenzen der Menge an Arbeitsspeicher, die von SQL-Abfragen verwendet, um Geben Sie die Quelle des externen Skripts Auftrags und priorisieren bestimmte arbeitsauslastungen definieren und steuern die Anzahl der parallelen Prozessen Workload regelmäßig verwendet.

## <a name="see-also"></a>Siehe auch

+ [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Editionen und Komponenten von SQL Server-2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [Tipps für Computerressourcen mit umfangreichen Daten in R (Machine Learning-Server)](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
