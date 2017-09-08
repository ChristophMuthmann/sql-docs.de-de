---
title: "Erstellen eines eigenständigen R-Servers | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f39a03ecf7b74e0e1305d692a71c28609c80bf0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-standalone-r-server"></a>Erstellen eines eigenständigen R-Servers

SQL Server-Setup umfasst die Option zum Installieren eines Machine learning-Server, der außerhalb von SQL Server ausgeführt wird. 

Diese Option ist möglicherweise nützlich, wenn Sie zum Entwickeln von R-Lösungen mit hoher Leistung unter Windows und anschließend die Lösungen auf anderen Plattformen freigeben müssen. Die Serveroption können auch richten eine Umgebung zum Erstellen von Lösungen für die Ausführung für diese remote rechenkontexte unterstützt:
  
  + Eine Instanz von SQL Server, die R Services ausführt
  + Eine Instanz von R Server, die einen Hadoop- oder Spark-Cluster verwendet
  + Teradata-Analyse in der Datenbank
  + R Server unter Linux 

Dieses Thema beschreibt die Einrichtungsschritte in SQL Server-Setup für Microsoft R Server und Microsoft Machine Learning-Server.

## <a name="which-should-i-install"></a>Welche sollte ich installieren?

**Microsoft R Server** wurde zuerst als Teil von SQL Server 2016 angeboten wird, und die Sprache "R" unterstützt. Die letzte Version von Microsoft R Server wurde 9.0.1.
In SQL Server 2017 R Server umbenannt wurde **Microsoft Machine Learning-Server**, mit Unterstützung für Python hinzugefügt. Die neueste Version von Microsoft Machine Learning-Server ist 9.1.0.

Microsoft R Server und Microsoft Machine Learning-Server ist die Enterprise Edition erforderlich.

