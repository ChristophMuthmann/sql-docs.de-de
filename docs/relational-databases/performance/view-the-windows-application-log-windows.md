---
title: "Anzeigen des Anwendungsprotokolls von Windows (Windows) | Microsoft Docs"
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
  - "Anzeigen von Protokollen"
  - "Anwendungsprotokolle [SQL Server]"
  - "Protokolle [SQL Server], Anwendung"
  - "Überwachen des Anwendungsprotokolls von Windows NT [SQL Server]"
  - "Windows NT-Anwendungsprotokolle [SQL Server]"
  - "Einblenden von Protokollen"
  - "Überwachen [SQL Server], Ereignisse"
  - "Protokolle [SQL Server], anzeigen"
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Anzeigen des Anwendungsprotokolls von Windows (Windows)
  Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verwendung des Windows-Anwendungsprotokolls konfiguriert ist, werden bei jeder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sitzung neue Ereignisse in das Protokoll geschrieben. Im Gegensatz zum Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird beim Starten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz nicht jedes Mal ein neues Anwendungsprotokoll erstellt.  
  
### So zeigen Sie das Anwendungsprotokoll von Windows an  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**und anschließend auf **Verwaltung**, und klicken Sie dann auf **Ereignisanzeige**.  
  
2.  Klicken Sie in der Ereignisanzeige auf **Anwendung**.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ereignisse werden in der **Source**-Spalte durch den Eintrag **MSSQLSERVER** identifiziert (benannte Instanzen werden durch **MSSQL$***<Instanzname>* identifiziert). Die Ereignisse des SQL Server-Agents werden durch den Eintrag SQLSERVERAGENT identifiziert (bei benannten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Ereignisse durch **SQLAgent$**\<*Instanzname*> identifiziert). Die Ereignisse des Microsoft Search-Dienstes werden durch den Eintrag **Microsoft Search**identifiziert.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Ereignisanzeige**, klicken Sie anschließend auf **Verbindung mit anderem Computer herstellen**, und nehmen Sie im Dialogfeld **Computer auswählen** die entsprechenden Einstellungen vor, um das Protokoll eines anderen Computers anzuzeigen.  
  
5.  Wenn Sie wahlweise nur die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ereignisse anzeigen möchten, klicken Sie im Menü **Ansicht** auf **Filter**, und wählen Sie in der Liste **Ereignisquelle** den Eintrag **MSSQLSERVER**aus. Um nur die Ereignisse des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents anzuzeigen, wählen Sie stattdessen in der Liste **Ereignisquelle** den Eintrag **SQLSERVERAGENT** aus.  
  
6.  Um weitere Informationen zu einem bestimmten Ereignis anzuzeigen, doppelklicken Sie auf dieses Ereignis.  
  
## Siehe auch  
 [Anzeigen des SQL Server-Fehlerprotokolls &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  