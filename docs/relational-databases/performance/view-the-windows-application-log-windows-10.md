---
title: Anzeigen des Anwendungsprotokolls von Windows (Windows) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 03060bdd05acbec76f4be69ffd8b8f05b54e59bd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-the-windows-application-log-windows-10"></a>Anzeigen des Anwendungsprotokolls von Windows (Windows 10)
  Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verwendung des Windows-Anwendungsprotokolls konfiguriert ist, werden bei jeder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sitzung neue Ereignisse in das Protokoll geschrieben. Im Gegensatz zum Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird beim Starten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz nicht jedes Mal ein neues Anwendungsprotokoll erstellt.  
  
### <a name="view-the-windows-application-log"></a>Anzeigen des Anwendungsprotokolls von Windows  
  
1.  Geben Sie in der **Suchleiste** **Ereignisanzeige** ein, und wählen Sie anschließend die Desktopanwendung „Ereignisanzeige“ aus.
  
2.  Öffnen Sie in der Ereignisanzeige das **Anwendungs- und Dienstprotokoll**.    
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ereignisse werden in der **Source**-Spalte durch den Eintrag **MSSQLSERVER** identifiziert (benannte Instanzen werden durch **MSSQL$***<Instanzname>* identifiziert). Die Ereignisse des SQL Server-Agents werden durch den Eintrag SQLSERVERAGENT identifiziert (bei benannten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Ereignisse durch **SQLAgent$**\<*Instanzname*> identifiziert). Die Ereignisse des Microsoft Search-Dienstes werden durch den Eintrag **Microsoft Search**identifiziert.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Ereignisanzeige (Lokal)**, wählen Sie anschließend **Verbindung mit anderem Computer herstellen**, und nehmen Sie im Dialogfeld **Computer auswählen** die entsprechenden Einstellungen vor, um das Protokoll eines anderen Computers anzuzeigen.  
  
5.  Wenn Sie wahlweise nur die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ereignisse anzeigen möchten, klicken Sie im Menü **Ansicht** auf **Filter**, und wählen Sie in der Liste **Ereignisquelle** den Eintrag **MSSQLSERVER**aus. Um nur die Ereignisse des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents anzuzeigen, wählen Sie stattdessen in der Liste **Ereignisquelle** den Eintrag **SQLSERVERAGENT** aus.  
  
6.  Um weitere Informationen zu einem bestimmten Ereignis anzuzeigen, doppelklicken Sie auf dieses Ereignis.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen des SQL Server-Fehlerprotokolls &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
