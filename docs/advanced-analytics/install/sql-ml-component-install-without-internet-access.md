---
title: Installieren Sie SQL Server-Machine Learning-Komponenten ohne Internetzugang | Microsoft Docs
ms.custom: 
ms.date: 03/05/2018
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
ms.openlocfilehash: 3f542786420eec8377dfe52ba3a1b73a24fbf524
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-machine-learning-components-without-internet-access"></a>Installieren von SQL Server-Machine learning-Komponenten ohne Internetzugang
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Standardmäßig Installationsprogramme mit Downloadwebsites abzurufenden erforderliche Microsoft verbinden und aktualisierte Komponenten für machine Learning auf SQL Server. Wenn firewalleinschränkungen verhindern, dass der Installationsprogramm diesen Standorten erreichen, können Sie ein Gerät mit Internetzugang Herunterladen von Dateien, Dateien mit einem offline-Server übertragen und führen Sie Setup.

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

> [!NOTE]  
> Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> Installieren einer Patchanforderung 

Microsoft hat ein Problem bei der speziellen Version von Microsoft VC++ 2013 Runtime-Binärdateien erkannt, die von SQL Server als vorausgesetzte Komponenten installiert werden. Wenn dieses Update an den VC++ Runtime-Binärdateien nicht installiert wird, können bei SQL Server in bestimmten Szenarios Stabilitätsprobleme auftreten. Bevor Sie SQL Server installieren, sollten Sie entsprechend den Anweisungen unter [Versionsanmerkungen zu SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) vorgehen, um festzustellen, ob Ihr Computer einen Patch für die VC-Runtime-Binärdateien benötigt.  


## <a name="download-cab-files"></a>Herunterladen der CAB-Dateien

Herunterladen Sie auf einem Server mit Internetzugang die für eine offline-Installation erforderliche CAB-Dateien Das Setup-Programm verwendet die CAB-Dateien, um zusätzliche Funktionen zu installieren.

Release  |Downloadlink  |
---------|---------|
**SQL Server-2017 Erstveröffentlichung** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python Open     |keine Änderung; Vorheriges verwenden |
Microsoft Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server      |keine Änderung; Vorheriges verwenden|
Microsoft Python Open     |keine Änderung; Vorheriges verwenden|
Microsoft Python Server    |keine Änderung; Vorheriges verwenden|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python Open     |keine Änderung; Vorheriges verwenden|
Microsoft Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 2017 CU4** |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python Open     |keine Änderung; Vorheriges verwenden|
Microsoft Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|

### <a name="bkmk_2016Installers"></a>Downloads für SQLServer 2016

> [!IMPORTANT]
> 
> Wenn Sie SQL Server 2016 SP1 CU4 oder SP1 CU5 offline installieren zu können, laden Sie SRO_3.2.2.16000_1033.cab herunter. Wenn Sie SRO_3.2.2.13000_1033.cab aus FWLINK 831785 heruntergeladen, gemäß der einrichten (Dialogfeld), benennen Sie die Datei als SRO_3.2.2.16000_1033.cab vor der Installation des kumulativen Updates.

Release  |Downloadlink  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server     | keine Änderung; Vorheriges verwenden |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server     |keine Änderung; Vorheriges verwenden|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server     |keine Änderung; Vorheriges verwenden |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server     |keine Änderung; Vorheriges verwenden|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server     |keine Änderung; Vorheriges verwenden|
**SQL Server 2016 SP 1 CU4 und GDR**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |keine Änderung; Vorheriges verwenden|
Microsoft R Server    |keine Änderung; Vorheriges verwenden |

