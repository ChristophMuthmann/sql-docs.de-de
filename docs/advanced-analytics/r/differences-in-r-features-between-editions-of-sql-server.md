---
title: Unterschiede in Machine Learning-Funktionen zwischen SQL Server-Editionen | Microsoft Docs
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 57b4279882cf2c1363dc40616175552260aff0c9
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>Unterschiede in Machine Learning-Funktionen zwischen SQL Server-Editionen
 
 Unterstützung für Machine Learning ist in SQL Server 2016 und SQL Server-2017 verfügbar. In diesem Artikel listet die Editionen, die das Feature zu unterstützen, sind zusätzliche Einschränkungen, die in bestimmten Editionen gelten und sind Funktionen, die nur in bestimmten Editionen verfügbar.

 > [!NOTE]
 > SQL Server-Machine Learning umfasst in der Regel keine der [operationalisierung](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) Funktionen, die in Microsoft R Server "oder" Machine Learning-Server enthalten sind.
 > 
 > Wenn Sie diese Funktionen benötigen, können Sie Microsoft R Server oder Computer Learning separat installieren zur Unterstützung einer Bereitstellung von Vorhersagemodellen als Webdienst. 

## <a name="summary-of-differences"></a>Zusammenfassung der Unterschiede

-   **Enterprise Edition**
    
     SQL Server-2017 enthält Machine Learning-Services (In-Datenbanken. SQL Server 2016 enthält R-Dienste. Diese Funktion unterstützt Analytics in der Datenbank in SQL Server, einschließlich der Verwendung von SQL Server als computekontext verwenden.
     
     SQL Server-2017 umfasst Microsoft Machine Learning-Server (eigenständig). SQL Server 2016 umfasst Microsoft R Server (eigenständig). Diese Funktion unterstützt operationalisierung von Machine learning, die nicht erfordert, dass die Verwendung von SQL Server als computekontext verwenden.

     Es gibt keine Einschränkungen für diese Funktionen in der Enterprise Edition, die durch die Parallelisierung und streaming optimierte Leistung und Skalierbarkeit bietet. Diese Edition maximiert auch die Verwendung der plattformunterstützung für streaming und parallele Ausführung. Das bedeutet, die Eingabedaten anders als Standard Edition muss nicht in den Arbeitsspeicher passen jedoch gestreamt werden.
     
     In der Datenbank-Analysen, die mit SQL Server unterstützt die Ressourcenkontrolle externer Skripts, die Nutzung von Serverressourcen anpassen.
     
     Neuere Versionen von Microsoft R Server und Machine Learning-Servers gehören eine verbesserte Version des Moduls operationalisierung, die eine schnelle und sichere Bereitstellung unterstützt und Freigabe von R-Lösungen. Weitere Informationen finden Sie unter [Operationalisieren Analysen mit Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization).

-   **Developer Edition**

     Besitzt dieselben Funktionen wie Enterprise Edition, Developer Edition kann jedoch nicht in Produktionsumgebungen verwendet werden.  
  
-   **Standard Edition**

     Verfügt über alle Funktionen in der Datenbank-Analysefunktionen von mit Ausnahme der Ressourcenkontrolle mit Enterprise Edition enthalten. Leistung und Skalierung sind zudem beschränkt: die Daten, die verarbeitet werden können, müssen in den Serverarbeitsspeicher passen und Verarbeitung an einen einzelnen Compute-Thread beschränkt ist, selbst bei Verwendung der **"revoscaler"** Funktionen.
  
-   **Express und Web-Editionen**
  
     Nur Express Edition with Advanced Services enthält Machine learning-Funktionen. Die Leistungseinschränkungen ähneln denen in der Standard Edition. 
     
     Web Edition ist nicht für Aufgaben wie das Erstellen von Machine Learning-Modellen vorgesehen. Die PREDICT-Funktion können Sie jedoch bewerten Modelle trainiert an anderer Stelle verwenden.

-   **Azure SQL-Datenbank**
  
     Nach der Veröffentlichung einer anfänglichen Test-R Services ist zurzeit **nicht** ausstehende weiteren Entwicklung in Azure SQL-Datenbank verfügbar. 

### <a name="external-script-languages-supported"></a>Externes Skriptsprachen unterstützt

Für alle Editionen werden die folgenden Machine Learning-Sprachen unterstützt:

+ SQLServer 2017: R und Python
+ SQLServer 2016: Nur R

Microsoft R Open ist in allen Editionen enthalten.

Microsoft R Client kann mit allen Editionen arbeiten.

## <a name="machine-learning-in-enterprise-edition"></a>Machine learning-in der Enterprise Edition

Leistung der Machine Learning-Lösungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird erwartet, dass in der Regel mit konventionellen R, erhält die gleiche Hardware Implementierungen übertreffen. Die liegt daran, dass in SQL Server R-Lösungen mit Serverressourcen ausgeführt werden können und in einigen Fällen mit mehreren Prozessen, die mit distributed der **"revoscaler"** Funktionen. 

Leistung ist nicht für Python-Lösungen bewertet wurde, wie die Funktion befindet sich noch in Entwicklung, aber einige der Vorteile gelten soll.

Benutzer können auch erwartungsgemäß erhebliche Unterschiede in der Leistung und Skalierbarkeit im Hinblick auf dem gleichen Computer Lern-Lösung, wenn in der Enterprise Edition im Vergleich ausgeführt. Standard Edition Ursachen gehören Unterstützung für parallele Verarbeitungsthreads, erhöhte für maschinelles lernen, verfügbar und streaming (oder Segmentierung), die RevoScaleR-Funktionen, mehr Daten als in den Arbeitsspeicher passen können behandeln können. 

Allerdings kann die Leistung auch auf identische Hardware von vielen Faktoren außerhalb der R oder Python-Codes beeinträchtigt werden. Folgende Faktoren konkurrierende Nachfrage nach Serverressourcen, die Art der Abfrageplan, der erstellt wird, schemaänderungen, die Notwendigkeit zum Aktualisieren von Statistiken oder erstellen ein neuer Abfrageplan, Fragmentierung und mehr. Es ist möglich, dass eine gespeicherte Prozedur mit R oder Python-Code in Sekunden unter eine Arbeitslast ausgeführt, aber nehmen, wenn Minuten andere ausgeführte Dienste vorhanden sind.  Aus diesem Grund wird empfohlen, dass Sie mehrere Aspekte der serverleistung, Netzwerk für remote rechenkontexte, einschließlich der beim Machine Learning-leistungsmessung überwachen.

Zudem wird empfohlen, dass Sie konfigurieren [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (verfügbar in der Enterprise Edition) anzupassen, dass externe Skripts für Aufträge priorisiert oder unter starker serverarbeitsauslastungen behandelt. Sie können Klassifizierungsfunktionen Begrenzen der Menge an Arbeitsspeicher, die von SQL-Abfragen verwendet, um Geben Sie die Quelle des externen Skripts Auftrags und priorisieren bestimmte arbeitsauslastungen definieren und steuern die Anzahl der parallelen Prozessen Workload regelmäßig verwendet.

## <a name="machine-learning-in-developer-edition"></a>Machine learning-Developer Edition

Developer Edition bietet Leistung entspricht, die Enterprise Edition.

Verwenden der Developer Edition wird für produktionsumgebungen nicht unterstützt.

## <a name="machine-learning-in-standard-edition"></a>Machine learning-Standard Edition

Auch die Standard Edition sollte einige Leistungsvorteile bieten, im Vergleich zu Standard R-Paketen, die die gleiche Hardwarekonfiguration angeben.

Die Ressourcenkontrolle unterstützt Standard Edition nicht. Standard Edition bietet auch nur eine eingeschränkte Leistung und Skalierbarkeit im Vergleich zu Enterprise und Developer Edition.

Alle der **"revoscaler"** Funktionen und Pakete sind in der Standard Edition enthalten, aber der Dienst, der gestartet wird, und R-Skripts verwaltet ist beschränkt, in die Anzahl von Prozessen, die sie verwenden kann. Darüber hinaus müssen vom Skript verarbeitete Daten in den Arbeitsspeicher passen.

Die gleichen Einschränkungen gelten für Lösungen, in denen **Revoscalepy**.

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Machine learning-Express Edition with Advanced Services

Express Edition unterliegt denselben Einschränkungen wie Standard Edition.

## <a name="machine-learning-in-web-edition"></a>Machine learning-im Web Edition

Web Edition unterstützt keine Ausführung von R oder Python-Skripts. Allerdings können Sie die [PREDICT](../../t-sql/queries/predict-transact-sql.md) Funktion ausführen [native Bewertung](../sql-native-scoring.md) auf ein Modell, das auf einer anderen Instanz von SQL Server oder R trainiert und klicken Sie dann in das erforderliche Binärformat gespeichert wurde.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden Themen:

+ [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Editionen und Komponenten von SQL Server-2017](../../sql-server/editions-and-components-of-sql-server-2017.md)

Weitere Informationen zu anderen Features in SQL Server finden Sie unter:

+ [Editionen und unterstützten Funktionen von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) 

Weitere Informationen dazu, wie Sie Ihre Lösung für große Datasets optimieren können, finden Sie unter [Tipps für Computerressourcen mit umfangreichen Daten in R](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips) Dokumentation.
