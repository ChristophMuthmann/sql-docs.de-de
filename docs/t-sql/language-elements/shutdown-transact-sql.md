---
title: SHUTDOWN (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: df8ef0a3cfe0ac4adb6f45bddb0bef650fea6ff3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Beendet SQL Server sofort.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>Argumente  
 WITH NOWAIT  
 Optional. Schließt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ohne Prüfpunkte in allen Datenbanken durchzuführen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird beendet, nachdem versucht wurde, alle Benutzerprozesse zu beenden. Nach einem Neustart des Servers wird ein Rollbackvorgang für alle nicht abgeschlossenen Transaktionen ausgeführt.  
  
## <a name="remarks"></a>Remarks  
 Wenn die Option WITHNOWAIT nicht verwendet wird, wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch SHUTDOWN durch folgende Vorgehensweise heruntergefahren:  
  
1.  Deaktivieren von Anmeldenamen (außer für Mitglieder der festen Serverrollen **sysadmin** und **serveradmin**).  
  
    > [!NOTE]  
    >  Um eine Liste aller aktuellen Benutzer anzuzeigen, führen Sie **sp_who** aus.  
  
2.  Warten, bis die zurzeit ausgeführten Transact-SQL-Anweisungen oder gespeicherten Prozeduren beendet sind. Um eine Liste aller aktiven Prozesse und Sperren anzuzeigen, führen Sie entsprechend **sp_who** und **sp_lock** aus.  
  
3.  Einfügen eines Prüfpunktes in jede Datenbank.  
  
 Durch Verwenden der SHUTDOWN-Anweisung wird der Aufwand für die automatische Wiederherstellung auf ein Minimum reduziert. Dieser Aufwand ist erforderlich, wenn Mitglieder der festen Serverrolle **sysadmin** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu starten.  
  
 Mithilfe anderer Tools und Methoden kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ebenfalls beendet werden. Von allen Tools und Methoden wird ein Prüfpunkt in allen Datenbanken ausgegeben. Sie können Daten, für die ein Commit ausgeführt wurde, folgendermaßen aus dem Datencache leeren und den Server anhalten:  
  
-   Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers.  
  
-   Durch Ausführen von **net stop mssqlserver** über eine Eingabeaufforderung für eine Standardinstanz oder durch Ausführen von **net stop mssql$***instancename* über eine Eingabeaufforderung für eine benannte Instanz.  
  
-   Mithilfe der Dienste in der Systemsteuerung.  
  
 Wenn **sqlservr.exe** von der Eingabeaufforderung aus gestartet wurde, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch Drücken von STRG+C heruntergefahren werden. Durch Drücken von STRG+C wird jedoch kein Prüfpunkt eingefügt.  
  
> [!NOTE]  
>  Wenn Sie eine dieser Methoden zum Anhalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, wird die `SERVICE_CONTROL_STOP`-Meldung an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Die SHUTDOWN-Berechtigungen werden Mitgliedern der festen Serverrollen **sysadmin** und **serveradmin** zugewiesen. Sie sind nicht übertragbar.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr (Anwendung)](../../tools/sqlservr-application.md)   
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
