---
title: 'Lektion 2: Herstellen einer Verbindung von einem anderen Computer | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e9fcfd0dfb1171371a8b1ead7543ec14d67035d1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-connecting-from-another-computer"></a>Lektion 2: Herstellen einer Verbindung von einem anderen Computer
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Zum Erhöhen der Sicherheit ist der Zugriff auf [!INCLUDE[ssDE](../includes/ssde-md.md)] der Developer-, Express- und Evaluation-Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] von einem anderen Computer aus nach der Erstinstallation nicht möglich. In dieser Lektion erfahren Sie, wie Sie die Protokolle aktivieren, die Ports konfigurieren und die Windows-Firewall für das Herstellen von Verbindungen von anderen Computern konfigurieren.  
  
Diese Lektion enthält die folgenden Aufgaben:  
  
-   [Aktivieren von Protokollen](#protocols)  
  
-   [Konfigurieren eines festen Ports](#port)  
  
-   [Öffnen von Ports in der Firewall](#firewall)  
  
-   [Herstellen einer Verbindung mit dem Datenbankmodul von einem anderen Computer](#otherComp)  
  
-   [Herstellen einer Verbindung mithilfe des SQL Server-Browserdiensts](#browser)  
  
## <a name="protocols"></a>Aktivieren von Protokollen  
Aus Sicherheitsgründen werden [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], Developer und Evaluation nur mit begrenzter Netzwerkkonnektivität installiert. Verbindungen mit [!INCLUDE[ssDE](../includes/ssde-md.md)] können von Tools hergestellt werden, die auf demselben Computer ausgeführt werden. Von anderen Computern aus ist dies jedoch nicht möglich. Wenn Sie beabsichtigen, Ihre Entwicklungsarbeiten auf demselben Computer auszuführen, auf dem auch das [!INCLUDE[ssDE](../includes/ssde-md.md)]installiert ist, müssen keine zusätzlichen Protokolle aktiviert werden. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] stellt eine Verbindung mit [!INCLUDE[ssDE](../includes/ssde-md.md)] mithilfe des Shared Memory-Protokoll her. Dieses Protokoll ist bereits aktiviert.  
  
Wenn Sie planen, die Verbindung mit [!INCLUDE[ssDE](../includes/ssde-md.md)] von einem anderen Computer herzustellen, müssen Sie ein Protokoll aktivieren, z. B. TCP/IP.  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>So aktivieren Sie TCP/IP-Verbindungen von einem anderen Computern  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    > Möglicherweise steht sowohl die 32-Bit- als auch die 64-Bit-Option zur Verfügung.  
  
    > [!NOTE]  
    > Da der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../includes/msconame-md.md)] -Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt. Der Dateiname enthält eine Zahl, die die Versionsnummer von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]darstellt. Mit dem Befehl „Ausführen“ können Sie den Konfigurations-Manager öffnen. Nachfolgend finden Sie die Pfade zu den letzten vier Versionen, wenn Windows auf dem Laufwerk C: installiert ist.  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
2.  Erweitern Sie im **SQL Server-Konfigurations-Manager**den Eintrag **SQL Server-Netzwerkkonfiguration**, und klicken Sie anschließend auf **Protokolle für** *<InstanceName>*.  
  
    Die Standardinstanz (eine unbenannte Instanz) wird als **MSSQLSERVER**aufgelistet. Wenn Sie eine benannte Instanz installiert haben, wird der von Ihnen angegebene Name aufgeführt. [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] wird als **SQLEXPRESS**installiert, es sei denn, der Name wurde während des Setups geändert.  
  
3.  Klicken Sie in der Liste der Protokolle mit der rechten Maustaste auf das zu aktivierende Protokoll (**TCP/IP**), und klicken Sie anschließend auf **Aktivieren**.  
  
    > [!NOTE]  
    > Wenn Sie Änderungen an Netzwerkprotokollen vorgenommen haben, müssen Sie den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Dienst neu starten. Dieser Schritt wird in der nächsten Aufgabe ausgeführt.  
  
## <a name="port"></a>Konfigurieren eines festen Ports  
Zum Erhöhen der Sicherheit wird die Windows-Firewall von Windows Server 2008, [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]und Windows 7 aktiviert. Um von einem anderen Computer eine Verbindung mit dieser Instanz herzustellen, müssen Sie einen Kommunikationsport in der Firewall öffnen. Die Standardinstanz von [!INCLUDE[ssDE](../includes/ssde-md.md)] lauscht an Port 1433; aus diesem Grund ist es nicht erforderlich, einen festen Port zu konfigurieren. Benannte Instanzen, einschließlich [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] , lauschen jedoch an dynamischen Ports. Bevor Sie einen Port in der Firewall öffnen können, müssen Sie [!INCLUDE[ssDE](../includes/ssde-md.md)] so konfigurieren, dass an einem bestimmten Port gelauscht wird, der als fester oder statischer Port bezeichnet wird. Andernfalls wird von [!INCLUDE[ssDE](../includes/ssde-md.md)] bei jedem Start möglicherweise ein anderer Port überwacht. Weitere Informationen zu Firewalls, den Standardeinstellungen der Windows-Firewall und eine Beschreibung der TCP-Ports, die sich auf Datenbankmodul, Analysis Services, Reporting Services und Integration Services auswirken, finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!NOTE]  
> Portnummernzuweisungen werden von der Internet Assigned Numbers Authority verwaltet und sind unter [http://www.iana.org](http://go.microsoft.com/fwlink/?LinkId=48844)aufgelistet. Portnummern sollten von 49152 bis 65535 zugewiesen werden.  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>Konfigurieren von SQL Server für das Lauschen an einem bestimmten Ports  
  
1.  Erweitern Sie im [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager **SQL Server-Netzwerkkonfiguration**, und klicken Sie anschließend auf die Serverinstanz, die Sie konfigurieren möchten.  
  
2.  Doppelklicken Sie im rechten Bereich auf **TCP/IP**.  
  
3.  Klicken Sie im Dialogfeld **TCP/IP-Eigenschaften** auf die Registerkarte **IP-Adressen** .  
  
4.  Geben Sie im Feld **TCP-Port** des Abschnitts **IPAll** eine verfügbare Portnummer ein. Geben Sie für die Zwecke dieses Tutorials **49172**ein.  
  
5.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen, und klicken Sie auf **OK** , um die Warnung zu bestätigen, dass der Dienst neu gestartet werden muss.  
  
6.  Klicken Sie im linken Bereich auf **SQL Server-Dienste**.  
  
7.  Klicken Sie im rechten Bereich mit der rechten Maustaste auf die Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]und anschließend auf **Neu starten**. Nach dem Neustart lauscht [!INCLUDE[ssDE](../includes/ssde-md.md)] am Port **49172**.  
  
## <a name="firewall"></a>Öffnen von Ports in der Firewall  
Durch Firewallsysteme kann der nicht autorisierte Zugriff auf Computerressourcen verhindert werden. Um bei aktivierter Firewall von einem anderen Computer eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] herzustellen, müssen Sie einen Port in der Firewall öffnen.  
  
