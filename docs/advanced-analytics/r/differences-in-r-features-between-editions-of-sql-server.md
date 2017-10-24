---
title: Unterschiede in Machine Learning-Funktionen zwischen SQL Server-Editionen | Microsoft Docs
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9b520b7fc7e97498f4b46a43ad991558025123a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>Unterschiede in Machine Learning-Funktionen zwischen SQL Server-Editionen
 
 Unterstützung für Machine Learning ist in den folgenden Editionen von SQL Server 2016 und SQL Server-2017 verfügbar:

## <a name="summary-of-differences"></a>Zusammenfassung der Unterschiede

-   **Enterprise Edition**
    
     SQL Server-2017 enthält Machine Learning-Services (In-Datenbanken. SQL Server 2016 enthält R-Dienste. Diese Funktion unterstützt Analytics in der Datenbank in SQL Server, einschließlich der Verwendung von SQL Server als computekontext verwenden.
     
     SQL Server-2017 umfasst Microsoft Machine Learning-Server (eigenständig). SQL Server 2016 umfasst Microsoft R Server (eigenständig). Diese Funktion unterstützt operationalisierung von Machine learning, die nicht erfordert, dass die Verwendung von SQL Server als computekontext verwenden.

     Es gibt keine Einschränkungen für diese Funktionen in der Enterprise Edition, die durch die Parallelisierung und streaming optimierte Leistung und Skalierbarkeit bietet. Diese Edition maximiert auch die Verwendung der plattformunterstützung für streaming und parallele Ausführung.
     
     In der Datenbank-Analysen, die mit SQL Server unterstützt die Ressourcenkontrolle externer Skripts, die Nutzung von Serverressourcen anpassen.
     
     Neuere Versionen von Microsoft R Server einschließen, eine verbesserte Version des Moduls operationalisierung, die eine schnelle und sichere Bereitstellung unterstützt und Freigabe von R-Lösungen. Weitere Informationen finden Sie unter [Mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package).

-   **Developer Edition**

     Besitzt dieselben Funktionen wie Enterprise Edition, Developer Edition kann jedoch nicht in Produktionsumgebungen verwendet werden.  
  
-   **Standard Edition**

     Verfügt über alle Funktionen in der Datenbank-Analysefunktionen von mit Ausnahme der Ressourcenkontrolle mit Enterprise Edition enthalten. Leistung und Skalierung ist außerdem beschränkt: die Daten, die verarbeitet werden können, müssen in den Serverarbeitsspeicher passen und Verarbeitung an einen einzelnen Compute-Thread beschränkt ist, selbst bei Verwendung der **"revoscaler"** Funktionen.
  
-   **Express und Web-Editionen**
  
     Nur Express Edition with Advanced Services enthält Machine learning-Funktionen. Die Leistungseinschränkungen ähneln denen in der Standard Edition. Web Edition ist nicht für Aufgaben wie das Erstellen von Machine Learning-Modellen vorgesehen; die PREDICT-Funktion können Sie jedoch bewerten Modelle trainiert an anderer Stelle verwenden.

-   **Azure SQL-Datenbank**
  
     Machine Learning-Funktionen wie R und Python-Skripts werden in Azure SQL-Datenbank derzeit nicht unterstützt.
     
     Weitere Informationen und Hinweise zu, wenn diese Funktion zur Verfügung stehen, werden die SQL Server-Blog finden Sie unter: [Python in SQL Server-2017: Erweiterte in Datenbank-Machine Learning](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


### <a name="languages-supported-in-all-editions"></a>In allen Editionen unterstützten Sprachen

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

Die Developer Edition bietet die gleiche Leistung, die Enterprise Edition bietet. Die Verwendung der Developer Edition wird jedoch nicht für Produktionsumgebungen unterstützt.

## <a name="machine-learning-in-standard-edition"></a>Machine learning-Standard Edition

Auch die Standard Edition sollte einige Leistungsvorteile bieten, im Vergleich zu Standard R-Paketen, die die gleiche Hardwarekonfiguration angeben.

Die Ressourcenkontrolle unterstützt Standard Edition nicht. Verwenden die Ressourcenkontrolle ist die beste Methode zum Anpassen von Serverressourcen zur Unterstützung von verschiedenen arbeitsauslastungen wie z. B. Modell trainieren und bewerten.

Die Standard Edition bietet auch nur eine eingeschränkte Leistung und Skalierbarkeit im Vergleich zur Enterprise und Developer Edition. Alle der **"revoscaler"** Funktionen und Pakete sind in der Standard Edition enthalten, aber der Dienst, der gestartet wird, und R-Skripts verwaltet ist beschränkt, in die Anzahl von Prozessen, die sie verwenden kann. Darüber hinaus müssen vom Skript verarbeitete Daten in den Arbeitsspeicher passen.  Die gleichen Einschränkungen gelten für Lösungen, in denen **Revoscalepy**.

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Machine learning-Express Edition with Advanced Services

Express Edition unterliegt denselben Einschränkungen wie Standard Edition.

## <a name="machine-learning-in-web-edition"></a>Machine learning-im Web Edition

Web Edition unterstützt keine Ausführung von R oder Python-Skripts. Sie können jedoch die Vorhersagefunktion ausführen [native Bewertung](../sql-native-scoring.md) auf ein Modell, das auf einer anderen Instanz von SQL Server oder R trainiert und klicken Sie dann in das erforderliche Binärformat gespeichert wurde.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden Themen:

+ [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Editionen und Komponenten von SQL Server-2017](../../sql-server/editions-and-components-of-sql-server-2017.md)

Weitere Informationen zu anderen Features in SQL Server finden Sie unter:

+ [Von den SQL Server 2016-Editionen unterstützte Funktionen](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

Weitere Informationen zu Microsoft R-Funktionen und wie Sie Ihre Lösung für große Datasets optimieren können, finden Sie unter der [Microsoft R Server](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips) Dokumentation.

