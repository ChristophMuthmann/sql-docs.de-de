---
title: Sp_create_removable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7b5a66828c1ee49734e720137d3a0ededc0098e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spcreateremovable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Datenbank für austauschbare Medien. Erstellt drei oder mehr Dateien (eine für die Systemkatalogtabellen, eine für das Transaktionsprotokoll und eine oder mehrere für die Datentabellen) und platziert die Datenbank in diesen Dateien.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Wir empfehlen die Verwendung [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@dbname=** ] **'***dbname***'**  
 Der Name der Datenbank, die zur Verwendung auf austauschbaren Medien erstellt werden soll. *Dbname* ist **Sysname**.  
  
 [ **@syslogical=** ] **'***syslogical***'**  
 Der logische Name der Datei, die die Systemkatalogtabellen enthält. *Syslogical* ist **Sysname**.  
  
 [ **@sysphysical=** ] **'***sysphysical***'**  
 Der physische Name (einschließlich vollständiger Pfadangabe) der Datei, die die Datentabellen enthält. Enthält einen vollqualifizierten Pfad der Datei, die die Systemkatalogtabellen enthält. *Sysphysical* ist **nvarchar(260)**.  
  
 [ **@syssize=** ] *syssize*  
 Die in MB angegebene Größe der Datei, die die Systemkatalogtabellen enthält. *Syssize* ist **Int**. Die minimale *Syssize* ist 1.  
  
 [ **@loglogical=** ] **'***loglogical***'**  
 Der logische Name der Datei, die das Transaktionsprotokoll enthält. *Loglogical* ist **Sysname**.  
  
 [ **@logphysical=** ] **'***logphysical***'**  
 Der physische Name (einschließlich vollständiger Pfadangabe) der Datei, die die Datentabellen enthält. Enthält einen vollqualifizierten Pfad der Datei, die die Transaktionsprotokolltabellen enthält. *Logphysical* ist **nvarchar(260)**.  
  
 [ **@logsize=** ] *logsize*  
 Die in MB angegebene Größe der Datei, die das Transaktionsprotokoll enthält. *Logsize* ist **Int**. Die minimale *Logsize* ist 1.  
  
 [ **@datalogical1=** ] **'***datalogical***'**  
 Der logische Name der Datei, die die Datentabellen enthält. *Datalogical* ist **Sysname**.  
  
 Die Anzahl von Datendateien muss zwischen 1 und 16 liegen. In der Regel wird mehr als eine Datendatei erstellt, wenn zu erwarten ist, dass die Datenbank umfangreich wird und auf mehrere Datenträger verteilt werden muss.  
  
 [ **@dataphysical1=** ] **'***dataphysical***'**  
 Der physische Name (einschließlich vollständiger Pfadangabe) der Datei, die die Datentabellen enthält. Enthält einen vollqualifizierten Pfad der Datei, die die Datentabellen enthält. *Dataphysical* ist **nvarchar(260)**.  
  
 [ **@datasize1=** ] **'***datasize***'**  
 Die in MB angegebene Größe der Datei, die die Datentabellen enthält. *Datasize* ist **Int**. Die minimale *Datasize* ist 1.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie diese gespeicherte Prozedur, wenn Sie eine Kopie einer Datenbank auf austauschbaren Medien erstellen, wie z. B. auf CD, und die Datenbank an andere Benutzer verteilen möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung CREATE DATABASE, CREATE ANY DATABASE oder ALTER ANY DATABASE.  
  
 Zur Steuerung der Datenträgernutzung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Berechtigung zum Erstellen von Datenbanken in der Regel auf einige wenige Anmeldekonten beschränkt.  
  
### <a name="permissions-on-data-and-log-files"></a>Berechtigungen für Daten und Protokolldateien  
 Bei der Durchführung bestimmter Vorgänge an einer Datenbank werden die entsprechenden Berechtigungen für ihre Daten und Protokolldateien festgelegt. Durch die Berechtigungen wird verhindert, dass die Dateien versehentlich manipuliert werden, wenn sie sich in einem Verzeichnis mit offenen Berechtigungen befinden.  
  
|Vorgang auf Datenbank|Berechtigungen, die für die Dateien festgelegt sind|  
|---------------------------|------------------------------|  
|Ändern, um eine neue Datei hinzuzufügen|Erstellt|  
|Gesichert|Angefügt|  
|Wiederherstellen|Getrennt|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Daten und Protokolldateien fest führt Berechtigungen Datei.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die `inventory`-Datenbank als austauschbare Datenbank erstellt.  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
