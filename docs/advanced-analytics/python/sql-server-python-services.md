---
title: SQL Server R Services | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 140885b86f0f6fa1a56119246c859f143f596726
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="machine-learning-services-with-python"></a>Machine Learning-Dienste mit Python

Python ist eine Programmiersprache, die hohe Flexibilität und Leistungsfähigkeit für eine Vielzahl von Machine learning-Aufgaben bietet. Für Python-Open Source-Bibliotheken enthalten mehrere Plattformen für anpassbare neuronale Netzwerke sowie beliebte Bibliotheken für die Verarbeitung natürlicher Sprache. Diese weit verbreiteten Sprache wird jetzt in SQL Server 2017 CTP 2.0 und höher unterstützt.

Da Python integriert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankmodul, können Sie Analysen in der Nähe der Daten und zu vermeiden, die Kosten und Sicherheitsrisiken durch Verschieben von Daten.  Sie können die Machine Learning Projektmappen auf Grundlage von Python mit geeigneten, vertrauten Tools wie Visual Studio bereitstellen. Ihre Produktionsanwendungen können Vorhersagen, Modelle, Abrufen oder visuellen Elementen aus der Python-3.5-Laufzeit durch Aufrufen von einfach einen T-SQL-Prozedur.

Diese Version enthält die Anaconda-Verteilung von Python als auch das neue [Revoscalepy](../python/what-is-revoscalepy.md) Bibliothek, um die Skalierung und Leistung von Ihrer für maschinelles lernen von Lösungen zu verbessern.

Sie können alles installieren müssen Sie mit Python mithilfe von 2017 von SQL Server-Setup zu beginnen:

+ **Machine Learning-Services (Datenbankintern):** installieren Sie diese Funktion, zusammen mit der SQL Server-Datenbankmodul, um sichere Ausführung von R-Skripts auf ermöglichen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.
  
     Wenn Sie dieses Feature auswählen, Erweiterungen im Datenbankmodul zur Unterstützung der Ausführung von Python-Skripts installiert sind und ein neuer Dienst erstellt, die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], um die Verwaltung der Kommunikation zwischen der Python-Laufzeit und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.

+ **Machine Learning-Server (eigenständig):** , wenn Sie SQL Server-Integration nicht benötigen, installieren Sie diese Funktion, um in Microsoft R Server Python-Unterstützung zu erhalten. Auf diese Weise können Sie die Python-Lösungen mit operationalisieren **Mrsdeploy**.
  
     Installieren Sie dieses Feature nicht auf demselben Computer, auf dem SQL Server-Machine Learning-Services ausgeführt wird.


## <a name="additional-resources"></a>Weitere Ressourcen

[Einrichten von Python-Machine Learning-In-Database-Dienste](setup-python-machine-learning-services.md)

[Python-Lernprogramme](../tutorials/sql-server-python-tutorials.md)
