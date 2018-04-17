---
title: SQL Server-Machine Learning-Dienste mit Python | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b8ef234b0e8c09e3d4be9488b7ac628c225e67f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-machine-learning-services-with-python"></a>SQL Server-Machine Learning-Dienste mit Python
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
