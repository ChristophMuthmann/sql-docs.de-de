---
title: Konfigurieren von Serverstartoptionen (SQL Server-Konfigurations-Manager) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 01/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: afa975c31183df845300dbe3e06cc5b7ae272ae9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="scm-services---configure-server-startup-options"></a>SCM-Dienste: Konfigurieren der Serverstartoptionen
  In diesem Thema wird beschrieben, wie Sie Startoptionen, die bei jedem Starten von [!INCLUDE[ssDE](../../includes/ssde-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendet werden, mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers konfigurieren. Weitere Informationen finden Sie unter [Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
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
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Apps** im Charm **Suchen** zu öffnen, geben Sie **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Klicken Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im rechten Bereich mit der rechten Maustaste auf **SQL Server (***<instance_name>***)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie auf der Registerkarte **Startparameter** im Feld **Startparameter angeben** den Parameter ein, und klicken Sie anschließend auf **Hinzufügen**.  
  
     Für den Einzelbenutzermodus geben Sie z. B. im Feld **Startparameter angeben** **-m** ein, und klicken Sie anschließend auf **Hinzufügen**. (Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Einzelbenutzermodus erneut starten, müssen Sie zunächst den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent beenden. Andernfalls stellt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent möglicherweise zuerst eine Verbindung her und verhindert, dass Sie als zweiter Benutzer eine Verbindung herstellen können.)  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Starten Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)]neu.  
  
    > [!WARNING]  
    >  Wenn Sie nicht mehr im Einzelbenutzermodus arbeiten möchten, wählen Sie im Feld Startparameter im Feld **Vorhandene Parameter** den Parameter **-m** aus, und klicken Sie dann auf **Entfernen**. Starten Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] erneut, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im typischen Multibenutzermodus wiederherzustellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten von SQL Server im Einzelbenutzermodus](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [Herstellen einer Verbindung mit SQL Server, wenn Systemadministratoren gesperrt sind](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  

