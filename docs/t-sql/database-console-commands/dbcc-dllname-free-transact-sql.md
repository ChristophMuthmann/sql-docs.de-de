---
title: DBCC-DLL-Namen (FREE) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs: TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
caps.latest.revision: "27"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ad6b900d45ef1c87c0aca0d961685c68a72a33d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Entfernt die angegebene erweiterte gespeicherte Prozedur DLL aus dem Arbeitsspeicher.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
 \<*DLL-Name*>  
 Der Name der DLL, die aus dem Arbeitsspeicher gelöscht werden soll.  
  
 WITH NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Hinweise
Wenn eine erweiterte gespeicherte Prozedur ausgeführt wird, die DLL bleibt so lange von der Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bis der Server heruntergefahren wird. Diese Anweisung kann eine DLL aus dem Arbeitsspeicher entladen werden, ohne herunterzufahren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Zum Anzeigen der DLL-Dateien, die momentan vom geladen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], führen Sie **Sp_helpextendedproc**
  
## <a name="result-sets"></a>Resultsets  
Wenn eine gültige DLL angegeben wird, gibt DBCC *dllname* (FREE) Folgendes zurück:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="examples"></a>Beispiele  
Im folgende Beispiel wird vorausgesetzt, dass `xp_sample` als xp_sample.dll implementiert ist und ausgeführt wurde. DBCC \< *DLL-Namen*> (FREE) entladen, die die Datei xp_sample.dll zugeordneten der `xp_sample` erweiterte Prozedur.
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Ausführungsmerkmale erweiterter gespeicherter Prozeduren](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[Entfernen der DLL einer erweiterten gespeicherten Prozedur aus dem Arbeitsspeicher](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
