---
title: "Verhindern des automatischen Starts einer Instanz von SQL Server (SQL Server-Konfigurations-Manager) | Microsoft Docs"
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
  - "SQL Server, beenden"
  - "SQL Server, automatisches Starten"
  - "Deaktivieren des automatischen Startens"
  - "Beenden von SQL Server"
  - "Verhindern des automatischen Startens [SQL Server]"
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Verhindern des automatischen Starts einer Instanz von SQL Server (SQL Server-Konfigurations-Manager)
  In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des SQL Server-Konfigurations-Managers verhindern können, dass eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] automatisch gestartet wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist normalerweise für den automatischen Start konfiguriert. Sie können diese Einstellung ändern, indem Sie den Startmodus für die Instanz auf manuell festlegen.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### So verhindern Sie das automatische Starten einer Instanz von SQL Server  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers auf der **Startseite** Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager im Charm **Suchen** unter **Apps** zu öffnen, geben Sie **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im SQL Server-Konfigurations-Manager **Dienste**, und klicken Sie dann auf **SQL Server**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **MSSQLServer**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Legen Sie im Dialogfeld **SQL Server \<***Instanzname***> Eigenschaften** im Feld **Eigenschaften** den Wert für **Startmodus** auf **Manuell** fest.  
  
5.  Klicken Sie auf **OK**, um das Dialogfeld **SQL Server \<***Instanzname***> Eigenschaften** zu schließen, und schließen Sie dann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager.  
  
## Siehe auch  
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  