+ [Installieren Sie Microsoft R Server (eigenständig) mit SQL Server-setup](#bkmk_installRServer)
+ [Installieren Sie Microsoft Machine Learning-Server (eigenständig) mit SQL Server-setup](#bkmk_installRServer) 

  Für die Installation ist eine SQL Server-Lizenz erforderlich. Upgrades werden in der Regel auf den SQL Server-Versionsrhythmus ausgerichtet. Dadurch wird sichergestellt, dass Ihre Entwicklungstools synchron mit der Version sind, die im SQL Server-Rechenkontext ausgeführt wird.

+ [Installieren von R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

  Mit dieser Option wird die R-Server mithilfe der Supportrichtlinie für moderne Lifecycle installiert. Sie können dieses Installationsprogramm auch nach dem Setup zum Aktualisieren einer Instanz von SQL Server 2016 ausführen. Derzeit Sie _kann nicht_ Python-Unterstützung mit dieser Option installieren. Um Python zu erhalten, müssen Sie Machine Learning-Servers mit 2017 von SQL Server-Setup installieren.

##  <a name="bkmk_installRServer"></a>Gewusst wie: Installieren von Microsoft-Machine Learning-Server (eigenständig)
  
1. Wenn Sie eine frühere Version von Microsoft R Server installiert haben, wird empfohlen, dass Sie diese zunächst deinstallieren.

2. 2017 von SQL Server-Setup ausführen.
  
3. Klicken Sie auf die **Installation** , und wählen Sie **neue Machine Learning-Server (Standalone) Installation**.

4. Nachdem die Überprüfung der Regeln abgeschlossen ist, akzeptieren Sie SQL Server-Lizenzbedingungen, und wählen Sie eine neue Installation.

5. Auf der **Funktionsauswahl** Seite die folgenden Optionen sollte bereits ausgewählt werden:
    
    - Microsoft-Machine Learning-Server (eigenständig)
    
    - R und Python werden beide standardmäßig ausgewählt.
    
    Alle anderen Optionen sollten ignoriert werden.

6.  Akzeptieren Sie die Lizenzbedingungen für das Herunterladen und Installieren von Machine learning-Komponenten. Ein separaten Volumenlizenzvertrag ist erforderlich für Microsoft R Open und Python. 
    
    Wenn die Schaltfläche **Annehmen** deaktiviert wird, können Sie auf **Weiter**klicken. 
    
    Die Installation dieser Komponenten (und aller möglicherweise von ihnen geforderten Voraussetzungen) kann eine Weile dauern. 
    
    Wenn der Computer nicht über Internetzugriff verfügt, sollten Sie die Installationsprogramme für die Komponente im Voraus herunterladen. Weitere Informationen finden Sie unter [ML Installieren von Komponenten ohne Internetzugang](./installing-ml-components-without-internet-access.md). 
    
7.  Überprüfen Sie Ihre Auswahl auf der Seite **Installationsbereit** , und klicken Sie anschließend auf **Installieren**.


Weitere Informationen über die automatisierte oder Offline-Installation finden Sie unter [Installieren von Microsoft R Server über die Befehlszeile](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md).

###  <a name="bkmk_installRServer"></a> Installieren von Microsoft R-Server (eigenständig)  

1. Wenn Sie eine frühere Version von Microsoft R Server oder eine beliebige Version von Revolution Analytics-Tools installiert haben, müssen Sie es zunächst deinstallieren.  Weitere Informationen finden Sie unter [Ausführen eines Upgrades von einer älteren Version von Microsoft R Server](#bkmk_Uninstall).

2. Führen Sie SQL Server 2016-Setup. Es wird empfohlen, dass Sie Servicepack 1 oder höher installieren.

3. Klicken Sie auf der Registerkarte **Installation** auf **New R Server (Standalone) installation** (Neue R-Server -Installation (eigenständig)).
    
     ![Setupoption für R Server (eigenständig)](media/rsql-rstandalonesetup.png "Setupoption für R Server (eigenständig)")
    
4.  Auf der Seite **Feature selection** (Funktionsauswahl) sollte die folgende Option bereits aktiviert sein:
    
    **R Server (eigenständig)**  
    
    Alle anderen Optionen können ignoriert werden. Installieren Sie SQL Server R Services oder SQL Server-Databae-Modul nicht.
    
5.  Akzeptieren Sie die Lizenzbedingungen für das Herunterladen und Installieren von Microsoft R Open. Wenn die Schaltfläche **Annehmen** deaktiviert wird, können Sie auf **Weiter**klicken. 
    
    Die Installation dieser Komponenten (und aller möglicherweise von ihnen geforderten Voraussetzungen) kann eine Weile dauern.
    
6.  Überprüfen Sie Ihre Auswahl auf der Seite **Installationsbereit** , und klicken Sie anschließend auf **Installieren**.  


### <a name="upgrade-an-existing-r-server-to-901"></a>Aktualisieren eines vorhandenen R-Servers auf 9.0.1

Bei der Installation einer früheren Version von Microsoft R Server (eigenständig) können Sie die Instanz, um neuere Versionen der R-Komponenten verwenden, aktualisieren. Das Upgrade ändert sich auch auf den Server-Supportrichtlinie für moderne Lebenszyklus. Dadurch wird die Instanz auf einem anderen Zeitplan häufiger aktualisiert werden, als die SQL Server-Versionen.

1. Installieren Sie Microsoft R Server (eigenständig), wenn es nicht bereits installiert ist.

2. Separate Windows-basierten Installationsprogramm ausgehend von den Orten hier aufgeführten Download: [führen Microsoft R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall).

3. Führen Sie das Installationsprogramm, und führen Sie die [diese Anweisungen](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer).


### <a name="change-in-default-folder-for-r-packages"></a>Ändern Sie Ordner für R-Pakete im Standardmodus

Bei der Installation mit SQL Server-Setup werden R-Bibliotheken installiert, in einem Ordner, der SQL Server-Version, die Sie für das Setup verwendet zugeordnet. Darüber hinaus finden Sie in diesem Ordner Beispieldaten, die Dokumentation für die R-Basispakete sowie die Dokumentation der R-Tools und der Laufzeit.

**R Server (eigenständig) mit Installation mithilfe von SQL Server 2016**

`C:\Program Files\Microsoft SQL Server\130\R_SERVER`

**R Server (eigenständig) mit Installation mithilfe von SQL Server 2017**

`C:\Program Files\Microsoft SQL Server\140\R_SERVER`

**Setup unter Verwendung von eigenständigen Windows installer**

Allerdings werden bei der Installation mit dem separate Windows Installer oder wenn Sie ein upgrade mit dem separate Windows Installer, R-Bibliotheken in den folgenden Ordner für die R-Server verschoben:

`C:\Program Files\Microsoft\R Server\R_SERVER`
      
**Installation von R-Serie "oder" Machine LEarning-Dienste In Datenbanken**

Wenn Sie eine Instanz von SQL Server R Services (Datenbankintern) "oder" Machine Learning-Services (Datenbankintern) installiert haben und diese Instanz befindet sich auf demselben Computer, werden die R-Bibliotheken und Tools standardmäßig in einem anderen Ordner installiert:

`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`

Rufen Sie nicht direkt die R-Pakete oder -Dienstprogramme auf, die der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz zugeordnet sind. Wenn der Server für R und R Services auf demselben Computer installiert sind, wenn Sie "rgui.exe" oder andere Tools ausführen müssen, verwenden Sie die R-Tools und die Pakete installiert, indem Sie den Ordner R_SERVER.


### <a name="development-tools"></a>Entwicklungstools

Eine Entwicklungsaufgabe IDE ist nicht als Teil von Setup installiert. Zusätzliche Tools sind nicht erforderlich, da alle Standardtools eingeschlossen werden würde, die mit einer Verteilung von R oder Python angegeben werden.

Es wird empfohlen, dass Sie versuchen, die die neue Version von [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], wie Visual Studio R und Python, als auch SQL Server- und BI-Tools unterstützt. Sie können jedoch bevorzugte Entwicklungsumgebung einschließlich RStudio.

## <a name="troubleshooting"></a>Problembehandlung  

### <a name="incompatible-version-of-r-client-and-r-server"></a>Inkompatible Version von R Client und R Server

Wenn Sie die neueste Version von Microsoft R Client installieren und anschließend verwenden, um R mittels eines fernen Rechenkontexts auf SQL Server zu verwenden, erhalten Sie möglicherweise die folgende Fehlermeldung:

*Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

In der Regel wird die Version von R, die mit SQL Server R Services installiert ist, aktualisiert, wenn Service Releases veröffentlicht werden. Installieren Sie alle Servicepacks, um sicherzustellen, dass Sie stets über die aktuellsten Versionen von R-Komponenten verfügen. Für eine Kompatibilität mit Microsoft R Client 9.0.0 müssen Sie die Updates installieren, die in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262)beschrieben werden. 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Installieren von Microsoft R Server in einer Instanz von SQL Server auf Windows Core

In der RTM-Version von SQL Server 2016 lag ein bekanntes Problem beim Hinzufügen von Microsoft R Server für eine Instanz auf Windows Server Core-Edition. Dies wurde behoben.

Wenn dieses Problem auftritt, können Sie die in [KB3164398](https://support.microsoft.com/kb/3164398) beschriebene Fehlerbehebung anwenden, um die R-Funktion zur vorhandenen Instanz auf Windows Server Core hinzuzufügen.   Weitere Informationen finden Sie unter [Microsoft R Server (eigenständig) kann nicht auf einem Windows Server Core-System installiert werden](https://support.microsoft.com/kb/3168691).


###  <a name="bkmk_Uninstall"></a> Ausführen eines Upgrades von einer älteren Version von Microsoft R Server

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

[Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)


