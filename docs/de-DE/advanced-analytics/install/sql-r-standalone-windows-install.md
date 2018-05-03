---
title: Installieren von SQL Server 2016 R Server (eigenständig) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e7e5b61cb8e41d818fc13d1cc97cd4d998256efc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-2016-r-server-standalone"></a>Installieren von SQL Server 2016 R Server (eigenständig)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt, wie SQL Server 2016-Setup zum Installieren der eigenständigen Version des **SQL Server 2016 R Server**.

## <a name="bkmk_prereqs"> </a> Prüfliste vor der Installation

SQL Server 2016 ist erforderlich. Wenn Sie SQL Server-2017 verfügen, installieren Sie [SQL Server 2017 Machine Learning-Server (eigenständig)](sql-machine-learning-standalone-windows-install.md) stattdessen.

Wenn Sie alle früheren Versionen von Revolution Analytics-Tools bzw. die Pakete installiert, müssen Sie diese zunächst deinstallieren. 

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Installieren einer Patchanforderung 

Microsoft hat ein Problem bei der speziellen Version von Microsoft VC++ 2013 Runtime-Binärdateien erkannt, die von SQL Server als vorausgesetzte Komponenten installiert werden. Wenn dieses Update an den VC++ Runtime-Binärdateien nicht installiert wird, können bei SQL Server in bestimmten Szenarios Stabilitätsprobleme auftreten. Bevor Sie SQL Server installieren, sollten Sie entsprechend den Anweisungen unter [Versionsanmerkungen zu SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) vorgehen, um festzustellen, ob Ihr Computer einen Patch für die VC-Runtime-Binärdateien benötigt.  

## <a name="run-setup"></a>Ausführen von 'Setup'

Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.

1. Starten Sie den Setup-Assistenten für SQL Server 2016. Es wird empfohlen, dass Sie Servicepack 1 oder höher installieren.

2. Auf der **Installation** auf **neue R Server (Standalone) Installation**.
    
     ![Starten Sie das Setup von R Server eigenständigen](media/2016-setup-installation-rsvr.png "starten Sie das Setup von eigenständigen R-Server")
    
3.  Auf der Seite **Feature selection** (Funktionsauswahl) sollte die folgende Option bereits aktiviert sein:
    
    **R Server (eigenständig)**  
    
    ![Funktionsauswahl für einen eigenständigen R Server](media/2016setup-rserver-features.png "Funktionsauswahl für einen eigenständigen R Server")
    
    Alle anderen Optionen können ignoriert werden. 
    
    > [!NOTE]
    > Vermeiden Sie die Installation der **gemeinsam genutzte Funktionen** Wenn Sie Setup auf einem Computer ausführen, bei der es dem R-Dienste bereits für die Analyse von SQL Server in der Datenbank installiert wurde. Dadurch wird die doppelte Bibliotheken erstellt.
    > 
    > Während der R-Skripts, die in SQL Server ausgeführt, die von SQL Server nicht in Konflikt mit der von anderen Datenbankmoduldienste belegte verwaltet werden, dem eigenständigen R-Server hat keine solchen Einschränkungen und kann mit anderen Datenbankvorgängen beeinträchtigen.
    > 
    > Im Allgemeinen wird empfohlen, dass die Installation von R Server (eigenständig) auf einem separaten Computer von SQL Server R Services (Datenbankintern).

4.  Akzeptieren Sie die Lizenzbedingungen für das Herunterladen und Installieren von Microsoft R Open. Wenn die Schaltfläche **Annehmen** deaktiviert wird, können Sie auf **Weiter**klicken.
    
    Die Installation dieser Komponenten und alle erforderlichen Komponenten, die sie benötigen, die kann eine Weile dauern.
    
5.  Überprüfen Sie Ihre Auswahl auf der Seite **Installationsbereit** , und klicken Sie anschließend auf **Installieren**.

## <a name="default-installation-folders"></a>Standard-Installationsordner

Bei der Installation von R-Server mit SQL Server-Setup werden R-Bibliotheken in einem Ordner zugeordnet, die Sie für das Setup verwendet SQL Server-Version installiert. In diesem Ordner finden Sie auch Beispieldaten, die Dokumentation für die R-Basispakete und die Dokumentation von R-Tools und der Laufzeit.

Allerdings werden bei Installation von Microsoft R Server über separate Windows Installer (nicht SQL-Setup), oder führen Sie ein upgrade des separaten Windows Installers, R-Bibliotheken in einem anderen Ordner installiert.

Zwar werden dagegen empfohlen, wenn Sie eine Instanz von SQL Server R Services (Datenbankintern) auch auf dem gleichen Computer installiert, wird eine zweite Kopie des R-Bibliotheken und Tools in einem anderen Ordner installiert.

Die folgende Tabelle enthält die Pfade für jede Installation.

|Version| Installationsmethode | Standardordner|
|----|----|----|
|R-Server (eigenständig) |SQL Server 2016-Setup-Assistenten|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R-Server (eigenständig) |Eigenständiges Windows-Installationsprogramm|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning-Server (eigenständig) |  2017 von SQL Server-Setup-Assistenten, mit der Option für R-Sprache |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning-Server (eigenständig) |  2017 von SQL Server-Setup-Assistenten mit Python Standardsprache (Option) |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning-Server (eigenständig) |  Eigenständiges Windows-Installationsprogramm |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (In-Database) |SQL Server 2016-Setup-Assistenten|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning-Dienste (datenbankintern) |2017 von SQL Server-Setup-Assistenten, mit der Option für R-Sprache|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning-Dienste (datenbankintern) |2017 von SQL Server-Setup-Assistenten mit Python Standardsprache (Option)| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

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

+ [Lernprogramm: Ausführen von R in T-SQL-](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).
+ [Lernprogramm: In-Database-Analyse für R-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).

