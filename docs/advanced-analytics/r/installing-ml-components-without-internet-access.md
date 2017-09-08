---
title: Machine Learning-Komponenten ohne Internetzugang installieren | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7307104b9ad5df2bb8f034525cc82847d21a14bf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>Machine Learning-Komponenten ohne Internetzugang installieren

Da die R und Python-Komponenten, die mit SQL Server 2016 oder SQL Server-2017 bereitgestellte open-Source sind, wird Microsoft R oder Python-Komponenten nicht standardmäßig installiert.

Stattdessen geben Sie die zugehörigen Installationsprogramme und Pakete auf dem Microsoft Download Center und andere vertrauenswürdige Sites zur Vereinfachung gebündelt. Sie müssen zustimmen, um die erforderliche Lizenz, und klicken Sie dann SQL Server-Setup installiert R oder Python-Komponenten für Sie.

In diesem Thema Downloadpfade die für die Installationsprogramme und einen Überblick über den offline-Setupvorgang.

## <a name="installation-process"></a>Installationsvorgang

Setup der Computerkomponenten in SQL Server 2016 und SQL Server-2017 verwendet ist in der Regel eine Internetverbindung erforderlich. Wenn SQL Server-Setup ausgeführt wird, wenn Sie den Computer Learnig Optionen ausgewählt haben, überprüft Setup für die Python oder R Installationsprogramme, als auch alle anderen erforderlichen Komponenten. Ist eine Internetverbindung besteht, wird er von SQL Server für Sie installiert.

> [!IMPORTANT]
> Auf einem Server ohne Internetzugang müssen Sie zusätzliche Installationsprogramme herunterladen, bevor Sie Setup fortsetzen.

Sie benötigen mindestens R oder Python Installationsprogramme herunterladen, die für die Version unterstützt oder Buildnummer von SQL Server, die installiert werden.

