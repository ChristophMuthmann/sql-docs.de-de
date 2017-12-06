---
title: Was &#39; s neu in Machine Learning Services | Microsoft Docs
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5bfdab27d2d071d93e78bec2d48244f8a7bcb803
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>Was ist neu in Machine Learning Services in SQL Server

In SQL Server 2016 eingeführt Microsoft SQL Server R Services, eine Funktion, die Enterprise-Skalierung Data Science, durch die Integration von der Sprache "R" mit dem SQL Server-Datenbankmodul unterstützt.

Im SQL Server 2017 wurde die Datenbank integriert Machine Learning noch leistungsfähiger, durch Hinzufügen der Unterstützung für die beliebten Python-Sprache. Die Unterstützung für neue Sprachen enthalten ist ein neuer Name: **Machine Learning-Services (Datenbankintern)**.

Fangen Sie hier die neueste Ankündigung! [Python in SQL Server-2017: Erweiterte in Datenbank-Machine Learning](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017"></a>Neues in SQL Server 2017

Machine Learning-Server in SQL Server bietet eine umfassende Unterstützung für das Erstellen und Bereitstellen von Machine Learning-Lösungen in R oder Python. Hier sind die wichtigsten dieser Version:

### <a name="whats-new-in-cumulative-update-1-for-sql-server-2017"></a>Neues im kumulativen Update 1 für SQL Server-2017

Sie können jetzt die Python- und R-Komponenten auf Machine Learning-Servers 9.2.1.24 aktualisieren. Diese Version bietet zahlreiche Verbesserungen zu **Revoscalepy** und **"revoscaler"**, einschließlich leistungsverbesserungen.

### <a name="in-database-python-integration"></a>Python-Integration in der Datenbank

Sie können Python in gespeicherten Prozeduren ausführen oder Python Remote mithilfe von SQL Server-Computers als computekontext auszuführen. Diese Integration eröffnet neue Möglichkeiten für die großen Community von Python-Entwickler und Datenanalysten ausnutzen der Leistungsfähigkeit von SQL Server.

SQL Server-Entwickler können Sie zugreifen, die eine umfangreiche Python-Bibliotheken in open-Source-Ökosystem, einschließlich gängigen Frameworks wie Scikit-TensorFlow Caffe und Theano/Keras finden. Und achten Sie darauf, wie z. B. Innovationen von Microsoft Durchsuchen **Revoscalepy** und **Microsoftml**!

Ausgeführte Python, die nur in der Datenbank ist nicht "machine learning, wie". Es gibt unzählige andere Anwendungen für die Integration von Python mit SQL, und verwenden die Leistungsfähigkeit der einzelnen Sprachen zur Bereitstellung von intelligenter, leistungsstarker Lösungen.

+ **revoscalepy**

    Diese Version enthält die endgültige Version von **Revoscalepy**, die Python-Entsprechungen der Algorithmen im "revoscaler" ausgeben. Sie können die Python-Modelle für linear und logistische Regressionen, Entscheidungsstrukturen, verstärkten Bäumen und zufällige Gesamtstrukturen, alle parallelisiert und kann in remote rechenkontexte ausgeführt erstellen.

    Weitere Informationen finden Sie unter [neuerungen Revoscalepy](python/what-is-revoscalepy.md).

+ Remote rechenkontexte für Python

    Diese Version unterstützt die Verwendung von mehreren Datenquellen und remote rechenkontexte. Der datenanalyst oder Entwickler kann Python-Code auf einem remote-SQL-Server zum Durchsuchen von Daten oder Modelle erstellen, ohne Verschieben von Daten ausführen. Verwendung von remote rechenkontexte erfordert **Revoscalepy**.

+ Python-Unterstützung in Microsoft Machine Learning-Server (eigenständig)

    [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]Schließt die Möglichkeit, eine eigenständige Version von Microsoft Machine Learning-Server installieren. Mithilfe von Machine Learning-Server können Sie verteilen und Skalieren von R oder Python-Code ohne Verwendung von SQL Server.

### <a name="linux-support"></a>Linux-Unterstützung

Machine Learning mithilfe von R oder Python in der Datenbank ist derzeit nicht in SQL Server on Linux unterstützt. Suchen Sie nach Ankündigungen in einer späteren Version.

Allerdings unter Linux können Sie ausführen [native Bewertung](sql-native-scoring.md) mit der VORHERSAGE von T-SQL-Funktion. Systemeigene Bewertung können Sie aus einem vortrainierte Modell sehr schnell zu bewerten, ohne aufrufen oder sogar eine R-Laufzeit erfordern. Dies bedeutet, dass Sie SQL Server on Linux verwenden können, zum Generieren von Vorhersagen, die sehr schnell, um Clientanwendungen zu fungieren.

### <a name="new-algorithms"></a>Neue Algorithmen

Die **MicrosoftML** -Paket für R und Python enthält der Technik Machine Learning-Algorithmen und von remotecomputekontexten Datentransformation, die skalierte oder Ausführen in Remote sein können. Algorithmen sind anpassbare Tiefe neuronale Netzwerke, schnelle Entscheidungsstrukturen und entscheidungswälder, lineare Regression und logistische Regression. Das Paket MicrosoftML im Lieferumfang von R und Python-Schnittstellen.

Weitere Informationen finden Sie unter [Einführung in MicrosoftML](using-the-microsoftml-package.md) und [Microsoftml für Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package).

### <a name="operationalization"></a>Operationalisierung

Diese Version enthält mehrere Optionen und Features, mit denen Sie die Bereitstellung und Verteilen von Machine Learning-Aufgaben:

+ Bereitstellen Sie und integrieren Sie Computer Python-Lösungen mithilfe des T-SQL

    Die Integration von Python mit T-SQL bedeutet, dass Sie eine beliebige Python-Code mit aufrufen, können `sp_execute_external_script`. Diese sichere Infrastruktur ermöglicht die Bereitstellung von Enterprise-Grade von Python-Modellen und Skripts, die von einer Anwendung mithilfe einer einfachen gespeicherten Prozedur aufgerufen werden können. Zusätzlicher Leistung wird durch streaming von Daten aus SQL Python-Prozesse und MPI Ring Parallelisierung.

+ **Mrsdeploy** für Python

    Die **Mrsdeploy** für Paket [!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)] und [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] unterstützt die Bereitstellung von Python-Modellen und Skripts als Webdienste. Ein Beispiel dafür, wie es funktioniert, finden Sie unter [veröffentlichen und Nutzen von Python-Code](python/publish-consume-python-code.md).

