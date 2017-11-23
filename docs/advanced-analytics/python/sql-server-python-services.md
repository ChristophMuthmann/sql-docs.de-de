---
title: Machine Learning-Dienste mit Python | Microsoft Docs
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: af81754d0e6b87546432ea864098da4615522670
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="machine-learning-services-with-python"></a>Machine Learning-Dienste mit Python

Python ist eine Programmiersprache, die hohe Flexibilität und Leistungsfähigkeit für eine Vielzahl von Machine learning-Aufgaben bietet. Für Python-Open Source-Bibliotheken enthalten mehrere Plattformen für anpassbare neuronale Netzwerke sowie beliebte Bibliotheken für die Verarbeitung natürlicher Sprache. Diese weit verbreiteten Sprache wird jetzt in SQL Server 2017 CTP 2.0 und höher unterstützt.

Da Python integriert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankmodul, können Sie Analysen in der Nähe der Daten und zu vermeiden, die Kosten und Sicherheitsrisiken durch Verschieben von Daten.  Sie können die Machine Learning Projektmappen auf Grundlage von Python mit geeigneten, vertrauten Tools wie Visual Studio bereitstellen. Ihre Produktionsanwendungen können Vorhersagen, Modelle, Abrufen oder visuellen Elementen aus der Python-3.5-Laufzeit durch Aufrufen von einfach einen T-SQL-Prozedur.

Diese Version enthält die Anaconda-Verteilung von Python als auch das neue [Revoscalepy](../python/what-is-revoscalepy.md) Bibliothek, um die Skalierung und Leistung von Ihrer für maschinelles lernen von Lösungen zu verbessern.

Sie können alles installieren müssen Sie mit Python mithilfe von 2017 von SQL Server-Setup zu beginnen:

+ **Machine Learning-Services (Datenbankintern):** installieren Sie diese Funktion, zusammen mit der SQL Server-Datenbankmodul verwenden, um sichere Ausführung von Python-Skripts auf ermöglichen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
     Wenn Sie dieses Feature auswählen, Erweiterungen im Datenbankmodul zur Unterstützung der Ausführung von Python-Skripts installiert sind und ein neuer Dienst erstellt, die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], um die Verwaltung der Kommunikation zwischen der Python-Laufzeit und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.

+ **Machine Learning-Server (eigenständig):** , wenn Sie SQL Server-Integration nicht benötigen, installieren Sie diese Funktion, um Python und R-Unterstützung für verteilte Machine Learning zu erhalten. Sie können auch die Python-Projektmappe als Webdienst bereitstellen, mit **Mrsdeploy**.
  
     Installieren Sie dieses Feature nicht auf demselben Computer, auf dem SQL Server-Machine Learning-Services ausgeführt wird.


## <a name="additional-resources"></a>Weitere Ressourcen

[Einrichten von Python-Machine Learning-In-Database-Dienste](setup-python-machine-learning-services.md)

[Python-Lernprogramme](../tutorials/sql-server-python-tutorials.md)
