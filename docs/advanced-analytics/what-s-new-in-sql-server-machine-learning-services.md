---
title: Was&#39;s ist neu in SQL Server-Machine Learning-Services | Microsoft Docs
ms.date: 03/17/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 07c21de29f41826d1314f92f77fd9277f84cb0e7
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Neuigkeiten in SQL Server-Machine Learning-Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Machine Learning-Funktionen werden in SQL Server in jeder Version eingefügt, weiterhin zu erweitern, erweitern und die Integration zwischen die Plattform und die Data Science, Analyse und vertiefen und lernen, die Sie implementieren, über Ihre Daten möchten überwacht. 

## <a name="new-in-sql-server-2017"></a>Neu in SQLServer 2017

Diese Version hinzugefügt, Unterstützung der Python- und branchenführende Machine learning-Algorithmen. Entsprechend den neuen Bereich umbenannt, SQL Server-2017 markiert die Einführung von **SQL Server Machine Learning-Services (Datenbankintern)**, mit der sprachunterstützung für Python und r angezeigt. 

Diese Version auch eingeführt **SQL Server Machine Learning-Server (eigenständig)**, völlig unabhängig von der SQL-Server für R und Python-arbeitsauslastungen, die auf einem dedizierten System ausgeführt werden soll. Mit dem eigenständigen Server können Sie verteilen und Skalieren von R oder Python-Lösungen ohne Verwendung von SQL Server.