Je nach Konfiguration des Servers benötigen Sie möglicherweise zusätzliche Komponenten wie .NET Core.  Finden Sie unter [zusätzliche Komponenten](#bkmk_OtherComponents) Details.

Nachdem Sie die Installationsprogramme heruntergeladen haben, verwenden Sie diese, wenn die Funktion als Teil der SQL Server-Setup installieren.

### <a name="step-1-obtain-additional-installers"></a>Schritt 1: Beziehen Sie zusätzliche Installationsprogramme

Für **R** in SQL Server 2016 und SQL Server-2017, müssen Sie zwei unterschiedliche Installationsprogramme abgerufen. Der Setup-Assistent für SQL Server stellt sicher, dass sie in der richtigen Reihenfolge installiert werden.

+ Installationsprogramme mit **SRO** Geben Sie den Namen der open-Source-Komponenten.
+ Insallers mit **SRS** im Namen enthalten Komponenten von Microsoft, einschließlich derjenigen für Datenbankintegration bereitgestellt.


Für **Python** in SQL Server 2017 herunterladen, die einzelnen CAB-Datei und alle erforderlichen Komponenten.


1. Laden Sie das Installationsprogramm von den [Microsoft Download Center-Websites](#installerlocs) auf einen Computer mit Internetzugriff herunter, und speichern Sie das Installationsprogramm anstatt es auszuführen.
2. Kopieren Sie die Dateien des komponenteninstallationsprogramms (CAB-Datei) auf dem Computer, auf dem Sie Machine Learning-Komponenten installieren.
3. Aktuell wird der Setup-Assistent Englisch standardmäßig installiert. Um eine andere Sprache installieren, ändern Sie die Installer-Dateinamen wie hier beschrieben: [Änderungen, die für verschiedene Gebietsschemas erforderlichen](#modslocales).
4. Laden Sie alle zusätzlichen Komponenten, die erforderlich sind, z. B. MPI oder .NET Core werden.
5. Optional können Sie die archivierten Quellcode für die open-Source-Komponenten herunterladen, aber dies ist für SQL Server-Setup nicht erforderlich und kann jederzeit ausgeführt werden. Weitere Informationen finden Sie unter [R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).


> [!NOTE]
> Achten Sie darauf, die Dateien abzurufen, die mit der SQL Server-Version übereinstimmen, die Sie installieren werden.
> 
> Python wird in SQL Server 2017 CTP 2.0 unterstützt. Python wird in frühere Versionen, einschließlich SQL Server 2016 nicht unterstützt.

Eine schrittweise Anleitung des offline-Installationsprozesses für R Services in SQL Server 2016, empfehlen wir Ihnen, Artikel durch die [SQL Server-Kundenberatungsteams](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/). Dazu gehören auch das Patching- und Slipstream-Einrichtungsszenarios.


### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>Schritt 2: Ausführen von offline-Setup unter Verwendung des SQL Server-Setup-Assistenten

1. Führen Sie den Setup-Assistenten von SQL Server aus.
2. Wenn der Setup-Assistent die Lizenzierung Seite angezeigt wird, klicken Sie auf **Accept**.
3. Ein Dialogfeld wird geöffnet, die Sie für eingabeaufforderungen der **Installationspfad** der erforderlichen Pakete.
4. Klicken Sie auf **Durchsuchen** , suchen Sie den Ordner mit den Installer-Dateien, die Sie zuvor kopiert haben.
5. Wenn die richtigen Dateien gefunden wurden, können Sie auf **Weiter** klicken, um anzugeben, dass die Komponenten verfügbar sind.
10. Schließen Sie den Setup-Assistenten von SQL Server ab.
11. Führen Sie die erforderlichen Schritte nach der Installation, um sicherzustellen, dass der Dienst aktiviert ist.

## <a name="installerlocs"></a>Downloads

Release  |Downloadlink  
---------|---------
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
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 GDR**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**2017 CTP 1 für SQL Server**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**1.1 2017 CTP für SQL Server** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**1.4 2017 CTP für SQL Server** |
Microsoft R Open     |[SRO_xxxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_xxx.xxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Öffnen Sie Microsoft-Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft-Python-Server    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)

Wenn Sie den Quellcode für Microsoft R anzeigen möchten, ist zum Download zur Verfügung als Archiv tar-Format: [Installationsprogramme R-Server herunterladen](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Zusätzliche erforderliche Komponenten

Je nach Ihrer Umgebung müssen Sie möglicherweise lokale Kopien von Installationsprogrammen für die folgenden erforderlichen Komponenten machen.

Komponente  |Version
---------|---------
[Microsoft AS OLE DB-Anbieter für SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0


## <a name="modslocales"></a>Installieren für verschiedene Gebietsschemas

Wenn Sie die CAB-Dateien als Teil des SQL Server-Setups auf einen Computer mit Internetzugang herunterladen, erkennt der Setup-Assistent die lokale Sprache und ändert automatisch die Sprache des Installationsprogramms.

Wenn Sie jedoch eine der lokalisierten Versionen von SQL Server auf einem Computer ohne Internetzugang installieren und die R-Installationsprogramme auf eine lokale Freigabe herunterladen, müssen Sie manuell den Namen der heruntergeladenen Dateien bearbeiten und die korrekte Sprach-ID für die von Ihnen installierte Sprache einfügen.

Wenn Sie beispielsweise die japanische Version von SQL Server installieren, würden Sie den Namen der Datei von SRS_8.0.3.0_**1033**.cab in SRS_8.0.3.0_**1041**.cab ändern.


## <a name="slipstream-upgrades"></a>Slipstream-Upgrades

Als Slipstream-Einrichtung wird die Möglichkeit bezeichnet, einen Patch oder ein Update auf eine fehlgeschlagene Installation einer Instanz anzuwenden, um vorhandene Probleme zu beheben. Diese Methode hat den Vorteil, dass SQL Server während der Einrichtung aktualisiert wird, sodass Sie später nur einmal einen Neustart durchführen müssen.

+ Wenn der Server keinen Internetzugriff hat, müssen Sie das SQL Server-Installationsprogramm herunterladen und anschließend die passenden Versionen der Installationsprogramme der R-Komponente, **bevor** Sie den Updateprozess beginnen.  R-Komponenten sind nicht standardmäßig mit SQL Server enthalten.

+ Domänenmodus *hinzufügen* diese Komponenten einer *vorhandenen* Installation, die aktualisierte Version der SQL Server-Installationsprogramm verwenden, und die entsprechende Version der zusätzlichen Komponenten aktualisiert. Wenn Sie angeben, dass die R-Funktion installiert werden, sieht das Installationsprogramm für die passende Version der Installationsprogramme für Machine learning-Komponenten.

## <a name="command-line-arguments-for-setup"></a>Befehlszeilenargumente für Setup

Wenn Sie eine unbeaufsichtigte Installation ausführen zu können, müssen Sie bieten die folgenden Befehlszeilenargumente. Beachten Sie, dass Sie nicht benötigen, legen Sie zusätzlichen Flags So installieren Sie zusätzliche erforderliche Komponenten. Erforderliche Komponenten, z. B. .NET Core werden standardmäßig im Hintergrund installiert.

**Speicherort der Installationsprogramme**

- `/UPDATESOURCE`um den Speicherort der lokalen Datei mit diesem SQL Server-Update-Installationsprogramm anzugeben
- `/MRCACHEDIRECTORY`um den Ordner mit den R-Komponente CAB-Dateien anzugeben

**R-Komponenten in SQL Server 2016**

- `/ADVANCEDANALYTICS`beim Abrufen der Datenbankmodul-Unterstützung für externe Skripts
- `/IACCEPTROPENLICENSETERMS="True"`die separaten R Lizenzvertrag akzeptieren

**R-Komponenten in SQL Server SQL Server 2017**

- `/ADVANCEDANALYTICS`beim Abrufen der Datenbankmodul-Unterstützung für externe Skripts
- `/SQL_INST_MR`Verwenden von R
- `/IACCEPTROPENLICENSETERMS="True"`die separaten R Lizenzvertrag akzeptieren

**Python-Komponenten in SQL Server-2017**

- `/ADVANCEDANALYTICS`beim Abrufen der Datenbankmodul-Unterstützung für externe Skripts
- `/SQL_INST_MPY`Verwenden von Python
- `/IACCEPTPYTHONLICENSETERMS="True"`die separaten R Lizenzvertrag akzeptieren

> [!TIP]
> Dieser Artikel durch das Supportteam von R Services veranschaulicht, wie eine unbeaufsichtigte Installation oder Aktualisierung von R Services in SQL Server 2016 ausführen: [Bereitstellen von R Services auf Computern ohne Internetzugang](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

## <a name="see-also"></a>Siehe auch

[Installieren von Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)


