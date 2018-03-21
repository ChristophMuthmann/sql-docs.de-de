---
title: "Erste Schritte mit Microsoft R Server (Eigenständig) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: b7a9ec054b512e8825bf5cf9208a0c1deb3abbb8
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2018
---
# <a name="getting-started-with-machine-learning-server-standalone"></a>Erste Schritte mit Machine Learning-Server (eigenständig)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
Microsoft R Server (eigenständig) wird in SQL Server 2016 geholfen, schalten Sie die beliebte open Source-R-Sprache in das Unternehmen, um leistungsfähige analyselösungen und Integration mit anderen Geschäftsanwendungen zu aktivieren.  

In SQL Server 2017 wurde der Name in Machine Learning-Server (eigenständig) das Hinzufügen der Unterstützung für die Sprache Python entsprechend geändert. Beide Versionen sind kostenlos für Benutzer der Enterprise Edition oder Software Assurance verfügbar.

Dieser Artikel bietet einen allgemeinen Überblick darüber, wie Sie Machine Learning-Server (oder R-Server) verwenden können und wie beim Installieren und Beispiele zu beginnen.

## <a name="why-use-a-standalone-server-for-machine-learning"></a>Gründe für die Verwendung eines eigenständigen Servers für Machine learning

Wenn Sie zum Integrieren Ihrer für maschinelles lernen von Lösungen mit SQL Server-Daten benötigen, Machine Learning-Server bietet Ihnen die gleiche verteilte, skalierbare Unterstützung für R und Python und darüber hinaus unterstützt die Bereitstellung von Lösungen für Hadoop, Spark oder Linux.

Machine Learning-Server enthält außerdem vorab trainierten Modelle für bildanalysen und stimmungsanalyse, die Sie sofort in Anwendungen verwenden können.

Operationalisierung Funktionen von Machine Learning-Server bereitstellen und Verteilen von R und Python-Lösungen mithilfe von Webdiensten mit remote-Ausführung, gruppierten Topologien für Spark und Hadoop MapReduce, Unterstützung und Unterstützung für Windows oder Linux.

**SQL Server 2016**

+ Installieren Sie Microsoft R Server (eigenständig) von SQL Server 2016-Setup.

    Diese Option erstellt einen eigenständiger Server, der vollständig unabhängig von R Services (Datenbankintern) ist. Diese Version unterstützt nur R. Setup von einem eigenständigen Server ist in der Supportrichtlinie für SQL Server Enterprise Edition enthalten. Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R-Servers](../../advanced-analytics/r/create-a-standalone-r-server.md).

+ Installieren von R-Server über separate Windows Installer.

    Das Installationsprogramm erstellt eine völlig neue Instanz von Microsoft R Server, die die moderne Software-Lebenszyklus von Microsoft Support-Richtlinie verwendet. Sie können auch R Server für Linux, Cloudera, Teradata und Hadoop installieren.
    
    Weitere Informationen finden Sie unter [Installieren von R Server 9.1 für Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

**SQL Server 2017**

+ Installieren Sie Machine Learning-Server (eigenständig) von 2017 von SQL Server-Setup. 

    Diese Option erstellt einen eigenständiger Server zur Unterstützung von operationalisierung von für maschinelles lernen in R, Python oder beides. Setup von einem eigenständigen Server ist in der Supportrichtlinie für SQL Server Enterprise Edition enthalten. Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R-Servers](../../advanced-analytics/r/create-a-standalone-r-server.md).  

+ Verwenden Sie den neuen eigenständigen Windows Installer.

    Diese Methode erstellt eine neue Instanz der Machine Learning-Server, die die moderne Software-Lebenszyklus von Microsoft Support-Richtlinie verwendet. Sie können auch Machine Learning-Server auf Hadoop, Spark oder Linux installieren, ohne zusätzliche Kosten.
    
    Weitere Informationen finden Sie unter [Machine Learning-Server für Windows installieren](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

**Aktualisieren eines vorhandenen Servers**

+ Wenn Sie einen vorhandenen Server oder -Instanz, die Sie aktualisieren möchten, laden Sie, und führen Sie die Windows-basierten Installationsprogramm aus, um die Updates zu erhalten. 

    Weitere Informationen finden Sie unter [SqlBindR verwenden, zum Aktualisieren einer Instanz](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="start-using-machine-learning-server"></a>Starten der Verwendung von Machine Learning-Server

 Nachdem Sie die Serverkomponenten eingerichtet und konfiguriert die IDE, um die Machine Learning-Binärdateien verwenden haben, können Sie mit der Entwicklung Ihrer Lösung mithilfe der neuen APIs, wie z. B. "revoscaler" und Revoscalepy, MicrosoftML und die OlapR beginnen.
    
Um zu beginnen, finden Sie in diesen Handbüchern:

+ [Projektmappenvorlagen](https://docs.microsoft.com/machine-learning-server/r/sample-solutions)

    Thesen Beispiele gibt Lösungen, die veranschaulichen, wie Machine Learning in bestimmten Branchen gelten. Aktuelle Szenarien sind im Einzelhandel, Finanzen, Gesundheitswesen und Marketing.

+ [Untersuchen Sie R und ScaleR in 25 Funktionen](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Untersuchen Sie diese Sammlung von verteilbaren analytischen Funktionen, die hohe Leistung und Skalierung auf R-Lösungen bereitstellen. Enthält parallelisierbare Versionen von vielen der beliebtesten R-Modellierpakete wie K-Means-Clustering, Entscheidungsstrukturen, Entscheidungswälder und Tools für die Datenbearbeitung.

- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)

    Das MicrosoftML-Paket ist eine Reihe von neuen Machine learning-Algorithmen und Transformationen, die bei Microsoft entwickelt, die schnell und skalierbar sind. Sie können es in R oder Python verwenden. Weitere Informationen finden Sie unter [MicrosoftML für Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) und [MicrosoftML für R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).

## <a name="see-also"></a>Siehe auch

[Erste Schritte mit SQL Server-Machine Learning-Dienste](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)