---
title: "Konfigurieren einer Windows-Firewall f&#252;r den Zugriff auf den SSIS-Dienst | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherheit [Integration Services], Firewalls"
  - "Windows-Firewall [Integration Services]"
  - "Nicht autorisierter Zugriff [Integration Services]"
  - "Integration Services-Dienst, Firewalls"
  - "Firewallsysteme [Integration Services]"
  - "SQL Server Integration Services (SSIS), Firewalls"
  - "SSIS, Firewalls"
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Konfigurieren einer Windows-Firewall f&#252;r den Zugriff auf den SSIS-Dienst
    
> [!IMPORTANT]  
>  In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst beschrieben, ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie Objekte, z. B. Pakete, auf dem Integration Services-Server verwalten.  
  
 Durch das Windows-Firewallsystem wird der nicht autorisierte Zugriff auf Computerressourcen über eine Netzwerkverbindung verhindert. Um über diese Firewall auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zuzugreifen, müssen Sie die Firewall so konfigurieren, dass der Zugriff zulässig ist.  
  
> [!IMPORTANT]  
>  Zum Verwalten von Paketen auf einem Remoteserver müssen Sie keine Verbindung mit der Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf dem betreffenden Remoteserver herstellen. Bearbeiten Sie stattdessen die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, sodass die auf dem Remoteserver gespeicherten Pakete von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden. Weitere Informationen finden Sie unter [Konfigurieren des Integration Services-Diensts &#40;SSIS-Dienst&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwendet das DCOM-Protokoll. Weitere Informationen zur Funktionsweise des DCOM-Protokolls über Firewalls finden Sie im Artikel "[Using Distributed COM with Firewalls](http://go.microsoft.com/fwlink/?LinkId=12490)" in der MSDN Library.  
  
 Es gibt zahlreiche verschiedene Firewallsysteme auf dem Markt. Wenn Sie nicht die Windows-Firewall, sondern eine andere Firewall ausführen, suchen Sie in der Firewalldokumentation nach Informationen, die sich auf das von Ihnen verwendete System beziehen.  
  
 Falls die Firewall das Filtern auf Anwendungsebene unterstützt, können Sie mithilfe der Benutzeroberfläche von Windows die für diese Firewall zulässigen Ausnahmen angeben, wie z. B. Programme und Dienste. Andernfalls müssen Sie für DCOM eine begrenzte Anzahl von TCP-Ports konfigurieren. Der zuvor bereitgestellte Link zur Microsoft-Website enthält Informationen zum Angeben der zu verwendenden TCP-Ports.  
  
 Der Integration Services-Dienst verwendet Port 135. Dies kann nicht geändert werden. Sie müssen TCP-Port 135 für den Zugriff auf den Dienstkontroll-Manager (SCM, Service Control Manager) öffnen. SCM führt u. a. folgende Tasks aus: Starten und Beenden von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensten und Übertragen von Steuerungsanforderungen an den ausgeführten Dienst.  
  
 Die Informationen im folgenden Abschnitt gelten ausschließlich für die Windows-Firewall. Zum Konfigurieren des Windows-Firewallsystems können Sie einen Befehl an der Eingabeaufforderung ausführen oder aber Eigenschaften im Dialogfeld Windows-Firewall festlegen.  
  
 Weitere Informationen zu den Standardeinstellungen der Windows-Firewall und eine Beschreibung der TCP-Ports, die sich auf Datenbankmodul, Analysis Services, Reporting Services und Integration Services auswirken, finden Sie unter [Configure the Windows Firewall to Allow SQL Server Access](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) (Konfigurieren der Windows-Firewall für den SQL Server-Zugriff).  
  
## Konfigurieren einer Windows-Firewall  
 Sie können die folgenden Befehle verwenden, um TCP-Port 135 zu öffnen, MsDtsSrvr.exe der Ausnahmeliste hinzuzufügen und den Bereich zum Aufheben der Blockierung für die Firewall anzugeben.  
  
#### So konfigurieren Sie eine Windows-Firewall mithilfe des Eingabeaufforderungsfensters  
  
1.  Führen Sie den folgenden Befehl aus: `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  Führen Sie den folgenden Befehl aus: `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  Ersetzen Sie zum Öffnen der Firewall für alle Computer sowie für Computer im Internet scope=SUBNET durch scope=ALL.  
  
 In der folgenden schrittweisen Anleitung wird beschrieben, wie Sie mithilfe der Windows-Benutzeroberfläche TCP-Port 135 öffnen, MsDtsSrvr.exe der Ausnahmeliste hinzufügen und den Bereich zum Aufheben der Blockierung für die Firewall angeben.  
  
#### So konfigurieren Sie eine Firewall mithilfe des Dialogfelds "Windows-Firewall"  
  
1.  Doppelklicken Sie in der Systemsteuerung auf **Windows-Firewall**.  
  
2.  Klicken Sie im Dialogfeld **Windows-Firewall** auf die Registerkarte **Ausnahmen** , und klicken Sie dann auf **Programm hinzufügen**.  
  
3.  Klicken Sie im Dialogfeld **Programm hinzufügen** auf **Durchsuchen**, navigieren Sie zum Ordner „Programme\Microsoft SQL Server\100\DTS\Binn, klicken Sie auf MsDtsSrvr.exe“, und klicken Sie anschließend auf **Öffnen**. Klicken Sie auf **OK** , um das Dialogfeld **Programm hinzufügen** zu schließen.  
  
4.  Klicken Sie auf der Registerkarte **Ausnahmen** auf **Port hinzufügen**.  
  
5.  Geben Sie im Dialogfeld **Port hinzufügen** **RPC(TCP/135)** oder einen anderen beschreibenden Namen in das Feld **Name** ein, geben Sie **135** in das Feld **Portnummer** ein, und wählen anschließend Sie **TCP** aus.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwendet immer Port 135. Sie können keinen anderen Port angeben.  
  
6.  Im Dialogfeld **Port hinzufügen** können Sie optional auf **Bereich ändern** klicken, um den Standardbereich zu ändern.  
  
7.  Wählen Sie im Dialogfeld **Bereich ändern** das Optionsfeld **My network (subnet only)** (Eigenes Netzwerk (nur Subnetz)) aus, oder geben Sie eine benutzerdefinierte Liste ein, und klicken Sie anschließend auf **OK**.  
  
8.  Klicken Sie auf **OK** , um das Dialogfeld **Port hinzufügen**zu schließen.  
  
9. Klicken Sie auf **OK** , um das Dialogfeld **Windows-Firewall**zu schließen.  
  
    > [!NOTE]  
    >  In dieser Prozedur wird die Systemsteuerungsoption **Windows-Firewall** verwendet, um die Windows-Firewall zu konfigurieren. Über die Option **Windows-Firewall** wird nur die Firewall für das Profil des aktuellen Netzwerkspeicherorts konfiguriert. Sie können die Windows-Firewall jedoch auch mithilfe des **netsh**-Befehlszeilentools oder des MMC-Snap-Ins ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console) namens „Windows-Firewall mit erweiterter Sicherheit“ konfigurieren. Weitere Informationen über diese Tools finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## Siehe auch  
 [Konfigurieren des Integration Services-Diensts &#40;SSIS-Dienst&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  