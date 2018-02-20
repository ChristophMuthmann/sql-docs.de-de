---
title: "Installieren von Machine Learning einen eigenständigen Server oder einen eigenständigen R Server | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2ecb60bd02b3fc1ee7ac7101749fa7affc2523bd
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone"></a>Installieren von Machine Learning-Server (eigenständig) oder R Server (eigenständig)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server-Setup umfasst die Option zum Installieren eines Machine learning-Server, der außerhalb von SQL Server ausgeführt wird. Diese Option ist möglicherweise hilfreich, wenn Sie hohe Leistung Machine Learning-Lösungen entwickeln, remote rechenkontexte zu verwenden, oder, können für mehrere Plattformen, einschließlich bereitgestellt werden, müssen:
  
  + Eine Instanz von SQL Server 2016 oder SQL Server-2017, Machine Learning aktiviert ist
  + Eine Instanz des R-Server "oder" Machine Learning-Server in einem Hadoop oder Spark-cluster
  + R-Server "oder" Machine Learning-Server unter Linux

Dieser Artikel beschreibt, wie SQL Server-Setup verwenden, um die eigenständige Version des Machine Learning-Server oder Microsoft R Server zu installieren. Wenn Sie eine Enterprise Edition oder Software Assurance verfügen, ist die Installation des eigenständigen Machine Learning-Servers kostenlos.

