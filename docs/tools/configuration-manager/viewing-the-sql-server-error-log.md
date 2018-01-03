---
title: Anzeigen von SQL Server-Fehlerprotokoll | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0d1514d7d7be760e3d10a831794210c36eddfe25
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="viewing-the-sql-server-error-log"></a>Anzeigen des SQL Server-Fehlerprotokolls
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Anzeigen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fehlerprotokoll, um sicherzustellen, dass Prozesse erfolgreich (z. B. sicherungs-und Wiederherstellungsvorgänge, Batchbefehle oder andere Skripts und Prozesse) abgeschlossen wurden. Dies ist hilfreich, um aktuelle oder potenzielle Problembereiche zu ermitteln, einschließlich automatischer Wiederherstellungsmeldungen (insbesondere, wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angehalten und neu gestartet wurde), Kernelmeldungen oder anderer Fehlermeldungen auf Serverebene.  
  
 Um das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll anzuzeigen, können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einen beliebigen Text-Editor verwenden. Weitere Informationen zum Anzeigen des Fehlerprotokolls finden Sie unter [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md). Standardmäßig befindet sich das Fehlerprotokoll unter `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` und `ERRORLOG.`*n* .  
  
 Es wird immer dann ein neues Fehlerprotokoll erstellt, wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird, obwohl die gespeicherte Systemprozedur [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) zum Durchlaufen der Fehlerprotokolldateien verwendet werden kann, ohne dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu gestartet werden muss. In der Regel behält [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sicherungen der letzten sechs Protokolle bei. Dabei erhält die letzte Sicherung die Erweiterung .1, die zweitletzte Sicherung die Erweiterung .2 usw. Das aktuelle Fehlerprotokoll hat keine Erweiterung.  
  
 Beachten Sie, dass Sie auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll zu Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzeigen können, die offline sind oder nicht gestartet werden können. Weitere Informationen finden Sie unter [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md).  
  
  