| Release | Feature-update |
|---------|---------------|
| CU 4 | Fehlerkorrekturen und paketerneuerung, jedoch keine Funktion neue Ankündigungen. |
| CU 3 | Python modellieren Serialisierung in Revoscalepy, mit der [Rx_serialize_model Funktion](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/><br/>[Bewerten von systemeigenen](sql-native-scoring.md) plus Verbesserungen [Echtzeit Bewertung](real-time-scoring.md). In der Datenbank zu bewerten, Durchsatz ist eine Million Zeilen, die pro Sekunde, mit der R-Modelle. In diesem Update bieten Echtzeit Bewertung und systemeigene Bewertung eine bessere Leistung in einzeiligen und batchbewertung. Systemeigene Bewertung verwendet kann eine T-SQL-Funktion zur schnellen Bewertung, die auf eine beliebige Edition von SQL Server, sogar auf Linux ausgeführt werden. Die Funktion erfordert keine Installation von R oder zusätzliche Konfiguration. Dies bedeutet, dass Sie an anderer Stelle ein Modell trainieren, speichern Sie sie in SQL Server und führen Sie bewerten, ohne jemals aufrufen r Weitere Informationen zum Bewerten von Methoden, finden Sie unter [zum Ausführen von Realtime Bewertung oder systemeigenen bewerten](r/how-to-do-realtime-scoring.md). |
| CU 2 | Fehlerkorrekturen und paketerneuerung, jedoch keine Funktion neue Ankündigungen. |
| CU 1 | In Revoscalepy, fügt Rx_create_col_info für die Rückgabe von Schemainformationen aus einer SQL Server-Datenquelle, die ähnlich wie [RxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) für R. <br/><br/>Verbesserungen an [Rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) zur Unterstützung paralleler Szenarien, die mit der `RxLocalParallel` computekontext.|
| Erste Veröffentlichung |[**Python-Integration für die Analyse in der Datenbank**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>Die [Revoscalepy](python/what-is-revoscalepy.md) Paket ist die Python-Entsprechung von "revoscaler". Sie können die Python-Modelle für linear und logistische Regressionen, Entscheidungsstrukturen, verstärkten Bäumen und zufällige Gesamtstrukturen, alle parallelisiert und kann in remote rechenkontexte ausgeführt erstellen. Dieses Paket unterstützt die Verwendung von mehreren Datenquellen und remote rechenkontexte. Der datenanalyst oder Entwickler kann Python-Code auf einem remote-SQL-Server zum Durchsuchen von Daten oder Modelle erstellen, ohne Verschieben von Daten ausführen. <br/><br/>Die [Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) Paket ist die Python-Entsprechung des MicrosoftML R-Pakets.<br/><br/>T-SQL und Python-Integration über [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Sie können eine beliebige Python-Code, der mit dieser gespeicherten Prozedur aufrufen. Diese sichere Infrastruktur ermöglicht die Bereitstellung von Enterprise-Grade von Python-Modellen und Skripts, die von einer Anwendung mithilfe einer einfachen gespeicherten Prozedur aufgerufen werden können. Zusätzliche Leistungssteigerungen werden durch streaming von Daten aus SQL Python-Prozesse und MPI Ring Parallelisierung erreicht. <br/><br/>Können Sie die T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) Funktion ausführen [native Bewertung](sql-native-scoring.md) auf ein vortrainiertes Modell, die zuvor in das erforderliche Binärformat gespeichert wurde.|
| Erste Veröffentlichung | [**MicrosoftML (R)** ](using-the-microsoftml-package.md) enthält das ClipArt-Machine learning-Algorithmen und die Datentransformation, die skalierte oder Ausführen in remote rechenkontexte sein können. Algorithmen sind anpassbare Tiefe neuronale Netzwerke, schnelle Entscheidungsstrukturen und entscheidungswälder, lineare Regression und logistische Regression. |
| Erste Veröffentlichung | [**Pre-tained Modelle** ](r/install-pretrained-models-sql-server.md) für bilderkennung und positiv Negative stimmungsanalyse. Verwenden Sie diese Modelle, um auf Ihre eigenen Daten Vorhersagen zu generieren. |
| Erste Veröffentlichung | [**Paket Management**](r/r-package-management-for-sql-server-r-services.md), einschließlich der folgenden Vorteilen: Datenbankrollen können der DBA-Pakete verwalten und Zuweisen von Berechtigungen zum Installieren der Pakete, [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) in T-SQL-Anweisung Hilfe DBAs Pakete verwalten, ohne Wissen der R sowie ein umfangreichen Satz von R-Funktionen in ["revoscaler"](r/use-revoscaler-to-manage-r-packages.md) zu installieren, entfernen oder Pakete auflisten Besitz des Benutzers. |
| Erste Veröffentlichung | [**Operationalisierung über Mrsdeploy** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) für die Bereitstellung und hosting von R-Skript als Webdienst. Gilt für nur R-Skript (keine Python-Entsprechung). Vorgesehen für die Serveroption (eigenständig), um Ressourcen Wettbewerb mit anderen SQL Server-Vorgängen zu vermeiden. |


## <a name="new-in-sql-server-2016"></a>Neu in SQLServer 2016

Diese Version eingeführt wurden computerlernverfahren-Funktionen in SQL Server über **SQL Server 2016 R Services**, ein Modul in der Datenbank für die von R-Verarbeitungsskript für residenten Daten innerhalb einer Datenbank-Modulinstanz.

Darüber hinaus **SQL Server 2016 R Server (eigenständig)** als eine Möglichkeit zum Installieren von R Server auf einem WindowsServer veröffentlicht wurde. SQL Server-Setup hinterlegt, die die einzige Möglichkeit zum Installieren von R Server für Windows. In späteren Versionen konnte Entwickler und Datenanalysten, die die R-Server unter Windows wollten eine andere eigenständige Installer verwenden, um das gleiche Ziel zu erreichen. Der eigenständige Server in SQL Server ist funktionell gleichwertig mit der eigenständige Server-Produkts [Microsoft R Server für Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

| Release |Feature-update |
|---------|----------------|
| CU | [**Bewerten von Realtime** ](real-time-scoring.md) basiert auf systemeigene C++-Bibliotheken zum Lesen eines Modells in einem optimierten Binärformat gespeichert und anschließend Vorhersagen generieren, ohne die R-Laufzeitversion aufrufen zu müssen. Auf diese Weise bewerteten Vorgänge schneller. Mit Echtzeit bewerten zu können, können Sie eine gespeicherte Prozedur auszuführen oder Echtzeit Bewertung von R-Code ausführen. Echtzeit-Bewertung ist auch für SQL Server 2016 verfügbar, wenn die Instanz, auf die neueste Version von aktualisiert wird [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Erste Veröffentlichung | [**R-Integration für die Analyse in der Datenbank**](r/sql-server-r-services.md). <br/><br/> R-Pakete für die aufrufende R-Funktionen in T-SQL (und umgekehrt). RevoScaleR-Funktionen R Analytics Größenordnungen bereitstellen, indem Sie Segmentierung der Daten in Bestandteile, koordinieren und Verwalten von verteilte Verarbeitung und aggregieren Ergebnisse. In SQL Server 2016 R Services (Datenbankintern) ist das Modul "revoscaler" in eine Datenbankmodulinstanz, die Daten und Analysen, die zusammen in demselben Verarbeitungskontext sind integriert. <br/><br/>T-SQL und R-Integration über [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Sie können eine beliebige R-Code, der mit dieser gespeicherten Prozedur aufrufen. Diese sichere Infrastruktur ermöglicht die Bereitstellung der Unternehmensklasse Rn Modelle und Skripts, die von einer Anwendung mithilfe einer einfachen gespeicherten Prozedur aufgerufen werden können. Zusätzliche Leistungssteigerungen werden durch streaming von Daten aus SQL R-Prozesse und MPI Ring Parallelisierung erreicht. <br/><br/>Können Sie die T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) Funktion ausführen [native Bewertung](sql-native-scoring.md) auf ein vortrainiertes Modell, die zuvor in das erforderliche Binärformat gespeichert wurde.|

## <a name="linux-support-roadmap"></a>Roadmap für die Linux-Unterstützung

Machine Learning mithilfe von R oder Python in der Datenbank ist derzeit nicht in SQL Server on Linux unterstützt. Suchen Sie nach Ankündigungen in einer späteren Version.

Allerdings unter Linux können Sie ausführen [native Bewertung](sql-native-scoring.md) mit der VORHERSAGE von T-SQL-Funktion. Systemeigene Bewertung können Sie aus einem vortrainierte Modell sehr schnell zu bewerten, ohne aufrufen oder sogar eine R-Laufzeit erfordern. Dies bedeutet, dass Sie SQL Server on Linux verwenden können, zum Generieren von Vorhersagen, die sehr schnell, um Clientanwendungen zu fungieren.

## <a name="next-steps"></a>Nächste Schritte

+ [Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern)](install/sql-machine-learning-services-windows-install.md)
+ [Machine Learning-Lernprogramme und Beispiele](tutorials/machine-learning-services-tutorials.md)