+ [Installieren von R Server](#bkmk_installRServer) -verwendet SQL Server 2016-Setup
+ [Installieren von Machine Learning Server](#bkmk_installMLServer) -verwendet 2017 von SQL Server-Setup
+ [Aktualisieren einer vorhandenen Instanz von Microsoft R Server](#bkmk_upgrade)
+ [Entscheidungshilfe für Elemente, die installiert](#bkmk_tips)

##  <a name="bkmk_installMLServer"></a> Installieren von Machine Learning-Server (eigenständig)

Diese Funktion erfordert eine Enterprise-Lizenz oder eine entsprechende für **SQL Server-2017**.

Wenn Sie eine frühere Version von Microsoft R Server installiert haben, wird empfohlen, dass Sie diese zunächst deinstallieren.

Wenn der Computer nicht über Internetzugriff verfügt, sollten Sie die Installationsprogramme für die Komponente im Voraus herunterladen. Weitere Informationen finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](./installing-ml-components-without-internet-access.md).

1. 2017 von SQL Server-Setup ausführen.

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

Weitere Informationen zur automatisierten oder offline-Installation finden Sie unter [Installieren von Microsoft R Server über die Befehlszeile](../../advanced-analytics/r/install-microsoft-r-server-from-the-command-line.md).

##  <a name="bkmk_installRServer"></a> Installieren von Microsoft R-Server (eigenständig)

Diese Funktion erfordert eine Enterprise-Lizenz oder eine entsprechende für **SQL Server 2016**.

Wenn Sie alle früheren Versionen von Revolution Analytics-Tools bzw. die Pakete installiert haben, müssen Sie diese zunächst deinstallieren. Finden Sie unter [ein Upgrade von einer älteren Version von Microsoft R Server](#bkmk_Uninstall).

1. Führen Sie SQL Server 2016-Setup. Es wird empfohlen, dass Sie Servicepack 1 oder höher installieren.

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
    > Im Allgemeinen wird empfohlen, Machine Learning-Server (eigenständig) auf demselben Computer wie SQL Server-Machine Learning-Services zu installieren.

4.  Akzeptieren Sie die Lizenzbedingungen für das Herunterladen und Installieren von Microsoft R Open. Wenn die Schaltfläche **Annehmen** deaktiviert wird, können Sie auf **Weiter**klicken.
    
    Die Installation dieser Komponenten und alle erforderlichen Komponenten, die sie benötigen, die kann eine Weile dauern.
    
5.  Überprüfen Sie Ihre Auswahl auf der Seite **Installationsbereit** , und klicken Sie anschließend auf **Installieren**.

## <a name="bkmk_upgrade"></a> Aktualisieren einer vorhandenen Instanz von R-Server

Wenn Sie eine frühere Version von Microsoft R Server (eigenständig) installiert haben, können Sie die Instanz, um neuere Versionen der R-Komponenten verwenden, aktualisieren. Das Upgrade ändert sich auch der Support-Richtlinie, um mithilfe der Gruppenrichtlinie moderne Software Lebenszyklus unterstützen. Dadurch wird die Instanz auf einem anderen Zeitplan häufiger aktualisiert werden, als die SQL Server-Versionen.

1. Herunterladen Sie separate Windows-basierten Installationsprogramm von der hier aufgeführten Positionen: 

    + [Installieren Sie Machine Learning-Server für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Installieren von R Server 9.1 für Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

2. Führen Sie das Installationsprogramm, und befolgen Sie die Anweisungen. Wählen Sie auf der Seite, in dem Sie die zu installierenden Funktionen auswählen, jede Instanz des R-Server, die Sie aktualisieren möchten.

## <a name ="bkmk_tips"></a> Tipps zur Installation und eine nachverfolgung erforderlich

Dieser Abschnitt enthält zusätzliche Informationen, die im Zusammenhang mit Setup.

### <a name="which-version-should-i-install"></a>Die Version sollte ich installiere?

+ **Microsoft R Server** wurde zuerst als Teil von SQL Server 2016 angeboten wird, und die Sprache "R" unterstützt. Die letzte Version von Microsoft R Server wurde 9.0.1.

+ **Microsoft Machine Learning-Server** ist die neueste Version, die mit SQL Server-2017 veröffentlicht wurde, und bietet viele Updates, einschließlich der Unterstützung für Python. Kumulative Update 1 für SQL Server-2017 wurde freigegeben, inklusive der Version 9.2.1.24 von Machine Learning-Server. Dieses Update wird empfohlen, wenn die aktuelle Python-APIs verwendet werden soll.

+ **Ein direktes Upgrade**: Setup erfordert, dass eine SQL Server-Lizenz und Upgrades in der Regel mit der SQL Server--versionsrhythmus ausgerichtet sind. Dadurch wird sichergestellt, dass Ihre Entwicklungstools synchron mit der Version sind, die im SQL Server-Rechenkontext ausgeführt wird. Separate Windows-basierten Installationsprogramm können Sie jedoch häufiger Updates der Supportrichtlinie für moderne Softwarelebenszyklus erhalten. Sie können dieses Installationsprogramm auch zum Aktualisieren einer Instanz von SQL Server 2016 oder SQL Server-2017 verwenden.

### <a name="default-installation-folders"></a>Standard-Installationsordner

Bei der Installation von R-Server oder Machine Learning-Servers mit SQL Server-Setup werden R-Bibliotheken installiert, in einem Ordner, der SQL Server-Version, die Sie für das Setup verwendet zugeordnet. In diesem Ordner finden Sie auch Beispieldaten, die Dokumentation für die R-Basispakete und die Dokumentation von R-Tools und der Laufzeit.

Allerdings werden bei der Installation mit dem separate Windows Installer oder führen Sie ein upgrade des separaten Windows Installers, R-Bibliotheken in einem anderen Ordner installiert.

Nur zu Referenzzwecken werden, wenn Sie eine Instanz von SQL Server R Services (Datenbankintern) "oder" Machine Learning-Services (Datenbankintern) installiert haben und diese Instanz befindet sich auf demselben Computer ausführen, die R-Bibliotheken und Tools standardmäßig in einem anderen Ordner installiert.

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
### <a name="development-tools"></a>Entwicklungstools

Eine Entwicklungsaufgabe IDE ist nicht als Teil von Setup installiert. Zusätzliche Tools sind nicht erforderlich, da alle Standardtools eingeschlossen werden würde, die mit einer Verteilung von R oder Python angegeben werden.

Es wird empfohlen, dass Sie, die neue Version von versuchen [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]. Visual Studio unterstützt sowohl R und Python sowie Tools zur Datenbankentwicklung, Konnektivität mit SQL Server und BI-Tools. Sie können jedoch bevorzugte Entwicklungsumgebung einschließlich RStudio.

## <a name="troubleshooting"></a>Problembehandlung

Dieser Abschnitt enthält einige häufig auftretende Probleme bei der Installation von Machine Learning-Server oder R-Server sind.

### <a name="incompatible-version-of-r-client-and-r-server"></a>Inkompatible Version von R Client und R Server

Wenn Sie Microsoft-R-Client installieren und sie zum Ausführen von R in einen remote SQL Server-computekontext verwenden, erhalten Sie möglicherweise einen Fehler wie folgt:

*Sie sind Version 9.0.0 von Microsoft R-Client auf Ihrem Computer ausführen, die mit dem Microsoft R Server 8.0.3-Version nicht kompatibel ist. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

In SQL Server 2016 war es erforderlich, dass die Version von R, die in SQL Server R Services ausgeführt wurde wie die Microsoft-R-Client-Bibliotheken identisch sein. Diese Anforderung wurde in höheren Versionen entfernt. Wir empfehlen jedoch, dass Sie immer die neuesten Versionen des Machine learning-Komponenten erhalten, und installieren Sie alle Servicepacks. 

Wenn Sie eine frühere Version von Microsoft R Server aufweisen und Kompatibilität mit Microsoft R Client 9.0.0 sicherstellen müssen, installieren Sie die Updates, die beschrieben werden, in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262).

### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Installieren von Microsoft R Server in einer Instanz von SQL Server auf Windows Core

In der RTM-Version von SQL Server 2016 lag ein bekanntes Problem beim Hinzufügen von Microsoft R Server für eine Instanz auf Windows Server Core-Edition. Dies wurde behoben.

Wenn dieses Problem auftritt, können, wenden Sie das Update, die in beschriebenen [KB3164398](https://support.microsoft.com/kb/3164398) Feature "R" mit der vorhandenen Instanz unter Windows Server Core hinzu.   Weitere Informationen finden Sie unter [Microsoft R Server (eigenständig) kann nicht auf einem Windows Server Core-System installiert werden](https://support.microsoft.com/kb/3168691).

###  <a name="bkmk_Uninstall"></a> Upgrade von einer älteren Version von Microsoft R Server

Wenn Sie eine Vorabversion von Microsoft R Server installiert haben, müssen Sie diese deinstallieren, bevor Sie auf eine neuere Version aktualisieren können.

**Deinstallieren von Microsoft R Server (eigenständig)**

1.  Klicken Sie in der **Systemsteuerung**auf **Programme hinzufügen/entfernen**, und wählen Sie `Microsoft SQL Server 2016 <version number>`aus.

2.  Wählen Sie im Dialogfeld mit den Optionen zum **Hinzufügen**, **Reparieren**oder **Entfernen** von Komponenten die Option **Entfernen**aus.
  
3.  Wählen Sie auf der Seite **Funktionen auswählen** unter **Freigegebene Funktionen**die Option **R Server (eigenständig)**aus. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen** , um nur die ausgewählten Komponenten zu deinstallieren.

### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>Installation schlägt fehl mit dem Fehler „Es kann jeweils nur ein Revolution Enterprise-Produkt installiert werden.“

Dieser Fehler kann auftreten, wenn Sie eine ältere Installation von Revolution Analytics-Produkten oder eine Vorabversion von SQL Server R Services verwenden. Sie müssen alle früheren Versionen deinstallieren, bevor Sie eine neuere Version von Microsoft R Server installieren können. Eine parallele Installation mit anderen Versionen der Revolution Enterprise-Tools wird nicht unterstützt.

Parallele Installationen werden jedoch unterstützt, wenn R Server (eigenständig) mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] oder SQL Server 2016 verwendet wird.

### <a name="unable-to-uninstall-older-components"></a>Deinstallieren älterer Komponenten nicht möglich

Wenn Sie Probleme beim Entfernen einer älteren Version haben, müssen Sie unter Umständen die Registrierung bearbeiten, um betroffene Schlüssel zu entfernen.

> [!IMPORTANT]
> Dieses Problem tritt nur auf, wenn Sie eine Vorabversion von Microsoft R Server oder eine CTP-Version von SQL Server 2016 R Services installiert haben.
  
1. Öffnen Sie die Windows-Registrierung, und suchen Sie folgenden Schlüssel: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Löschen Sie einen der folgenden Einträge, wenn er vorhanden ist und der Schlüssel nur den Wert `sEstimatedSize2`enthält:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (für 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (für 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (für 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (für 7.5.0)
  
## <a name="see-also"></a>Siehe auch

[Machine Learning-Server (eigenständig)](../../advanced-analytics/r/r-server-standalone.md)
