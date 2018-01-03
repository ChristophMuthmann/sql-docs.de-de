---
title: Machine Learning-Komponenten ohne Internetzugang installieren | Microsoft Docs
ms.custom: 
ms.date: 11/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "30"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 93adacb061b3bf4c77606294ae8341144eaf24c9
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="installing-machine-learning-components-without-internet-access"></a>Machine Learning-Komponenten ohne Internetzugang installieren

Da die R und Python-Komponenten, die mit SQL Server 2016 und SQL Server-2017 bereitgestellten open-Source sind, wird Microsoft R oder Python-Komponenten nicht standardmäßig installiert. Stattdessen geben Sie die zugehörigen Installationsprogramme und Pakete auf dem Microsoft Download Center und andere vertrauenswürdige Sites zur Vereinfachung gebündelt. Muss stimmen Sie die entsprechende Lizenz, und klicken Sie dann SQL Server-Setup installiert R oder Python-Komponenten, für Sie.

In diesem Thema Downloadpfade die für die Installationsprogramme und einen Überblick über den offline-Setupvorgang.

## <a name="overview-of-the-offline-installation-process"></a>Übersicht über den Prozess offline-installation

Setup der Computerkomponenten in SQL Server 2016 und SQL Server-2017 verwendet ist in der Regel eine Internetverbindung erforderlich. Wenn SQL Server-Setup ausgeführt wird, wenn Sie eine der Machine learning Optionen ausgewählt haben, überprüft Setup den Python oder R Installationsprogramme, als auch alle anderen erforderlichen Komponenten.

+ **Wenn der Computer eine Internetverbindung verfügt.**

    SQL Server sucht und die Komponenten für die Sie heruntergeladen und installiert sie während des Setups. Akzeptieren Sie die Lizenzbedingungen separat für jede open-Source-Komponente (R oder Python), die Sie installieren.

