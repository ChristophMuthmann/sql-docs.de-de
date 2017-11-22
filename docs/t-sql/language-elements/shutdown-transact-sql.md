---
title: SHUTDOWN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs: TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 10a6b2c5bf093eaee3eacf183f98ecb644d2fc68
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Beendet sofort die SQL Server.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>Argumente  
 WITH NOWAIT  
 Optional. Schließt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ohne Prüfpunkte in allen Datenbanken durchzuführen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird beendet, nachdem versucht wurde, alle Benutzerprozesse zu beenden. Nach einem Neustart des Servers wird ein Rollbackvorgang für alle nicht abgeschlossenen Transaktionen ausgeführt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die WITHNOWAIT-Option verwendet wird, SHUTDOWN heruntergefahren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch:  
  
1.  Deaktivieren von Anmeldenamen (außer für Mitglieder der der **Sysadmin** und **Serveradmin** festen Serverrollen).  
  
    > [!NOTE]  
    >  Führen Sie zum Anzeigen einer Liste aller aktuellen Benutzer **Sp_who**.  
  
2.  Warten, bis die zurzeit ausgeführten Transact-SQL-Anweisungen oder gespeicherten Prozeduren beendet sind. Führen Sie zum Anzeigen einer Liste aller aktiven Prozesse und Sperren **Sp_who** und **Sp_lock**zugeordnet.  
  
3.  Einfügen eines Prüfpunktes in jede Datenbank.  
  
 Verwenden der SHUTDOWN-Anweisung wird die Menge minimiert automatische Wiederherstellung Aufwand ist erforderlich, wenn Mitglieder der **Sysadmin** feste Rolle Serverneustart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Mithilfe anderer Tools und Methoden kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ebenfalls beendet werden. Von allen Tools und Methoden wird ein Prüfpunkt in allen Datenbanken ausgegeben. Sie können Daten, für die ein Commit ausgeführt wurde, folgendermaßen aus dem Datencache leeren und den Server anhalten:  
  
-   Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers.  
  
-   Durch Ausführen von **net Stop Mssqlserver** über eine Eingabeaufforderung für eine Standardinstanz oder durch Ausführen **net Stop Mssql$***Instancename* über eine Eingabeaufforderung für eine benannte Instanz.  
  
-   Mithilfe der Dienste in der Systemsteuerung.  
  
 Wenn **sqlservr.exe** wurde gestartet, von der Befehlszeile aus, drücken STRG + C heruntergefahren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Durch Drücken von STRG+C wird jedoch kein Prüfpunkt eingefügt.  
  
> [!NOTE]  
>  Verwenden eine dieser Methoden zum Beenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sendet die `SERVICE_CONTROL_STOP` -Meldung an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der SHUTDOWN-Berechtigungen zugewiesen sind die **Sysadmin** und **Serveradmin** festen Serverrollen, und sie sind nicht übertragbar.  
  
## <a name="see-also"></a>Siehe auch  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [' sp_lock ' &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [Sp_who &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr (Anwendung)](../../tools/sqlservr-application.md)   
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
