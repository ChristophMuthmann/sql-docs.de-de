---
title: "Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], firewall systems
- firewall systems, [Database Engine]
- security [SQL Server], firewalls
ms.assetid: 0093b43c-c6b5-4574-9b30-3a0e91e1a1f9
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7d79f9d00344dceb2559d66f7f6f4450597c79f7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-a-windows-firewall-for-database-engine-access"></a>Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff

 > Inhalte, die mit früheren Versionen von SQL Server zusammenhängen, finden Sie unter [Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff](https://msdn.microsoft.com/en-US/library/ms175043(SQL.120).aspx).


  In diesem Thema wird beschrieben, wie eine Windows-Firewall für Datenbankmodulzugriff in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers konfiguriert wird. Durch Firewallsysteme kann der nicht autorisierte Zugriff auf Computerressourcen verhindert werden. Um über eine Firewall auf eine Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] zugreifen zu können, müssen Sie die Firewall auf dem Computer mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entsprechend konfigurieren.  
  
 Weitere Informationen zu den Standardeinstellungen der Windows-Firewall und eine Beschreibung der TCP-Ports, die sich auf das [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services und Integration Services auswirken, finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md). Es gibt zahlreiche verschiedene Firewallsysteme auf dem Markt. Informationen zu den für Ihr System relevanten Einstellungen finden Sie in der Firewalldokumentation.  
  
 Die wichtigsten Schritte zum Konfigurieren des Zugriffs werden im Folgenden beschrieben:  
  
1.  Konfigurieren Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] für die Verwendung eines bestimmten TCP/IP-Ports. In der Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wird Port 1433 verwendet. Sie können diese Einstellung jedoch ändern. Der vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendete Port ist im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll aufgeführt. Instanzen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)] und benannte Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwenden dynamische Ports. Informationen zum Konfigurieren dieser Instanzen zum Verwenden eines bestimmten Ports finden Sie unter [Konfigurieren eines Servers zur Überwachung eines bestimmten TCP-Ports &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Konfigurieren Sie die Firewall so, dass autorisierten Benutzern oder Computern der Zugriff auf diesen Port gewährt wird.  
  
> [!NOTE]  
>  Mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst können Benutzer ohne Kenntnis der Portnummer Verbindungen mit Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] herstellen, die nicht den Port 1433 überwachen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser verwenden möchten, müssen Sie UDP-Port 1434 öffnen. Um eine möglichst sichere Umgebung zu erzielen, lassen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst beendet, und konfigurieren Sie die Clients so, dass sie Verbindungen mithilfe der Portnummer herstellen müssen.  
  