+ **Wenn der Computer keinen Zugriff auf das internet**

    Sie müssen zusätzliche Installationsprogramme herunterladen, bevor Sie Setup fortsetzen. Laden Sie mindestens die R oder Python Installationsprogramme, die für die Version von SQL Server unterstützt werden, die installiert werden.

    Je nach Konfiguration des Servers benötigen Sie möglicherweise zusätzliche Komponenten.  Finden Sie unter [zusätzliche Komponenten](#bkmk_OtherComponents) Details.

    Nachdem Sie die Installationsprogramme heruntergeladen haben, verwenden Sie diese, wenn die Funktion als Teil der SQL Server-Setup installieren.

### <a name="step-1-obtain-additional-installers"></a>Schritt 1: Beziehen Sie zusätzliche Installationsprogramme

**Für R**

Die Sprache "R" wird in SQL Server 2016 und SQL Server-2017 unterstützt. Zwei verschiedene Installationsprogramme sind erforderlich, für die open-Source und proprietäre Komponenten. Der SQL Server-Setup-Assistent wird sichergestellt, dass sie in der richtigen Reihenfolge installiert werden.

+ Installationsprogramme mit **SRO** Geben Sie den Namen der open-Source-Komponenten.
+ Installationsprogramme mit **SRS** im Namen enthalten Komponenten von Microsoft, einschließlich derjenigen für Datenbankintegration bereitgestellt.

**Für Python**

Die Sprache Python wird nur in SQL Server-2017 unterstützt. Es stehen zwei separate Installationsprogramme, die Sie herunterladen müssen.

+ Installationsprogramme mit **SPO** in den Namen für Microsoft Python öffnen, und geben Sie die open-Source-Komponenten.
+ Installationsprogramme mit **SPS** im Namen sind für Microsoft-Python-Server und Komponenten von Microsoft, einschließlich derjenigen für Datenbankintegration bereitgestellten enthalten.

**Zum Herunterladen**

1. Laden Sie die Installationsprogramme in der [Microsoft Download Center-Websites](#installerlocs) auf einem Computer mit Internetzugriff, und speichern Sie das Installationsprogramm, anstatt ihn ausführen.
2. Kopieren Sie die Dateien des komponenteninstallationsprogramms (CAB-Datei) auf dem Computer, auf dem Sie Machine Learning-Komponenten installieren möchten.
3. Englisch von der Setup-Assistenten in SQL Server 2016 standardmäßig installiert. Installation unter Verwendung einer anderen Sprache die erforderliche Änderung des Dateinamens Installer aus, wie hier beschrieben: [Änderungen erforderlich sind, für verschiedene Gebietsschemas](#modslocales).
    Für SQL Server 2017 basierend auf dem Gebietsschema der Instanz die gewünschten Sprache identifiziert.
4. Laden Sie alle zusätzlichen Komponenten, die erforderlich sind, z. B. MPI oder .NET Core werden.
5. Optional können Sie die archivierten Quellcode für die open-Source-Komponenten herunterladen, aber dies ist für SQL Server-Setup nicht erforderlich und kann jederzeit ausgeführt werden. Weitere Informationen finden Sie unter [R Server für Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows).

Eine schrittweise Anleitung des offline-Installationsprozesses für R Services in SQL Server 2016, empfehlen wir Ihnen, Artikel durch die [SQL Server-Kundenberatungsteams](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/). der Artikel enthält Screenshots und deckt auch Patchen und Slipstream-Setup-Szenarien.

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>Schritt 2: Ausführen von offline-Setup unter Verwendung des SQL Server-Setup-Assistenten

1. Führen Sie den Setup-Assistenten von SQL Server aus.
2. Wenn der Setup-Assistent die Lizenzierung Seite angezeigt wird, klicken Sie auf **Accept**.
3. Ein Dialogfeld wird geöffnet, die Sie für eingabeaufforderungen der **Installationspfad** der erforderlichen Pakete.
4. Klicken Sie auf **Durchsuchen** , suchen Sie den Ordner mit den Installer-Dateien, die Sie zuvor kopiert haben.
5. Wenn die richtigen Dateien gefunden wurden, können Sie auf **Weiter** klicken, um anzugeben, dass die Komponenten verfügbar sind.
10. Schließen Sie den Setup-Assistenten von SQL Server ab.
11. Führen Sie die erforderlichen Schritte nach der Installation, um sicherzustellen, dass der Dienst aktiviert ist.

## <a name="installerlocs"></a>Zum download von Machine Learning-Komponenten

> [!NOTE]
> Achten Sie darauf, dass Sie die Dateien abrufen, die die Version von SQL Server entsprechen, die Sie installieren.
> 
> Unterstützung für Python ist seit SQL Server 2017 CTP 2.0 bereitgestellt. Python wird in frühere Versionen, einschließlich SQL Server 2016 nicht unterstützt.

+ [Beim Abrufen der R-Komponenten für SQL Server 2016](#bkmk_2016Installers)

+ [Beim Abrufen von R oder Python-Komponenten für SQL Server-2017](#bkmk_2017Installers)

### <a name="bkmk_2017Installers"></a>Downloads für SQLServer 2017

Release  |Downloadlink  |
---------|---------|
**2017 CTP 1 für SQL Server**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**1.1 2017 CTP für SQL Server** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**1.4 2017 CTP für SQL Server** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Öffnen Sie Microsoft-Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft-Python-Server    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**SQL Server 2017 RC1** |
Microsoft R Open     |[SRO_3.3.3.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851503)|
Microsoft R Server     |[SRS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851498)|
Öffnen Sie Microsoft-Python     |[SPO_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851499)|
Microsoft-Python-Server    |[SPS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851504)|
**SQL Server 2017 RC 2** |
Microsoft R Open     |[SRO_3.3.3.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851493)|
Microsoft R Server     |[SRS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851505)|
Öffnen Sie Microsoft-Python     |[SPO_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851506)|
Microsoft-Python-Server    |[SPS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851497)|
**RTM-Version von SQL Server 2017** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Öffnen Sie Microsoft-Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft-Python-Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |Vorheriges verwenden|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Öffnen Sie Microsoft-Python     |Vorheriges verwenden |
Microsoft-Python-Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |Vorheriges verwenden|
Microsoft R Server      |Vorheriges verwenden|
Öffnen Sie Microsoft-Python     |Vorheriges verwenden |
Microsoft-Python-Server    |Vorheriges verwenden|

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
**SQL Server 2016 SP1 CU2**     |
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

Wenn Sie den Quellcode für Microsoft R anzeigen möchten, ist zum Download zur Verfügung als Archiv tar-Format: [Installationsprogramme R-Server herunterladen](https://docs.microsoft.com/r-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Zusätzliche erforderliche Komponenten

Je nach Ihrer Umgebung müssen Sie möglicherweise lokale Kopien von Installationsprogrammen für die folgenden erforderlichen Komponenten machen.

Komponente  |Versionsoptionen
---------|---------
[Microsoft AS OLE DB-Anbieter für SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="modslocales"></a>Installieren für verschiedene Gebietsschemas

Wenn Sie beim Herunterladen der. CAB-Dateien als Teil des SQL Server-Setup auf einem Computer mit Internetzugriff des Setup-Assistenten die lokale Sprache erkennt und automatisch geändert wird, die Sprache des Installationsprogramms.

Allerdings können abhängig von Ihrer Version von SQL Server, Sie müssen zusätzliche Schritte ausführen, um die lokalisierte R-Komponenten auf einem Computer ohne Internetzugriff zu installieren.

+ **Für SQLServer 2016**

   Nachdem Sie die R-Installationsprogramme für eine lokale Freigabe herunterladen, müssen Sie möglicherweise manuell bearbeiten Sie den Namen der heruntergeladenen Dateien die richtigen Sprachen-ID für die Sprache eingefügt, das Sie installieren.

    Angenommen, um die japanische Version von SQL Server zu installieren, ändern Sie den Namen der Datei aus SRS_8.0.3.0_**1033**CAB zum SRS_8.0.3.0_**1041**CAB.

    > [!IMPORTANT]
    > Dieses Problem gilt nur für frühere Versionen und in späteren Versionen behoben wurde.
    > **Verwenden Sie nur diese problemumgehung auf, wenn das Installationsprogramm eine Meldung zurückgegeben, die richtige Sprache kann nicht installiert werden.**

+ **Für SQLServer 2017**

    Herunterladen der. CAB-Datei für die R oder Python-Komponenten.
    
    Die Sprache wird je nach Gebietsschema Server erkannt. Das richtige Gebietsschema wird automatisch mithilfe der heruntergeladenen installiert. CAB-Datei.

## <a name="slipstream-upgrades"></a>Slipstream-upgrades

Als Slipstream-Einrichtung wird die Möglichkeit bezeichnet, einen Patch oder ein Update auf eine fehlgeschlagene Installation einer Instanz anzuwenden, um vorhandene Probleme zu beheben. Diese Methode hat den Vorteil, dass SQL Server während der Einrichtung aktualisiert wird, sodass Sie später nur einmal einen Neustart durchführen müssen.

+ Wenn der Server keinen Internetzugriff hat, müssen Sie das SQL Server-Installationsprogramm herunterladen und anschließend die passenden Versionen der Installationsprogramme der R-Komponente, **bevor** Sie den Updateprozess beginnen.  R-Komponenten sind nicht standardmäßig mit SQL Server enthalten.

+ Domänenmodus *hinzufügen* diese Komponenten einer *vorhandenen* Installation, die aktualisierte Version der SQL Server-Installationsprogramm verwenden, und die entsprechende Version der zusätzlichen Komponenten aktualisiert. Wenn Sie angeben, dass die R-Funktion installiert werden, sucht das Installationsprogramm für die passende Version der Installationsprogramme für Machine learning-Komponenten.

## <a name="command-line-arguments-for-specifying-component-locations"></a>Befehlszeilenargumente für das Angeben von Positionen

Wenn Sie eine offline-Installation über die Befehlszeile durchführen zu können, müssen Sie angeben, die folgenden Befehlszeilenargumente zum Angeben des Speicherorts der Komponenten, die Sie zuvor heruntergeladen haben. Allerdings müssen Sie keine zusätzliche Attribute zum Installieren zusätzlicher erforderlicher Komponenten festgelegt; Erforderliche Komponenten, z. B. .NET Core werden standardmäßig im Hintergrund installiert.

**Speicherort der Installationsprogramme**

- `/UPDATESOURCE`um den Speicherort der lokalen Datei mit diesem SQL Server-Update-Installationsprogramm anzugeben
- `/MRCACHEDIRECTORY`um den Ordner mit den R-Komponente CAB-Dateien anzugeben
- `/MPYCACHEDIRECTORY`um den Ordner mit den Python-Komponente CAB-Dateien anzugeben

**R-Komponenten in SQL Server 2016**

- `/ADVANCEDANALYTICS`beim Abrufen der Datenbankmodul-Unterstützung für externe Skripts
- `/IACCEPTROPENLICENSETERMS="True"`die separaten R Lizenzvertrag akzeptieren

**R-Komponenten in SQL Server-2017**

- `/ADVANCEDANALYTICS`beim Abrufen der Datenbankmodul-Unterstützung für externe Skripts
- `/SQL_INST_MR`Verwenden von R
- `/IACCEPTROPENLICENSETERMS="True"`die separaten R Lizenzvertrag akzeptieren

**Python-Komponenten in SQL Server-2017**

- `/ADVANCEDANALYTICS`beim Abrufen der Datenbankmodul-Unterstützung für externe Skripts
- `/SQL_INST_MPY`Verwenden von Python
- `/IACCEPTPYTHONLICENSETERMS="True"`die separaten Python-Lizenzvertrag akzeptieren


> [!NOTE]
> Sie können nicht das Dienstkonto für Launchpad durch Verwenden von Parametern in SQL Server-Setup ändern. Es wird empfohlen, dass Sie installieren, verwenden die Standardkonten für den Dienst, und ändern Sie das Dienstkonto mithilfe von SQL Server-Konfigurations-Manager. Werden Sie nach der Anmeldung sicher, dass das Launchpad-Dienst neu zu starten.

## <a name="see-also"></a>Siehe auch

[Installieren von Microsoft R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows)

Dieser Artikel durch das Supportteam von R Services veranschaulicht, wie eine unbeaufsichtigte Installation oder Aktualisierung von R Services in SQL Server 2016 ausführen: [Bereitstellen von R Services auf Computern ohne Internetzugang](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).