> [!IMPORTANT]  
> Das Öffnen von Ports in der Firewall kann dazu führen, dass der Server böswilligen Angriffen ausgesetzt ist. Daher sollten Sie Ports grundsätzlich nur dann öffnen, wenn Sie sicher sind, dass Sie das Konzept der Firewallsysteme verstanden haben. Weitere Informationen finden Sie unter [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
Nachdem Sie [!INCLUDE[ssDE](../includes/ssde-md.md)] so konfiguriert haben, dass ein fester Port verwendet wird, müssen Sie die folgenden Anweisungen ausführen, um diesen Port in der Windows-Firewall zu öffnen. (Sie müssen keinen festen Port für die Standardinstanz konfigurieren, da für diese Instanz bereits TCP-Port 1433 als fester Port festgelegt ist.)  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>So öffnen Sie einen Port in der Windows-Firewall für den TCP-Zugriff (Windows 7)  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**, geben Sie **WF.msc**ein, und klicken Sie anschließend auf **OK**.  
  
2.  Klicken Sie im linken Bereich von **Windows-Firewall mit erweiterter Sicherheit**mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie anschließend im Aktionsbereich auf **Neue Regel** .  
  
3.  Wählen Sie im Dialogfeld **Regeltyp** die Option **Port**aus, und klicken Sie anschließend auf **Weiter**.  
  
4.  Wählen Sie im Dialogfeld **Protokoll und Ports** die Option **TCP**aus. Wählen Sie **Bestimmte lokale Ports**aus, und geben Sie anschließend die Portnummer der Instanz von [!INCLUDE[ssDE](../includes/ssde-md.md)]ein. Geben Sie 1433 für die Standardinstanz ein. Geben Sie **49172** ein, wenn Sie eine benannte Instanz konfigurieren und in der vorherigen Aufgabe einen festen Port konfiguriert haben. Klicken Sie auf **Weiter**.  
  
5.  Wählen Sie im Dialogfeld **Aktion** die Option **Verbindung zulassen**aus, und klicken Sie anschließend auf **Weiter**.  
  
6.  Wählen Sie im Dialogfeld **Profil** beliebige Profile aus, die die Verbindungsumgebung des Computers beschreiben, wenn Sie eine Verbindung zum [!INCLUDE[ssDE](../includes/ssde-md.md)]herstellen möchten, und klicken Sie dann auf **Weiter**.  
  
7.  Geben Sie im Dialogfeld **Name** einen Namen und eine Beschreibung für die Regel ein, und klicken Sie dann auf **Fertig stellen**.  
  
Weitere Informationen zur Konfiguration der Firewall, einschließlich Anweisungen für [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]finden Sie unter [Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md). Weitere Informationen zu den Standardeinstellungen der Windows-Firewall und eine Beschreibung der TCP-Ports, die sich auf Datenbankmodul, Analysis Services, Reporting Services und Integration Services auswirken, finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="otherComp"></a>Herstellen einer Verbindung mit dem Datenbankmodul von einem anderen Computer  
Nachdem Sie [!INCLUDE[ssDE](../includes/ssde-md.md)] für das Lauschen an einem festen Port konfiguriert und diesen Port in der Firewall geöffnet haben, können Sie jetzt von einem anderen Computer eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] herstellen.  
  
