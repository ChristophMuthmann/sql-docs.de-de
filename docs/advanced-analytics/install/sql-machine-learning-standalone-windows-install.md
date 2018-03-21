---
title: "Installieren von SQL Server 2017 Machine Learning-Server (eigenständig) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 5dcc5ee16f39ac8612106f40f98c4f85a060ec4d
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2017-machine-learning-server-standalone-on-windows"></a>Installieren von SQL Server 2017 Machine Learning-Server (eigenständig) unter Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server-Setup umfasst die Option zum Installieren eines Machine learning-Server, der außerhalb von SQL Server ausgeführt wird. Diese Option ist möglicherweise nützlich, wenn Sie zum Entwickeln von hohe Leistung Machine learning, Lösungen, die remote können Kontexten zu berechnen, Synonym Wechseln zwischen dem lokalen Server und einem Machine Learning-Remoteserver auf einem Spark-Cluster oder auf einem anderen SQL Server -Instanz.
  
Dieser Artikel beschreibt, wie SQL Server-Setup zum Installieren der eigenständigen Version des **Server mit SQL Server 2017 Machine Learning**. Wenn Sie eine Enterprise Edition oder Software Assurance verfügen, ist die Installation des eigenständigen Machine Learning-Servers kostenlos.

## <a name="bkmk_prereqs"> </a> Prüfliste vor der Installation

SQL Server-2017 ist erforderlich. Wenn Sie SQL Server 2016 haben, installieren Sie [SQL Server 2016 R Server (eigenständig)](sql-r-standalone-windows-install.md) stattdessen.

Bei der Installation einer früheren Version, z. B. SQL Server 2016 R Server (eigenständig) oder Microsoft R Server, deinstallieren Sie die vorhandene Installation, bevor Sie fortfahren.

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Ausführen von 'Setup'

Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.

1. Starten Sie den Setup-Assistenten für SQL Server-2017.

2. Klicken Sie auf die **Installation** , und wählen Sie **neue Machine Learning-Server (Standalone) Installation**.
    
     ![Machine Learning Server eigenständige Installation](media/2017setup-installation-page-mlsvr.png "Starten der Installation von Machine Learning einen eigenständigen Server")

3. Nachdem die Überprüfung der Regeln abgeschlossen ist, akzeptieren Sie SQL Server-Lizenzbedingungen, und wählen Sie eine neue Installation.

4. Auf der **Funktionsauswahl** Seite die folgenden Optionen sollte bereits ausgewählt werden:

    - Microsoft-Machine Learning-Server (eigenständig)

    - R und Python werden beide standardmäßig ausgewählt. Sie können entweder Sprache deaktivieren, aber es wird empfohlen, dass Sie mindestens eine der unterstützten Sprachen installieren.

     ![Machine Learning Server eigenständige Installation](media/2017setup-features-page-mlsvr-rpy.png "Starten der Installation von Machine Learning einen eigenständigen Server")
    
    Alle anderen Optionen sollten ignoriert werden. 
    
    > [!NOTE]
    > Vermeiden Sie die Installation der **gemeinsam genutzte Funktionen** verfügt der Computer bereits Machine Learning-Services für SQL Server in der Datenbank Analytics installiert. Dadurch wird die doppelte Bibliotheken erstellt.
    > 
    > Darüber hinaus während R oder Python-Skripts, die in SQL Server ausgeführt, die von SQL Server nicht in Konflikt mit der von anderen Datenbankmoduldienste belegte verwaltet werden, der eigenständigen Machine Learning-Server hat keine solchen Einschränkungen und kann mit anderen Datenbankvorgängen beeinträchtigen . Schließlich wird der Remotezugriff über RDP-Sitzung, die häufig für operationalisierung verwendet wird, in der Regel von Datenbankadministratoren blockiert.
    > 
    > Aus diesen Gründen empfehlen wir in der Regel, Machine Learning-Server (eigenständig) auf demselben Computer wie SQL Server-Machine Learning-Services zu installieren.

