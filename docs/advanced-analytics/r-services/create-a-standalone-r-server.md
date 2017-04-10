---
title: "Erstellen eines eigenst&#228;ndigen R-Servers | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# Erstellen eines eigenst&#228;ndigen R-Servers
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup umfasst eine Option für das Installieren von **Microsoft R Server (eigenständig)**. Mit dieser Option können Sie leistungsfähige R-Lösungen unter Windows entwickeln, während Sie eine Verbindung zur Datenbank oder Datenquelle Ihrer Wahl herstellen. Microsoft R Server ist nur in der Enterprise Edition verfügbar.  
  
 Bei der Installation von Microsoft R Server erhalten Sie dieselben verbesserten R-Pakete und Konnektivitätstools, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bereitgestellt werden, es ist jedoch keine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich, und die Ausführung von R-Skripts wird auf dem eigenständigen Computer und nicht in der Datenbank ausgeführt.  
  
> [!NOTE]  
>  Microsoft R Server ist jetzt auch über ein vereinfachtes Setup verfügbar, welches die Instanz in der [Modern Lifecycle](https://support.microsoft.com/help/447912)-Richtlinie registriert. Durch dieses Support-Angebot wird sichergestellt, dass Sie stets die aktuellste Version von R verwenden. Weitere Informationen zur Verwendung des vereinfachten Setups finden Sie unter [Run Microsoft R Server for Windows (Ausführen von Microsoft R Server für Windows)](https://msdnstage.redmond.corp.microsoft.com/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev).
>  
> Wenn Sie Microsoft R Server über das vereinfachte Setup installieren, können Sie jede angegebene Instanz von R Services dahingehend umstellen, dass sie häufiger Aktualisierungen der R-Komponenten erhält. Weitere Informationen finden Sie unter [Verwenden von sqlBindR.exe zum Aktualisieren einer Instanz von R Services](http://www.bing.com).   
  
##  <a name="a-namebkmkinstallrservicesindatabasea-install-microsoft-r-server-standalone"></a><a name="bkmk_installRServicesInDatabase"></a> Installieren von Microsoft R-Server (eigenständig)  
  
1.  Wenn Sie eine frühere Version von Microsoft R Server installiert haben, müssen Sie diese zunächst deinstallieren.  Weitere Informationen finden Sie unter [Ausführen eines Upgrades von einer älteren Version von Microsoft R Server](#bkmk_Uninstall). 

2. Führen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup aus.  
  
2.  Klicken Sie auf der Registerkarte **Installation** auf **New R Server (Standalone) installation** (Neue R-Server -Installation (eigenständig)).  
  
     ![Setup option for R Server Standalone](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "Setup option for R Server Standalone")  
  
3.  Auf der Seite **Feature selection** (Funktionsauswahl) sollte die folgende Option bereits aktiviert sein:  
  
    -   **R Server (eigenständig)**  
  
         Diese Option installiert sowohl freigegebene Funktionen einschließlich Open Source-R-Tools und -Basispakete als auch die erweiterten R-Pakete und -Konnektivitätstools von Microsoft R.  
  
     Alle anderen Optionen können ignoriert werden.  
  
4.  Akzeptieren Sie die Lizenzbedingungen für das Herunterladen und Installieren von Microsoft R Open. Wenn die Schaltfläche **Annehmen** deaktiviert wird, können Sie auf **Weiter** klicken. Die Installation dieser Komponenten (und aller möglicherweise von ihnen geforderten Voraussetzungen) kann eine Weile dauern.   
  
5.  Überprüfen Sie Ihre Auswahl auf der Seite **Installationsbereit**, und klicken Sie anschließend auf **Installieren**.  
  
> [!TIP]
> Weitere Informationen über die automatisierte oder Offline-Installation finden Sie unter [Installieren von Microsoft R Server über die Befehlszeile](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md).

  
## <a name="what-is-installed-and-where-to-find-r-packages"></a>Was wird installiert und wo finden Sie R-Pakete  
 Microsoft R Server enthält die R-Basispakete und eine Reihe von erweiterten R-Paketen, die die parallele Verarbeitung unterstützen, die Leistung verbessern und Verbindungen zu Datenquellen ermöglichen, einschließlich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Hadoop.  
  
-   **R-Pakete**  
  
     Die R-Bibliotheken werden zusammen mit anderen Tools und Dienstprogrammen installiert, die mit Microsoft SQL Server 2016 installiert werden. Beispiel:  
  
     `C:\Program Files\Microsoft SQL Server\130\R_SERVER`  
  
     Darüber hinaus finden Sie in diesem Ordner die Dokumentation für die R-Basispakete, die Beispieldaten und die Dokumentation der R-Tools und der Laufzeit.  
  
    > [!NOTE]  
    >  Wenn Sie eine Instanz von SQL Server mit R Services (In-Database) auf demselben Computer installiert haben, werden die R-Bibliotheken und -Tools in einem anderen Ordner installiert: `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`  
    >   
    >  Verwenden Sie nicht die R-Pakete oder -Dienstprogramme, die der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz zugeordnet sind. Verwenden Sie stets die R-Tools und -Pakete im Ordner R_SERVER.  
  
-   **R-Tools**  
  
     Im Rahmen des Setups wird keine R-Entwicklungs-IDE installiert. Sie können RStudio, [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] oder eine beliebige andere Entwicklungsumgebung installieren.  
  
     Zusätzliche Tools sind jedoch nicht erforderlich. Alle standardmäßigen R-Basistools sind in `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin` enthalten.  
  
     Weitere Informationen finden Sie unter [Einrichten oder Konfigurieren von R-Tools](../../advanced-analytics/r-services/setup-or-configure-r-tools.md).  


 
## <a name="troubleshooting"></a>Problembehandlung  

### <a name="incompatible-version-of-r-client-and-r-server"></a>Inkompatible Version von R Client und R Server

Wenn Sie die neueste Version von Microsoft R Client installieren und anschließend verwenden, um R mittels eines fernen Rechenkontexts auf SQL Server zu verwenden, erhalten Sie möglicherweise die folgende Fehlermeldung:

*Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

In der Regel wird die Version von R, die mit SQL Server R Services installiert ist, aktualisiert, wenn Service Releases veröffentlicht werden. Installieren Sie alle Servicepacks, um sicherzustellen, dass Sie stets über die aktuellsten Versionen von R-Komponenten verfügen. Für eine Kompatibilität mit Microsoft R Client 9.0.0 müssen Sie die Updates installieren, die in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262) beschrieben werden. 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Installieren von Microsoft R Server in einer Instanz von SQL Server auf Windows Core
Die Produktversion von SQL Server 2016 wies ein bekanntes Problem auf, wenn Microsoft R Server zu einer Instanz auf Windows Server Core-Edition hinzufügt wurde. Dies wurde behoben. 

Wenn dieses Problem auftritt, können Sie die in [KB3164398](https://support.microsoft.com/kb/3164398) beschriebene Fehlerbehebung anwenden, um die R-Funktion zur vorhandenen Instanz auf Windows Server Core hinzuzufügen.   Weitere Informationen finden Sie unter [Microsoft R Server (eigenständig) kann nicht auf einem Windows Server Core-System installiert werden](https://support.microsoft.com/kb/3168691).


###  <a name="a-namebkmkuninstalla-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> Ausführen eines Upgrades von einer älteren Version von Microsoft R Server  
 Wenn Sie eine Vorabversion von Microsoft R Server installiert haben, müssen Sie diese deinstallieren, bevor Sie auf eine neuere Version aktualisieren können.  
  
**Deinstallieren von Microsoft R Server (eigenständig)**  
  
1.  Klicken Sie in der **Systemsteuerung** auf **Programme hinzufügen/entfernen**, und wählen Sie `Microsoft SQL Server 2016 <version number>` aus.  
  
2.  Wählen Sie im Dialogfeld mit den Optionen zum **Hinzufügen**, **Reparieren** oder **Entfernen** von Komponenten die Option **Entfernen** aus.  
  
3.  Wählen Sie auf der Seite **Funktionen auswählen** unter **Freigegebene Funktionen** die Option **R Server (eigenständig)** aus. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen**, um nur die ausgewählten Komponenten zu deinstallieren.  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>Installation schlägt fehl mit dem Fehler „Es kann jeweils nur ein Revolution Enterprise-Produkt installiert werden.“  
Dieser Fehler kann auftreten, wenn Sie eine ältere Installation von Revolution Analytics-Produkten oder eine Vorabversion von SQL Server R Services verwenden. Sie müssen alle früheren Versionen deinstallieren, bevor Sie eine neuere Version von Microsoft R Server installieren können. Eine parallele Installation mit anderen Versionen der Revolution Enterprise-Tools wird nicht unterstützt.  

Parallele Installationen werden jedoch unterstützt, wenn R Server (eigenständig) mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] verwendet wird. 
  
### <a name="unable-to-uninstall-older-components"></a>Deinstallieren älterer Komponenten nicht möglich   
  
Wenn Sie Probleme beim Entfernen einer älteren Version haben, müssen Sie unter Umständen die Registrierung bearbeiten, um betroffene Schlüssel zu entfernen.  

> [!IMPORTANT]
> Dieses Problem tritt nur auf, wenn Sie eine Vorabversion von Microsoft R Server oder eine CTP-Version von SQL Server 2016 R Services installiert haben.
  
1. Öffnen Sie die Windows-Registrierung, und suchen Sie folgenden Schlüssel: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.  
2. Löschen Sie einen der folgenden Einträge, wenn er vorhanden ist und der Schlüssel nur den Wert `sEstimatedSize2` enthält:  
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (für 8.0.2)  
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (für 8.0.1)  
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (für 8.0.0)  
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (für 7.5.0)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)  
  
  