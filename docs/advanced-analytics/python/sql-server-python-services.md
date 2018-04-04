---
title: Machine Learning-Dienste mit Python | Microsoft Docs
ms.date: 03/16/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 275eedc011367e51e97c6bddae03858cdda932ee
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="machine-learning-services-with-python"></a>Machine Learning-Dienste mit Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python ist eine Programmiersprache, die hohe Flexibilität und Leistungsfähigkeit für eine Vielzahl von Machine learning-Aufgaben bietet. Für Python-Open Source-Bibliotheken enthalten mehrere Plattformen für anpassbare neuronale Netzwerke sowie beliebte Bibliotheken für die Verarbeitung natürlicher Sprache. Diese häufig verwendete Sprache wird jetzt in SQL Server 2017 Machine Learning unterstützt.

Da Python integriert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankmodul, können Sie Analysen in der Nähe der Daten und zu vermeiden, die Kosten und Sicherheitsrisiken durch Verschieben von Daten.  Sie können die Machine Learning Projektmappen auf Grundlage von Python mit geeigneten, vertrauten Tools wie Visual Studio bereitstellen. Ihre Produktionsanwendungen können Vorhersagen, Modelle, Abrufen oder visuellen Elementen aus der Python-3.5-Laufzeit durch Aufrufen von einfach einen T-SQL-Prozedur.

Diese Version enthält die Anaconda-Verteilung von Python, als auch die [Revoscalepy](../python/what-is-revoscalepy.md) Bibliothek, um die Skalierung und Leistung von Ihrer für maschinelles lernen von Lösungen zu verbessern.

Sie können alles installieren müssen Sie mit Python mithilfe von 2017 von SQL Server-Setup zu beginnen:

+ [**Machine Learning-Services (Datenbankintern)**](../install/sql-machine-learning-services-windows-install.md): Installieren Sie diese Funktion, zusammen mit der SQL Server-Datenbankmodul verwenden, um sichere Ausführung von Python-Skripts auf ermöglichen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
     Wenn Sie dieses Feature auswählen, Erweiterungen im Datenbankmodul zur Unterstützung der Ausführung von Python-Skripts installiert sind und ein neuer Dienst erstellt, die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], um die Verwaltung der Kommunikation zwischen der Python-Laufzeit und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.

+ [**Machine Learning-Server (eigenständig)**](../install/sql-machine-learning-standalone-windows-install.md): Wenn Sie SQL Server-Integration nicht benötigen, installieren Sie diese Funktion, um Python und R-Unterstützung für verteilte Machine Learning zu erhalten.

## <a name="see-also"></a>Siehe auch

+ [SQLServer Machine Learning und R Services (Datenbankintern)](../r/sql-server-r-services.md)
+ [SQLServer Machine Learning und R-Server (eigenständig)](../r/r-server-standalone.md)
+ [Python-Architektur](architecture-overview-sql-server-python.md)
+ [Python-Lernprogramme](../tutorials/sql-server-python-tutorials.md)
