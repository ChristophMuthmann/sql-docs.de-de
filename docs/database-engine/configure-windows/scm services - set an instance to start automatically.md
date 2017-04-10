---
title: "Festlegen des automatischen Starts einer Instanz von SQL Server (SQL Server-Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Automatisches Starten von SQL Server"
  - "SQL Server, automatisches Starten"
  - "Starten von SQL Server, automatisch"
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Festlegen des automatischen Starts einer Instanz von SQL Server (SQL Server-Konfigurations-Manager)
  In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des SQL Server-Konfigurations-Managers festlegen können, dass eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] automatisch gestartet wird. Bei der Installation wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalerweise für den automatischen Start konfiguriert. Diese Einstellung kann jederzeit geändert werden.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### So legen Sie für eine Instanz von SQL Server den automatischen Start fest  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers auf der **Startseite** Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager zu öffnen, geben Sie im Charm **Suchen** unter **Apps** die Zeichenfolge **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie in **SQL Server-Konfigurations-Manager**den Ordner **Services**, und klicken Sie dann auf **SQL Server**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Namen der Instanz, die automatisch gestartet werden soll, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Legen Sie im Dialogfeld **SQL Server \<***Instanzname***> Eigenschaften** unter **Startmodus** die Option **Automatisch** fest.  
  
5.  Klicken Sie auf **OK**, und schließen Sie dann den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager.  
  
## Siehe auch  
 [Verhindern des automatischen Starts einer Instanz von SQL Server &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm services - prevent automatic startup of an instance.md)   
 [Herstellen einer Verbindung mit einem anderen Computer &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/connect-to-another-computer-sql-server-configuration-manager.md)   
 [Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  