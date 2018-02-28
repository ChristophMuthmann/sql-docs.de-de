---
title: Konfigurieren von Serverstartoptionen (SQL Server-Konfigurations-Manager) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- SQL Server, startup parameters
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- startup parameters [SQL Server]
- SQL Server services, setting startup options
- SQL Server services, setting startup parameters
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ff11f5d2ec4c086733793ebb13e54ab5448b9dd3
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="scm-services---configure-server-startup-options"></a>SCM-Dienste: Konfigurieren der Serverstartoptionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In diesem Thema wird beschrieben, wie Sie Startoptionen, die bei jedem Starten von [!INCLUDE[ssDE](../../includes/ssde-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendet werden, mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers konfigurieren. Weitere Informationen finden Sie unter [Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
### <a name="limitations-and-restrictions"></a>Einschränkungen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager schreibt Startparameter in die Registrierung. Diese werden beim nächsten Start von [!INCLUDE[ssDE](../../includes/ssde-md.md)]wirksam.  
  
 Bei einem Cluster müssen Änderungen auf dem aktiven Server vorgenommen werden, während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] online ist und werden beim nächsten Start von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wirksam. Die Registrierungsaktualisierung der Startoptionen auf dem anderen Knoten findet beim nächsten Failover statt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Konfiguration von Serverstartoptionen ist auf Benutzer beschränkt, die die entsprechenden Einträge in der Registrierung ändern können. Dazu gehören folgende Benutzer.  
  
-   Mitglieder der lokalen Administratorgruppe.  
  
-   Das Domänenkonto, das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet wird, wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] für die Ausführung unter einem Domänenkonto konfiguriert ist.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-configure-startup-options"></a>So konfigurieren Sie Startoptionen  
  
1.  Klicken Sie auf **Start** , zeigen Sie auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers auf der **Startseite**Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    >  -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Apps** im Charm **Suchen** zu öffnen, geben Sie **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Klicken Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im rechten Bereich mit der rechten Maustaste auf **SQL Server (***<Instanzname>***)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie auf der Registerkarte **Startparameter** im Feld **Startparameter angeben** den Parameter ein, und klicken Sie anschließend auf **Hinzufügen**.  
  
     Für den Einzelbenutzermodus geben Sie z. B. im Feld **Startparameter angeben** **-m** ein, und klicken Sie anschließend auf **Hinzufügen**. (Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Einzelbenutzermodus erneut starten, müssen Sie zunächst den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent beenden. Andernfalls stellt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent möglicherweise zuerst eine Verbindung her und verhindert, dass Sie als zweiter Benutzer eine Verbindung herstellen können.)  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Starten Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)]neu.  
  
    > [!WARNING]  
    >  Wenn Sie nicht mehr im Einzelbenutzermodus arbeiten möchten, wählen Sie im Feld Startparameter im Feld **Vorhandene Parameter** den Parameter **-m** aus, und klicken Sie dann auf **Entfernen**. Starten Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] erneut, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im typischen Multibenutzermodus wiederherzustellen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Starten von SQL Server im Einzelbenutzermodus](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [Herstellen einer Verbindung mit SQL Server, wenn Systemadministratoren gesperrt sind](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [Starten, Beenden oder Anhalten des SQL Server-Agent-Diensts](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
 [Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md) 
  
