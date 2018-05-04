---
title: Sp_detach_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
caps.latest.revision: 86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7e36df67db10b423557384576f39a751531656e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Trennt eine zurzeit nicht verwendete Datenbank von einer Serverinstanz und führt optional vor dem Trennvorgang für alle Tabellen UPDATE STATISTICS aus.  
  
> [!IMPORTANT]  
>  Eine replizierte Datenbank kann nur getrennt werden, wenn sie nicht veröffentlicht ist. Weitere Informationen finden Sie im Abschnitt "Hinweise" weiter unten in diesem Thema.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@dbname =** ] **'***database_name***'**  
 Der Name der Datenbank, die getrennt werden soll. *Database_name* ist ein **Sysname** Wert hat den Standardwert NULL.  
  
 [ **@skipchecks =** ] **'***skipchecks***'**  
 Gibt an, ob UPDATE STATISTIC übersprungen oder ausgeführt werden soll. *"skipchecks"* ist ein **nvarchar(10)** Wert hat den Standardwert NULL. Um UPDATE STATISTICS auszulassen, geben Sie **"true"**. Um UPDATE STATISTICS explizit auszuführen, geben Sie **"false"**.  
  
 UPDATE STATISTICS wird standardmäßig ausgeführt, um Informationen zu den Daten in den Tabellen und Indizes zu aktualisieren. Das Ausführen von UPDATE STATISTICS ist nützlich für Datenbanken, die auf Nur-Lese-Medien verschoben werden sollen.  
  
 [  **@keepfulltextindexfile=** ] **"***Sp_detach_db***"**  
 Gibt an, dass die Volltextindex-Datei, die der zu trennenden Datenbank zugeordnet ist, während des Trennvorgangs der Datenbank nicht gelöscht wird. *Sp_detach_db* ist ein **nvarchar(10)** hat den Standardwert des **"true"**. Wenn *sp_detach_db* ist **"false"**, wird die Volltext-Indexdateien der Datenbank zugeordnet, und die Volltextindex-Metadaten werden gelöscht, es sei denn, die Datenbank schreibgeschützt ist. Wenn der Wert NULL oder **"true"**, volltextbezogene Metadaten beibehalten werden.  
  
> [!IMPORTANT]  
>  Die**@keepfulltextindexfile** Parameter wird in einer zukünftigen Version von entfernt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie diesen Parameter beim Entwickeln neuer Anwendungen nicht, und planen Sie so bald wie möglich das Ändern von Anwendungen, in denen er zurzeit verwendet wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Datenbank getrennt wird, werden alle Metadaten darin gelöscht. Wenn die Datenbank die Standarddatenbank für alle Anmeldekonten **master** wird ihre Standarddatenbank.  
  
> [!NOTE]  
>  Weitere Informationen dazu, wie die Standarddatenbank für alle Anmeldekonten anzeigen, finden Sie unter [Sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md). Wenn Sie die erforderlichen Berechtigungen verfügen, können Sie [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) eine Anmeldung eine neue Standarddatenbank zuweisen.  
  
## <a name="restrictions"></a>Einschränkungen  
 Eine Datenbank kann nicht getrennt werden, wenn Folgendes zutrifft:  
  
-   Die Datenbank ist zurzeit in Verwendung. Weitere Informationen finden Sie im Abschnitt "Erhalten exklusiven Zugriffs" weiter unten in diesem Thema.  
  
-   Wenn die Datenbank repliziert ist, wird sie veröffentlicht.  
  
     Bevor Sie die Datenbank trennen können, müssen Sie die Veröffentlichung deaktivieren, durch Ausführen von [Sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    >  Wenn Sie **sp_replicationdboption**nicht verwenden können, können Sie die Replikation durch Ausführen von [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)entfernen.  
  
-   Eine Datenbankmomentaufnahme ist in der Datenbank vorhanden.  
  
     Bevor Sie die Datenbank trennen können, müssen Sie alle Momentaufnahmen löschen. Weitere Informationen finden Sie unter [Löschen einer Datenbank-Momentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)angefügt werden.  
  
    > [!NOTE]  
    >  Eine Datenbankmomentaufnahme kann nicht getrennt oder angefügt werden.  
  
-   Die Datenbank ist gespiegelt.  
  
     Die Datenbank kann nur getrennt werden, wenn die Datenbank-Spiegelungssitzung beendet wird. Weitere Informationen finden Sie unter [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   Die Datenbank ist fehlerverdächtig.  
  
     Sie müssen für eine fehlerverdächtige Datenbank den Notfallmodus aktivieren, bevor Sie die Datenbank trennen können. Weitere Informationen zum Aktivieren des Notfallmodus für eine Datenbank finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Die Datenbank ist eine Systemdatenbank.  
  
## <a name="obtaining-exclusive-access"></a>Erhalten exklusiven Zugriffs  
 Das Trennen einer Datenbank erfordert den exklusiven Zugriff auf die Datenbank. Wenn die zu trennende Datenbank gerade verwendet wird, müssen Sie vor dem Trennen für die Datenbank den SINGLE_USER-Modus festlegen, um exklusiven Zugriff zu erhalten.  
  
 Beispielsweise die folgenden `ALTER DATABASE` -Anweisung erhalten exklusiven Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank nach allen aktuellen Benutzern aus der Datenbank trennen.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  Aktuelle erzwingen Benutzer aus der Datenbank sofort oder innerhalb einer angegebenen Anzahl von Sekunden auch verwenden, die Option ROLLBACK: ALTER DATABASE *Database_name* SET SINGLE_USER WITH ROLLBACK *Rollback_option*. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="reattaching-a-database"></a>Erneutes Anfügen einer Datenbank  
 Die getrennten Dateien bleiben gespeichert und können mithilfe von CREATE DATABASE (mit der FOR ATTACH- oder FOR ATTACH_REBUILD_LOG-Option) erneut angefügt werden. Die Dateien können auf einen anderen Server verschoben und dort angefügt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** feste Serverrolle oder die Mitgliedschaft in der **Db_owner** Rolle der Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel löst die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank mit *"skipchecks"* auf "true" festgelegt ist.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 Im folgenden Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank getrennt, wobei die Dateien für den Volltextindex und die Metadaten des Volltextindexes beibehalten werden. Durch diesen Befehl wird UPDATE STATISTICS ausgeführt. Dies entspricht dem Standardverhalten.  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Trennen einer Datenbank](../../relational-databases/databases/detach-a-database.md)  
  
  