5.  Akzeptieren Sie die Lizenzbedingungen für das Herunterladen und Installieren von Machine learning-Komponenten. Wenn Sie beide Sprachen installieren, ist eine separate Lizenzvertrag für Microsoft R und Python erforderlich.
    
     ![Python-Lizenzvertrag](media/2017setup-python-license.png "Python-Lizenzvertrag")
    
    Die Installation dieser Komponenten und alle erforderlichen Komponenten, die sie benötigen, die kann eine Weile dauern. Wenn die Schaltfläche **Annehmen** deaktiviert wird, können Sie auf **Weiter**klicken.

6.  Überprüfen Sie Ihre Auswahl auf der Seite **Installationsbereit** , und klicken Sie anschließend auf **Installieren**.

### <a name="default-installation-folders"></a>Standard-Installationsordner

Bei der Installation von R-Server oder Machine Learning-Servers mit SQL Server-Setup werden R-Bibliotheken installiert, in einem Ordner, der SQL Server-Version, die Sie für das Setup verwendet zugeordnet. In diesem Ordner finden Sie auch Beispieldaten, die Dokumentation für die R-Basispakete und die Dokumentation von R-Tools und der Laufzeit.

Allerdings werden bei der Installation mit dem separate Windows Installer oder führen Sie ein upgrade des separaten Windows Installers, R-Bibliotheken in einem anderen Ordner installiert.

Nur zu Referenzzwecken werden, wenn Sie eine Instanz von SQL Server R Services (Datenbankintern) "oder" Machine Learning-Services (Datenbankintern) installiert haben und diese Instanz befindet sich auf demselben Computer ausführen, die R-Bibliotheken und Tools standardmäßig in einem anderen Ordner installiert.

Die folgende Tabelle enthält die Pfade für jede Installation.

|Version| Installationsmethode | Standardordner|
|----|----|----|
|SQL Server 2017 Machine Learning-Server (eigenständig) |  2017 von SQL Server-Setup-Assistenten |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft-Machine Learning-Server (eigenständig) |  Eigenständiges Windows-Installationsprogramm |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Services (Datenbankintern) |2017 von SQL Server-Setup-Assistenten, mit der Option für R-Sprache|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016-R-Server (eigenständig) |  SQL Server 2016-Setup-Assistenten |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (Datenbankintern) |SQL Server 2016-Setup-Assistenten|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

## <a name="development-tools"></a>Entwicklungstools

Eine Entwicklungsaufgabe IDE ist nicht als Teil von Setup installiert. Zusätzliche Tools sind nicht erforderlich, da alle Standardtools eingeschlossen werden würde, die mit einer Verteilung von R oder Python angegeben werden.

Es wird empfohlen, dass Sie die neue Version von versuchen [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] oder [Python für Visual Studio](https://docs.microsoft.com/en-us/visualstudio/python/installing-python-support-in-visual-studio). Visual Studio unterstützt sowohl R und Python sowie Tools zur Datenbankentwicklung, Konnektivität mit SQL Server und BI-Tools. Sie können jedoch bevorzugte Entwicklungsumgebung einschließlich RStudio.

## <a name="get-help"></a>Abrufen von Hilfe

Benötigen Sie Hilfe bei der Installation oder Aktualisierung? Antworten auf häufig gestellte Fragen und bekannte Probleme finden Sie im folgenden Artikel:

* [Upgrade und Installation häufig gestellte Fragen – Machine Learning-Dienste](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Überprüfen Sie den Installationsstatus der Instanz, und beheben Probleme, wiederholen Sie dann diese benutzerdefinierten Berichte.

* [Benutzerdefinierte Berichte für SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Nächste Schritte

R-Entwickler können mit einigen einfachen Beispielen beginnen und die Grundlagen der Funktionsweise von R mit SQL Server. Im nächsten Schritt finden Sie unter den folgenden Links:

+ [Lernprogramm: Ausführen von R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Lernprogramm: In-Database-Analyse für R-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python-Entwickler können zum Verwenden von Python mit SQL Server gemäß diesen Lernprogrammen erfahren:

+ [Lernprogramm: Ausführen von Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Lernprogramm: In-Database-Analyse für Python-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).