+ Leistung

    Microsoft hat die Grenzen der Leistung für die Bewertung abgelegt. Mit in der Datenbank zu bewerten, die wir verarbeitet eine Million Zeilen, die pro Sekunde, mit der R-Modelle. In dieser Version neue Features für **Echtzeit Bewertung** und **native Bewertung** unterstützen eine bessere Leistung in einzeiligen und batchbewertung.

### <a name="realtime-scoring-and-native-scoring"></a>Echtzeit-Bewertung und systemeigene Bewertung

Echtzeit-Bewertung basiert auf systemeigene C++-Bibliotheken zum Lesen eines Modells in einem optimierten Binärformat gespeichert und anschließend Vorhersagen generieren, ohne die R-Laufzeitversion aufrufen zu müssen. Auf diese Weise bewerteten Vorgänge schneller.

Darüber hinaus diese Version von [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)] eine systemeigene T-SQL-Funktion enthält, für Fast Bewertung, die auf eine beliebige Edition von SQL Server, sogar auf Linux ausgeführt werden kann. Die Funktion erfordert keine Installation von R oder zusätzliche Konfiguration. Dies bedeutet, dass Sie an anderer Stelle ein Modell trainieren, speichern Sie sie in SQL Server und führen Sie bewerten, ohne jemals aufrufen r Diese Funktion wird als bezeichnet _native Bewertung_.

  - Systemeigene Bewertung steht nur in [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]. Er verwendet eine T-SQL-Funktion, die in jeder Edition von SQL Server, einschließlich Linux ausgeführt werden kann.
 - Echtzeit-Bewertung wird im unterstützt [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)], und klicken Sie im Microsoft Machine Learning-Server. Sie können eine gespeicherte Prozedur oder ausführen Echtzeit Bewertung von R-Code.
 - Echtzeit-Bewertung ist auch für SQL Server 2016 verfügbar, wenn die Instanz, auf die neueste Version von aktualisiert wird [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)].

Weitere Informationen dazu finden Sie in diesen Artikeln:

 + [Echtzeit-Bewertung](real-time-scoring.md)
 + [Native Bewertung](sql-native-scoring.md)
 + [Zum Ausführen von Realtime Bewertung oder systemeigenen bewerten](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-machine-learning-experience-and-get-pre-trained-models"></a>Upgrade des Computers Lernerfahrung und vorab trainierten Modelle abzurufen

Wenn Sie eine frühere Version von SQL Server 2016 R Services installiert haben, können Sie nun auf die neueste Version aktualisieren, durch den Wechsel Ihres Servers, sodass die moderne Software Lifecycle-Richtlinie verwenden. Auf diese Weise können Sie eine schnellere Releasezyklus für R nutzen und alle R-Komponenten automatisch aktualisiert. Weitere Informationen finden Sie unter [Neuigkeiten in Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/whats-new-in-machine-learning-server).

Der Installer bietet außerdem die Möglichkeit, eine Auflistung von Pre-tained Modelle im Binärformat zu installieren. Diese Modelle unterstützen Machine Learning in Szenarien wie z. B. bilderkennung, in denen es Kunden, um große Datasets zum Trainieren eines Modells suchen schwierig sein kann. Nach der Installation eines der Pre-tained Modelle können Sie es für die Vorhersage auf Ihren eigenen Daten ohne den Zeit- und Kostenaufwand beteiligten trainieren ein solches Modell große und komplexe verwenden.

Weitere Informationen finden Sie unter [vorab trainierten Modelle in SQL Server installieren](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>Paketverwaltung

Diese Version umfasst viele Verbesserungen bei der paketverwaltung für SQL Server. Dazu gehören:

- Datenbankrollen können der DBA-Pakete verwalten und Zuweisen von Berechtigungen zum Installieren der Pakete
- Erstellen EXTERNEN LIBRARY-Anweisung in T-SQL, um Pakete zu verwalten, ohne Wissen der R DBAs zu
- Ein umfangreichen Satz von R-Funktionen zu installieren, entfernen oder eine Liste der Pakete, die im Besitz von Benutzer

Weitere Informationen finden Sie unter [Paket Management](r/r-package-management-for-sql-server-r-services.md).

### <a name="get-started"></a>Erste Schritte

+ [Einrichten von Python in SQL Server-Machine Learning-Services](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [Einrichten von R in SQL Server-Machine Learning-Services](r/set-up-sql-server-r-services-in-database.md)

+ [Machine Learning-Lernprogramme und Beispiele](tutorials/machine-learning-services-tutorials.md)