Wenn der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Browser-Dienst auf dem Servercomputer ausgeführt wird und die Firewall den UDP-Port 1434 geöffnet hat, kann die Verbindung mithilfe des Computer- und des Instanznamens hergestellt werden. Aus Sicherheitsgründen wird in unserem Beispiel der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Browser-Dienst nicht verwendet.  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>So stellen Sie von einem anderen Computer eine Verbindung mit dem Datenbankmodul her  
  
1.  Melden Sie sich an einem zweiten Computer, auf dem sich die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Clienttools befinden, mit einem Konto an, das autorisiert ist, eine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]herzustellen, und öffnen Sie [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Bestätigen Sie im Dialogfeld **Verbindung mit Server herstellen** in der Liste **Servertyp** die Option **Datenbankmodul** .  
  
3.  Geben Sie im Feld **Servername** für das Protokoll **tcp:** ein, gefolgt vom Namen des Computers, einem Komma und der Portnummer. Beim Herstellen einer Verbindung mit der Standardinstanz wird automatisch Port 1433 angenommen und muss nicht angegeben werden. Geben Sie daher **tcp:***<Computername>* ein. Geben Sie in unserem Beispiel für eine benannte Instanz **tcp:***<Computername>***,49172** ein.  
  
    > [!NOTE]  
    > Wenn Sie **tcp:** nicht im Feld **Servername** eingeben, testet der Client alle aktivierten Protokolle in der Reihenfolge, die in der Clientkonfiguration festgelegt ist.  
  
4.  Bestätigen Sie im Feld **Authentifizierung** die **Windows-Authentifizierung**, und klicken Sie anschließend auf **Verbinden**.  
  
## <a name="browser"></a>Herstellen einer Verbindung mithilfe des SQL Server-Browserdiensts  
Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Browser-Dienst lauscht auf eingehende Anforderungen für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Ressourcen und stellt Informationen zu den auf dem Computer installierten [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanzen bereit. Wenn der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Browser-Dienst ausgeführt wird, können Benutzer Verbindungen mit benannten Instanzen herstellen, indem sie den Computer- und Instanznamen angeben, anstatt den Computernamen und die Portnummer. Da der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Browser nicht authentifizierte UDP-Anforderungen empfängt, ist er während der Installation nicht immer eingeschaltet. Eine Beschreibung des Diensts und eine Erklärung dazu, wann er eingeschaltet ist, finden Sie unter [SQL Server-Browserdienst &#40;Datenbankmodul und SSAS&#41;](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).  
  
Um den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Browser zu verwenden, müssen Sie dieselben Schritte wie zuvor ausführen und UDP-Port 1434 in der Firewall öffnen.  
  
Diese Ausführungen beenden das kurze Lernprogramm zur Konnektivität.  
  
## <a name="return-to-tutorials-portal"></a>Zurück zum Portal für die Lernprogramme  
[Lernprogramm: Erste Schritte mit dem Datenbankmodul](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

