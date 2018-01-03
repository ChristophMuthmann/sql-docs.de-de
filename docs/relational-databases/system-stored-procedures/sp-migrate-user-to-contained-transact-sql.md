---
title: Sp_migrate_user_to_contained (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 366d2347118fa55a8541e7f84a268b173ae5b2e3
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Konvertiert einen Datenbankbenutzer, der mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen verknüpft ist, in den Benutzer einer enthaltenen Datenbank mit Kennwort. In einer eigenständigen Datenbank können Sie mit diesem Verfahren Abhängigkeiten für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernen, in der die Datenbank installiert ist. **Sp_migrate_user_to_contained** trennt den Benutzer aus der ursprünglichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldenamen, damit Einstellungen wie Kennwort und Standardsprache für die eigenständige Datenbank separat verwaltet werden können. **Sp_migrate_user_to_contained** kann verwendet werden, vor dem Wechsel von der eigenständigen Datenbank in eine andere Instanz von der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , mit dem aktuellen Abhängigkeiten zu beseitigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldungen-Instanz.  
  
 **Hinweis** diese Prozedur wird nur in einer eigenständigen Datenbank verwendet. Weitere Informationen finden Sie unter [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@username =** ] **N'***Benutzer***"**  
 Der Name eines Benutzers in der aktuellen eigenständigen Datenbank, der mit einem authentifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen verknüpft ist. Der Wert ist **Sysname**, hat den Standardwert **NULL**.  
  
 [ **@rename =** ] **N'***Copy_login_name***"** | **N'** *Keep_name***"**  
 Wenn ein Datenbankbenutzer auf Basis eines Anmeldenamens einen anderen Benutzernamen als den Anmeldenamen enthält, mithilfe von *Keep_name* den Datenbankbenutzernamen während der Migration beibehalten werden sollen. Verwendung *Copy_login_name* neue eigenständige Datenbankbenutzer mit dem Namen der Anmeldung, anstelle des Benutzers zu erstellen. Wenn der Benutzername eines Datenbankbenutzers dem Anmeldenamen entspricht, wird mit beiden Optionen der Benutzer der enthaltenen Datenbank erstellt, ohne den Namen zu ändern.  
  
 [ **@disablelogin =** ] **N'***Disable_login***"** | **N'** *Do_not_disable_login***"**  
 *Disable_login* deaktiviert die Anmeldung in der master-Datenbank. Um eine Verbindung herzustellen, wenn die Anmeldung deaktiviert ist, muss die Verbindung angeben, den Namen der eigenständigen Datenbank als die **Anfangskatalog** als Teil der Verbindungszeichenfolge.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_migrate_user_to_contained** Benutzer der eigenständigen Datenbank mit Kennwort, unabhängig von der Eigenschaften oder Berechtigungen der Anmeldung erstellt. Die Prozedur kann z. B. erfolgreich, wenn die Anmeldung deaktiviert ist oder wenn der Benutzer abgelehnt wird die **verbinden** Berechtigung für die Datenbank.  
  
 **Sp_migrate_user_to_contained** gelten folgende Einschränkungen.  
  
-   Der Benutzername darf nicht bereits in der Datenbank vorhanden sein.  
  
-   Integrierte Benutzer wie dbo und guest, können nicht konvertiert werden.  
  
-   Der Benutzer kann nicht angegeben werden, der **EXECUTE AS** -Klausel einer signierten gespeicherten Prozedur.  
  
-   Der Benutzer kann nicht Besitzer eine gespeicherte Prozedur, die enthält die **EXECUTE AS OWNER** Klausel.  
  
-   **Sp_migrate_user_to_contained** kann nicht in einer Systemdatenbank verwendet werden.  
  
## <a name="security"></a>Security  
 Achten Sie beim Migrieren von Benutzern darauf, dass nicht alle Administratoranmeldungen von der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht werden. Wenn alle Anmeldungen gelöscht werden, finden Sie unter [Herstellen einer Verbindung mit SQL Server beim System Systemadministratoren gesperrt sind](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Wenn die **"BUILTIN\Administrators"** Anmeldung vorhanden ist, können Administratoren durch Starten ihre Anwendung mit Verbinden der **als Administrator ausführen** Option.  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die **CONTROL SERVER** -Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-migrating-a-single-user"></a>A. Migrieren eines einzelnen Benutzers  
 Im folgenden Beispiel wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename `Barry` in den Benutzer einer enthaltenen Datenbankbenutzer mit Kennwort migriert. Der Benutzername wird im Beispiel nicht geändert, und der Anmeldename ist weiterhin aktiviert.  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. Migrieren aller Datenbankbenutzer mit Anmeldenamen zu Benutzern in eigenständigen Datenbanken ohne Anmeldenamen  
 Im folgenden Beispiel werden alle Benutzer, die auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen basieren, in Benutzer enthaltener Datenbanken mit Kennwörtern migriert. Nicht berücksichtigt werden Anmeldungen, die nicht aktiviert sind. Das Beispiel muss in der enthaltenen Datenbank ausgeführt werden.  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md)  
  
  
