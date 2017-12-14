---
title: Anzeigen des SQL Server-Fehlerprotokolls (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7de82937a4bb622190da96b5668318304f641895
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Anzeigen des SQL Server-Fehlerprotokolls (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll enthält benutzerdefinierte Ereignisse und bestimmte Systemereignisse, die für die Problembehandlung nützlich sind. 

## <a name="view-the-logs"></a>Anzeigen der Protokolle

1. Wählen Sie in SQL Server Management Studio die Option **Objekt-Explorer** aus. Um den **Objekt-Explorer** zu öffnen, wählen Sie F8 aus. Alternativ klicken Sie im Hauptmenü auf **Ansicht**, und wählen Sie dann **Objekt-Explorer** aus:
    
    ![Object_Explorer](../../relational-databases/performance/media/object-explorer.png) 

2. Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von SQL Server her, und erweitern Sie dann diese Instanz.
  
3. Suchen und erweitern Sie den Abschnitt **Verwaltung** (unter der Voraussetzung, dass Sie über Berechtigungen zum Anzeigen verfügen).

4. Klicken Sie mit der rechten Maustaste auf **SQL Server-Protokolle**, wählen Sie erst **Ansicht** und anschließend **SQL Server-Protokoll** aus.

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. Der **Protokolldatei-Viewer** wird geöffnet, und es wird eine Liste der verfügbaren Protokolle angezeigt (dies kann einen Moment dauern).
  
  ## <a name="see-also"></a>Siehe auch
  Weitere Informationen finden Sie in dem nützlichen [MSSQLTips.com](https://www.mssqltips.com/)-Beitrag [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/) (Bestimmen des Speicherorts der SQL Server-Fehlerprotokolldatei).