> [!NOTE]  
>  Standardmäßig wird die Windows-Firewall von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows aktiviert. Damit wird Port 1433 geschlossen, um zu verhindern, dass Internetcomputer Verbindungen mit einer Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Ihrem Computer herstellen. Verbindungen zur Standardinstanz über TCP/IP sind nicht möglich, außer wenn Sie Port 1433 erneut öffnen. Die grundlegenden Schritte für die Konfiguration der Windows-Firewall werden in den folgenden Verfahren beschrieben. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
 Als Alternative zum Konfigurieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für das Lauschen an einem festen Port und zum Öffnen des Ports können Sie die ausführbare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datei (Sqlservr.exe) als Ausnahme in die Liste der blockierten Programme aufnehmen. Verwenden Sie diese Methode, wenn Sie weiterhin dynamische Ports verwenden möchten. Auf diese Weise kann nur auf eine einzige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugegriffen werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie eine Windows-Firewall für Datenbankmodulzugriff mit**  
  
     [SQL Server-Konfigurations-Manager](#SSMSProcedure)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
 Das Öffnen von Ports in der Firewall kann dazu führen, dass der Server böswilligen Angriffen ausgesetzt ist. Daher sollten Sie Ports grundsätzlich nur dann öffnen, wenn Sie sicher sind, dass Sie das Konzept von Firewallsystemen verstanden haben. Weitere Informationen finden Sie unter [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
 Gilt für: Windows Vista, Windows 7 und Windows Server 2008  
  
 Anhand der folgenden Prozeduren wird die Windows-Firewall unter Verwendung des MMC-Snap-Ins (Microsoft Management Console) "Windows-Firewall mit erweiterter Sicherheit" konfiguriert. Von der Windows-Firewall mit erweiterter Sicherheit wird nur das aktuelle Profil konfiguriert. Weitere Informationen über die Windows-Firewall mit erweiterter Sicherheit finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access"></a>So öffnen Sie einen Port in der Windows-Firewall für den TCP-Zugriff  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**, geben Sie **WF.msc**ein, und klicken Sie anschließend auf **OK**.  
  
2.  Klicken Sie im linken Bereich von **Windows-Firewall mit erweiterter Sicherheit**mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie anschließend im Aktionsbereich auf **Neue Regel** .  
  
3.  Wählen Sie im Dialogfeld **Regeltyp** die Option **Port**aus, und klicken Sie anschließend auf **Weiter**.  
  
4.  Wählen Sie im Dialogfeld **Protokoll und Ports** die Option **TCP**aus. Wählen Sie **Bestimmte lokale Ports**aus, und geben Sie anschließend die Portnummer der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]ein, z.B. **1433** für die Standardinstanz. Klicken Sie auf **Weiter**.  
  
5.  Wählen Sie im Dialogfeld **Aktion** die Option **Verbindung zulassen**aus, und klicken Sie anschließend auf **Weiter**.  
  
6.  Wählen Sie im Dialogfeld **Profil** beliebige Profile aus, die die Verbindungsumgebung des Computers beschreiben, wenn Sie eine Verbindung zum [!INCLUDE[ssDE](../../includes/ssde-md.md)]herstellen möchten, und klicken Sie dann auf **Weiter**.  
  
7.  Geben Sie im Dialogfeld **Name** einen Namen und eine Beschreibung für die Regel ein, und klicken Sie dann auf **Fertig stellen**.  
  
#### <a name="to-open-access-to-sql-server-when-using-dynamic-ports"></a>So ermöglichen Sie den Zugriff auf SQL Server bei der Verwendung von dynamischen Ports  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**, geben Sie **WF.msc**ein, und klicken Sie anschließend auf **OK**.  
  
2.  Klicken Sie im linken Bereich von **Windows-Firewall mit erweiterter Sicherheit**mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie anschließend im Aktionsbereich auf **Neue Regel** .  
  
3.  Wählen Sie im Dialogfeld **Regeltyp** die Option **Programm**aus, und klicken Sie anschließend auf **Weiter**.  
  
4.  Wählen Sie im Dialogfeld **Programm** die Option **Dieser Programmpfad**aus. Klicken Sie auf **Durchsuchen**, navigieren Sie zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , auf die Sie durch die Firewall hindurch zugreifen möchten, und klicken Sie dann auf **Öffnen**. Standardmäßig befindet sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Verzeichnis **C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe**. Klicken Sie auf **Weiter**.  
  
5.  Wählen Sie im Dialogfeld **Aktion** die Option **Verbindung zulassen**aus, und klicken Sie anschließend auf **Weiter**.  
  
6.  Wählen Sie im Dialogfeld **Profil** beliebige Profile aus, die die Verbindungsumgebung des Computers beschreiben, wenn Sie eine Verbindung zum [!INCLUDE[ssDE](../../includes/ssde-md.md)]herstellen möchten, und klicken Sie dann auf **Weiter**.  
  
7.  Geben Sie im Dialogfeld **Name** einen Namen und eine Beschreibung für die Regel ein, und klicken Sie dann auf **Fertig stellen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gewusst wie: Konfigurieren von Firewalleinstellungen (Azure SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  

