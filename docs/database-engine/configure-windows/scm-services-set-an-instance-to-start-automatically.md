---
title: 'SCM-Dienste: Festlegen einer SQL Server-Instanz auf den automatischen Start | Microsoft-Dokumentation'
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
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8474199d7184a0fb893dad644b00a8ef25e178ff
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>SCM-Dienste: Festlegen einer SQL Server-Instanz auf den automatischen Start
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers festlegen können, dass eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch gestartet wird. Bei der Installation wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalerweise für den automatischen Start konfiguriert. Diese Einstellung kann jederzeit geändert werden.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>So legen Sie für eine Instanz von SQL Server den automatischen Start fest  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers auf der **Startseite**Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Apps** im Charm **Suchen** zu öffnen, geben Sie **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie in **SQL Server-Konfigurations-Manager**den Ordner **Services**, und klicken Sie dann auf **SQL Server**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Namen der Instanz, die automatisch gestartet werden soll, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Legen Sie im Dialogfeld **SQL Server \<***Instanzname***> Eigenschaften** unter **Startmodus** die Option **Automatisch** fest.  
  
5.  Klicken Sie auf **OK**, und schließen Sie dann den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verhindern des automatischen Starts einer Instanz von SQL Server &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Herstellen einer Verbindung mit einem anderen Computer (SQL Server-Konfigurations-Manager)](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
  