Wenn Sie den Quellcode für Microsoft R anzeigen möchten, ist zum Download zur Verfügung als Archiv tar-Format: [Installationsprogramme R-Server herunterladen](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Zusätzliche erforderliche Komponenten

Je nach Ihrer Umgebung müssen Sie möglicherweise lokale Kopien von Installationsprogrammen für die folgenden erforderlichen Komponenten machen.

Komponente  |Version
---------|---------
[Microsoft AS OLE DB-Anbieter für SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="transfer-files"></a>Übertragen von Dateien

Übertragen Sie die ZIP-SQL Server-Installationsmedien und die Dateien, die bereits auf den Computer heruntergeladen werden auf dem Sie Setup installieren.

Legen die CAB-Dateien in einem geeigneten Ordner z. B. **Downloads** oder temporären Ordner der Setup-Benutzer: C:\Users < Benutzername > \AppData\Local\Temp.

Put the en_sql_server_2017.iso file in a convenient folder. Doppelklicken Sie auf **setup.exe** um Installation zu beginnen.

### <a name="run-setup"></a>Ausführen von 'Setup'

Beim Ausführen von SQL Server-Setup auf einem Computer, die vom Internet getrennt Setup fügt eine **Offlineinstallation** Seite des Assistenten, damit Sie den Speicherort der CAB-Dateien angeben können, die Sie im vorherigen Schritt kopiert haben.

1. Starten Sie den SQL Server-Setup-Assistenten.

2. Wenn der Setup-Assistent die Lizenzierung Seite für open Source-R oder Python-Komponenten angezeigt wird, klicken Sie auf **Accept**. Annahme der Lizenzbedingungen können Sie mit dem nächsten Schritt fortfahren.

3. In der **Offlineinstallation** Seite **Installationspfad**, geben Sie den Ordner, enthält die CAB-Dateien, die Sie zuvor kopiert haben.

4. Weiterhin folgenden den aufforderungen, um die Installation abzuschließen.

Nachdem die Installation abgeschlossen ist, den Dienst neu starten und konfigurieren Sie den Server zum Ausführen von Skripts zu aktivieren, wie in beschrieben [installieren Sie SQL Server 2017 Machine Learning Services (Datenbankintern)](sql-machine-learning-services-windows-install.md) oder [Installieren von SQL Server 2016 R Services (Datenbankintern)](sql-r-services-windows-install.md).

## <a name="slipstream-upgrades-for-offline-servers"></a>Slipstream-Upgrades für offline-Server

Als Slipstream-Einrichtung wird die Möglichkeit bezeichnet, einen Patch oder ein Update auf eine fehlgeschlagene Installation einer Instanz anzuwenden, um vorhandene Probleme zu beheben. Diese Methode hat den Vorteil, dass SQL Server während der Einrichtung aktualisiert wird, sodass Sie später nur einmal einen Neustart durchführen müssen.

+ Wenn der Server keinen Internetzugriff hat, müssen Sie das SQL Server-Installationsprogramm herunterladen und anschließend die passenden Versionen der Installationsprogramme der R-Komponente, **bevor** Sie den Updateprozess beginnen.  R-Komponenten sind nicht standardmäßig mit SQL Server enthalten.

+ Wenn Sie diese Komponenten zu einer vorhandenen Installation hinzufügen, verwenden Sie die aktualisierte Version des SQL Server-Installationsprogramm und die entsprechenden aktualisierte Version der zusätzlichen Komponenten. Wenn Sie angeben, dass die R-Funktion installiert werden, sucht das Installationsprogramm für die passende Version der Installationsprogramme für Machine learning-Komponenten.

## <a name="get-help"></a>Abrufen von Hilfe

Benötigen Sie Hilfe bei der Installation oder Aktualisierung? Antworten auf häufig gestellte Fragen und bekannte Probleme finden Sie im folgenden Artikel:

* [Upgrade und Installation häufig gestellte Fragen – Machine Learning-Dienste](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Überprüfen Sie den Installationsstatus der Instanz, und beheben Probleme, wiederholen Sie dann diese benutzerdefinierten Berichte.

* [Benutzerdefinierte Berichte für SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

Dieser Artikel durch das Supportteam von R Services veranschaulicht, wie eine unbeaufsichtigte Installation oder Aktualisierung von R Services in SQL Server 2016 ausführen: [Bereitstellen von R Services auf Computern ohne Internetzugang](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).


## <a name="next-steps"></a>Nächste Schritte

R-Entwickler können mit einigen einfachen Beispielen beginnen und die Grundlagen der Funktionsweise von R mit SQL Server. Im nächsten Schritt finden Sie unter den folgenden Links:

+ [Lernprogramm: Ausführen von R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Lernprogramm: In-Database-Analyse für R-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python-Entwickler können zum Verwenden von Python mit SQL Server gemäß diesen Lernprogrammen erfahren:

+ [Lernprogramm: Ausführen von Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Lernprogramm: In-Database-Analyse für Python-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).

