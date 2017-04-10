---
title: "Bestimmen, ob das Datenbankmodul installiert und gestartet wurde | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server, Bestimmung der Installation"
  - "Überprüfen der Datenbankmodulinstallation"
  - "Anzeigen der Datenbankmodulinstallation"
  - "Überprüfung der Datenbankmodulinstallation [SQL Server]"
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Bestimmen, ob das Datenbankmodul installiert und gestartet wurde
  Bei einer erfolgreichen Installation von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] werden Dateien auf dem Dateisystem installiert, Einträge in der Registrierung erstellt und verschiedene Tools installiert. In diesem Thema wird beschrieben, wie bestimmt wird, ob der [!INCLUDE[ssDE](../../includes/ssde-md.md)] installiert und in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers gestartet wird.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### Anzeigen und Starten des Datenbankmoduls mithilfe des SQL Server-Konfigurations-Managers  
  
1.  Klicken Sie auf **Start**, wählen Sie **Alle Programme**aus, zeigen Sie auf **Microsoft SQL Server**, auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
     Wenn diese Einträge im Menü **Start** nicht enthalten sind, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht korrekt installiert. Führen Sie das Setup aus, um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]zu installieren.  
  
2.  Klicken Sie im linken Bereich von **SQL Server-Konfigurations-Manager**auf **SQL Server 2005-Dienste**. Im rechten Bereich werden mehrere Dienste im Zusammenhang mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgelistet. Wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] installiert ist, wird der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Dienst als **SQL Server (MSSQLSERVER)** aufgelistet, wenn es sich um die Standardinstanz handelt, oder als **SQL Server (**\<*Instanzname*>**)**, wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] als benannte Instanz installiert wurde. Sofern der Instanzname nicht geändert wird, wird [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] als benannte Instanz mit dem Namen **SQLEXPRESS**installiert. Ein grünes Dreieckssymbol weist darauf hin, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgeführt wird. Ein rotes Dreieckssymbol gibt an, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] beendet wurde.  
  
3.  Um das [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu starten, klicken Sie im rechten Bereich mit der rechten Maustaste auf das [!INCLUDE[ssDE](../../includes/ssde-md.md)] und klicken dann auf **Start**.  
  
> [!NOTE]  
>  Während Setup kann der Benutzer ein Verzeichnis für die Installation der Programmdateien und der Datenbankdateien auswählen. Wenn der Benutzer den Standardspeicherort übernimmt, werden die Dateien unter [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] und C:\Programme\Microsoft SQL Server\MSSQL.*x* installiert, wobei *x* eine Zahl ist.  
  
  