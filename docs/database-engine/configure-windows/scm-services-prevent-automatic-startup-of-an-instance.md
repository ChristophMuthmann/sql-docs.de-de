---
title: 'SCM-Dienste: Verhindern eines automatischen Starts einer Instanz | Microsoft-Dokumentation'
ms.custom: 
ms.date: 01/06/2016
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
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a47e6e4da6d415de5d5b8fac1150c0da21980f8a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="scm-services---prevent-automatic-startup-of-an-instance"></a>SCM-Dienste: Verhindern eines automatischen Starts einer Instanz
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers verhindern können, dass eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch gestartet wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist normalerweise für den automatischen Start konfiguriert. Sie können diese Einstellung ändern, indem Sie den Startmodus für die Instanz auf manuell festlegen.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>So verhindern Sie das automatische Starten einer Instanz von SQL Server  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers auf der **Startseite**Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Apps** im Charm **Suchen** zu öffnen, geben Sie **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im SQL Server-Konfigurations-Manager **Dienste**, und klicken Sie dann auf **SQL Server**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **MSSQLServer**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Legen Sie im Dialogfeld **SQL Server \<***Instanzname***> Eigenschaften** auf der Registerkarte **Dienst** im Feld **Allgemein** den Wert für **Startmodus** auf **Manuell** fest.  
  
5.  Klicken Sie auf **OK**, um das Dialogfeld **SQL Server \<***Instanzname***> Eigenschaften** zu schließen, und schließen Sie dann den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
