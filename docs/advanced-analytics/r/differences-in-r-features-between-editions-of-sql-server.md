---
title: SQL Server Machine Learning-Services - funktionsverfügbarkeit über Editionen | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: b64e836dc8969058e5012197e85fa78d40b87ac6
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>Verfügbarkeit von Features für Editionen von SQL Server-Machine Learning-Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Machine Learning-Funktionen sind in SQL Server 2016 und SQL Server-2017 verfügbar. In diesem Artikel listet die Editionen, die die Funktion bereitstellen, werden Einschränkungen, die in bestimmten Editionen gelten und sind Funktionen, die nur in bestimmten Editionen verfügbar.


## <a name="sql-server-2017-features"></a>2017 von SQL Server-Funktionen

Enterprise und Developer Edition haben dieselbe Funktion Erfassung, sodass Sie Lösungen für eine Unternehmensinstallation erstellen können, ohne dass die gleiche Kosten anfallen. Obwohl die Editionen funktionell gleichwertig sind, wird mithilfe der Developer Edition für produktionsumgebungen nicht unterstützt.

Der Unterschied zwischen grundlegenden und erweiterten Integration ist Skalierung. Erweiterte Integration können alle verfügbaren Kerne für die parallele Verarbeitung von Datasets auf eine beliebige Größe, die von Ihrem Computer aufnehmen kann. Grundlegende Integration ist auf 2 Kerne und Datasets im Arbeitsspeicher einpassen beschränkt. 

Grundlegende und erweiterte Integration gilt für die Instanzen (In-Database). Ein eigenständiger Server ist keine Datenbank-Engine-Instanz-Funktion und wird als Installationsoption nur in der Developer und Enterprise Editions angeboten.

|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Grundlegende Integration von R|ja|ja|ja|ja|nein|   
|Erweiterte Integration von R|ja|Nein|Nein|Nein|nein| 
|Grundlegende Integration von Python|ja|ja|ja|ja|nein|
|Erweiterte Integration von Python|ja|Nein|Nein|Nein|nein| 
|Machine Learning-Server (eigenständig)|ja|Nein|Nein|Nein|nein|   

 > [!NOTE]
 > Nur auf ein Server (eigenständig) bietet die [operationalisierung](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) Funktionen, die in einer Microsoft (nicht-SQL-Branding) R-Server "oder" Machine Learning-Server-Installation enthalten sind. Operationalisierung enthält Web Service-Bereitstellung und hosting-Funktionen.
>
> Für die Installation (In-Database) wird die entsprechende Vorgehensweise zum operationalisieren Lösungen Nutzung der Funktionen des Datenbankmoduls, beim Konvertieren von Code an eine Funktion, die in einer gespeicherten Prozedur ausgeführt werden kann.


## <a name="sql-server-2016-r-features"></a>SQL Server 2016-R-Funktionen

SQL Server 2016 schließt nur die R-Integration. In SQL Server 2016 grundlegenden und erweiterten R-Integration entsprechen 2017 von SQL Server.

## <a name="r-feature-availability-in-azure-sql-database"></a>Verfügbarkeit von R-Funktionen in Azure SQL-Datenbank
  
Nach einer anfänglichen Test--Version wurde R Services ausstehende Weiterentwicklung aus Azure SQL-Datenbank entfernt. 

## <a name="performance-expectations-for-enterprise-edition"></a>Leistungserwartungen für die Enterprise Edition

Leistung der Machine Learning-Lösungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird erwartet, dass in der Regel mit konventionellen R, erhält die gleiche Hardware Implementierungen übertreffen. Die liegt daran, dass in SQL Server R-Lösungen mit Serverressourcen ausgeführt werden können und in einigen Fällen mit mehreren Prozessen, die mit distributed der **"revoscaler"** Funktionen. 

Benutzer können auch erwartungsgemäß erhebliche Unterschiede in der Leistung und Skalierbarkeit im Hinblick auf dem gleichen Computer Lern-Lösung, wenn in der Enterprise Edition im Vergleich ausgeführt. Standard Edition Ursachen gehören Unterstützung für parallele Verarbeitungsthreads, erhöhte für maschinelles lernen, verfügbar und streaming (oder Segmentierung), die RevoScaleR-Funktionen, mehr Daten als in den Arbeitsspeicher passen können behandeln können. 

Allerdings kann die Leistung auch auf identische Hardware von vielen Faktoren außerhalb der R oder Python-Codes beeinträchtigt werden. Folgende Faktoren konkurrierende Nachfrage nach Serverressourcen, die Art der Abfrageplan, der erstellt wird, schemaänderungen, die Notwendigkeit zum Aktualisieren von Statistiken oder erstellen ein neuer Abfrageplan, Fragmentierung und mehr. Es ist möglich, dass eine gespeicherte Prozedur mit R oder Python-Code in Sekunden unter eine Arbeitslast ausgeführt, aber nehmen, wenn Minuten andere ausgeführte Dienste vorhanden sind.  Aus diesem Grund wird empfohlen, dass Sie mehrere Aspekte der serverleistung, Netzwerk für remote rechenkontexte, einschließlich der beim Machine Learning-leistungsmessung überwachen.

Zudem wird empfohlen, dass Sie konfigurieren [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (verfügbar in der Enterprise Edition) anzupassen, dass externe Skripts für Aufträge priorisiert oder unter starker serverarbeitsauslastungen behandelt. Sie können Klassifizierungsfunktionen Begrenzen der Menge an Arbeitsspeicher, die von SQL-Abfragen verwendet, um Geben Sie die Quelle des externen Skripts Auftrags und priorisieren bestimmte arbeitsauslastungen definieren und steuern die Anzahl der parallelen Prozessen Workload regelmäßig verwendet.

## <a name="see-also"></a>Siehe auch

+ [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Editionen und Komponenten von SQL Server-2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [Tipps für Computerressourcen mit umfangreichen Daten in R (Machine Learning-Server)](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
