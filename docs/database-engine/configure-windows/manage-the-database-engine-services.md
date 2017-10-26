---
title: Verwalten des Datenbankmodul-Dienstes | Microsoft-Dokumentation
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
- SQL Server Configuration Manager, accessing
- Database Engine [SQL Server], services
- managing services [SQL Server], about service management
- services [SQL Server]
- SQL Server Agent service, managing
- SQL Server services, about SQL Server service
- MSSQLServer
- server configuration [SQL Server]
- managing services [SQL Server]
- SQL Server Agent service
- services [SQL Server], managing
- administering SQL Server, services
- SQL Server services
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f3aa60ecd19dc22669cc98915fb853d4480d1fa5
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="manage-the-database-engine-services"></a>Verwalten der Datenbankmoduldienste
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird unter den Betriebssystemen als Dienst ausgeführt. Ein Dienst ist ein Anwendungstyp, der im Hintergrund ausgeführt wird. Dienste stellen gewöhnlich wichtige Betriebssystemfunktionen bereit, wie z. B. Webbereitstellung, Ereignisprotokollierung oder Dateibereitstellung. Dienste können ausgeführt werden, ohne dass auf dem Computerdesktop eine Benutzeroberfläche angezeigt wird. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent und mehrere andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten werden als Dienste ausgeführt. Diese Dienste werden in der Regel zusammen mit dem Betriebssystem gestartet. Dies hängt von der Konfiguration während der Installation ab. Manche Dienste werden standardmäßig nicht gestartet. In diesem Abschnitt wird die Verwaltung verschiedener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste beschrieben. Vor dem Anmelden an einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sollten Sie wissen, wie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gestartet, beendet, angehalten, fortgesetzt und neu gestartet wird. Nach dem Anmelden können Sie verschiedene Aufgaben ausführen, wie z. B. das Verwalten des Servers oder das Abfragen einer Datenbank.  
  
## <a name="using-the-sql-server-service"></a>Verwenden des SQL Server-Diensts  
 Beim Starten einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst. Nach dem Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensts können Benutzer neue Verbindungen mit dem Server herstellen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst kann als Dienst lokal oder remote gestartet und beendet werden. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst wird als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) bezeichnet, wenn es sich um die Standardinstanz handelt, oder als MSSQL$*\<Instanzname>* bei einer benannten Instanz.  
  
## <a name="using-sql-server-configuration-manager"></a>Verwenden des SQL Server-Konfigurations-Managers  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager können Sie verschiedene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste beschrieben.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager kann keine [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-Dienste verwalten.  
  
 Mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager können auch die Eigenschaften des ausgewählten Diensts angezeigt werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ist ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] -MMC-Snap-In (Microsoft Management Console). Weitere Informationen über MMC und die Funktionsweise von Snap-Ins finden Sie in der Windows-Hilfe.  
  
 **So greifen Sie auf den SQL Server-Konfigurations-Manager zu**  
  
-   Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
 **So greifen Sie über Windows 8 auf den SQL Server-Konfigurations-Manager zu**  
  
 Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager beim Ausführen von Windows 8.0 nicht als Anwendung angezeigt. Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager zu öffnen, geben Sie im Charm **Suchen** unter **Apps**Folgendes ein: **SQLServerManager12.msc** (für [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]), **SQLServerManager11.msc** (für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) oder **SQLServerManager10.msc** (für[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ein. Drücken Sie dann die **EINGABETASTE**.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|||  
|-|-|  
|[Sicherheitsanforderungen für das Verwalten von Diensten](../../database-engine/configure-windows/security-requirements-for-managing-services.md)|[Verhindern des automatischen Starts einer Instanz von SQL Server &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)|  
|[Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|[Ändern des Dienststartkontos für SQL Server &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-change-the-service-startup-account.md)|  
|[Ausführen von SQL Server mit oder ohne Netzwerk](../../database-engine/configure-windows/run-sql-server-with-or-without-a-network.md)|[Konfigurieren von Serverstartoptionen &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)|  
|[SQL Server-Browserdienst &#40;Datenbankmodul und SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)|[Ändern des Kennworts der von SQL Server verwendeten Konten &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-change-the-password-of-the-accounts-used.md)|  
|[Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md)|[Konfigurieren von SQL Server-Fehlerprotokollen](../../database-engine/configure-windows/scm-services-configure-sql-server-error-logs.md)|  
|[Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|[Ändern des Serverauthentifizierungsmodus](../../database-engine/configure-windows/change-server-authentication-mode.md)|  
|[Starten von SQL Server im Einzelbenutzermodus](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)|[SQL Writer-Dienst](../../database-engine/configure-windows/sql-writer-service.md)|  
|[Starten Sie von SQL Server mit Minimalkonfiguration](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)|[Senden einer Nachricht über das Herunterfahren &#40;Eingabeaufforderung&#41;](../../database-engine/configure-windows/broadcast-a-shutdown-message-command-prompt.md)|  
|[Herstellen einer Verbindung mit einem anderen Computer &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)|[Anmelden an einer Instanz von SQL Server &#40;Befehlszeile&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[Festlegen des automatischen Starts einer Instanz von SQL Server &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)|[Konfigurieren von Dateisystemberechtigungen für den Datenbankmodulzugriff](../../database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Konfigurieren des SQL Server-Agents](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900)  
  
 [Anmelden an SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
  

