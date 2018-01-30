---
title: Anzeigen des Anwendungsprotokolls von Windows (Windows) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
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
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 206304441aa399e25c6f63c502e4ebfe98972829
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="view-the-windows-application-log-windows-10"></a>Anzeigen des Anwendungsprotokolls von Windows (Windows 10)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verwendung des Windows-Anwendungsprotokolls konfiguriert ist, werden bei jeder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sitzung neue Ereignisse in das Protokoll geschrieben. Im Gegensatz zum Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird beim Starten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz nicht jedes Mal ein neues Anwendungsprotokoll erstellt.  
  
## <a name="view-the-windows-application-log"></a>Anzeigen des Anwendungsprotokolls von Windows  
  
1. Geben Sie in der **Suchleiste** **Ereignisanzeige** ein, und wählen Sie anschließend die Desktop-App **Ereignisanzeige** aus.
  
2. Öffnen Sie in der **Ereignisanzeige** das **Anwendungs- und Dienstprotokoll**.

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ereignisse werden in der Spalte **Source** durch den Eintrag **MSSQLSERVER** identifiziert (benannte Instanzen werden durch **MSSQL$***<Instanzname>* identifiziert). Die Ereignisse des SQL Server-Agents werden durch den Eintrag SQLSERVERAGENT identifiziert (bei benannten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Ereignisse durch **SQLAgent$**\<*Instanzname*> identifiziert). Die Ereignisse des Microsoft Search-Dienstes werden durch den Eintrag **Microsoft Search**identifiziert.  
  
4. Um das Protokoll eines anderen Computers anzuzeigen, klicken Sie mit der rechten Maustaste auf **Ereignisanzeige (lokal)**. Wählen Sie **Verbindung mit anderem Computer herstellen** aus, und füllen Sie die Felder aus, um die Bearbeitung des Dialogfelds **Computer auswählen** abzuschließen.  
  
5. Optional, zur ausschließlichen Anzeige von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ereignissen, wählen Sie im Menü **Ansicht** die Option **Filter** aus. Wählen Sie in der **Ereignisquelle**-Liste **MSSQLSERVER** aus. Um nur die Ereignisse des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents anzuzeigen, wählen Sie stattdessen in der Liste **Ereignisquelle** den Eintrag **SQLSERVERAGENT** aus.  
  
6. Um weitere Informationen zu einem bestimmten Ereignis anzuzeigen, doppelklicken Sie auf dieses Ereignis.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen des SQL Server-Fehlerprotokolls &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
