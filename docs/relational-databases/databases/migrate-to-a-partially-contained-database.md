---
title: "Migrieren zu einer partiell eigenständigen Datenbank | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ce086529c97471ed6b2e80e5487aadab70be2c9
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="migrate-to-a-partially-contained-database"></a>Migrate to a Partially Contained Database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie die Umstellung auf das teilweise eigenständige Datenbankmodell vorbereitet wird. Anschließend werden die Migrationsschritte erläutert.  
  
 **In diesem Thema:**  
  
-   [Vorbereiten auf das Migrieren einer Datenbank](#prepare)  
  
-   [Aktivieren enthaltener Datenbanken](#enable)  
  
-   [Konvertieren einer Datenbank in eine teilweise eigenständige Datenbank](#convert)  
  
-   [Migrieren von Benutzern zu Benutzern eigenständiger Datenbanken](#users)  
  
##  <a name="prepare"></a> Vorbereiten auf das Migrieren einer Datenbank  
 Überprüfen Sie die folgenden Punkte, wenn Sie eine Datenbank zum teilweise eigenständigen Datenbankmodell migrieren möchten.  
  
-   Machen Sie sich mit dem teilweise eigenständigen Datenbankmodell vertraut. Weitere Informationen finden Sie unter [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
-   Sie müssen die Risiken verstehen, die mit teilweise eigenständigen Datenbanken verbunden sind. Weitere Informationen finden Sie unter [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
-   Enthaltene Datenbanken unterstützen weder die Replikation, noch das Aufzeichnen oder das Nachverfolgen von Änderungsdaten. Vergewissern Sie sich, dass diese Funktionen für die Datenbank nicht verwendet werden.  
  
-   Sehen Sie die Liste der Datenbankfunktionen ein, die für teilweise eigenständige Datenbanken geändert werden. Weitere Informationen finden Sie unter [Geänderte Funktionen &#40;Eigenständige Datenbank&#41;](../../relational-databases/databases/modified-features-contained-database.md).  
  
-   Fragen Sie [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) ab, um nicht enthaltene Objekte oder Funktionen in der Datenbank zu suchen. Weitere Informationen finden Sie weiter oben unter  
  
-   Überwachen Sie das **database_uncontained_usage** -XEvent, um festzustellen, ob nicht enthaltene Funktionen verwendet werden.  
  
##  <a name="enable"></a> Aktivieren enthaltener Datenbanken  
 Enthaltene Datenbanken müssen für die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz aktiviert sein, bevor sie erstellt werden können.  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>Aktivieren von enthaltenen Datenbanken mit Transact-SQL  
 Im folgenden Beispiel werden enthaltene Datenbanken für die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz aktiviert.  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>Aktivieren von enthaltenen Datenbanken mit Management Studio  
 Im folgenden Beispiel werden enthaltene Datenbanken für die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz aktiviert.  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Servernamen, und klicken Sie auf **Eigenschaften**.  
  
2.  Legen Sie auf der Seite **Erweitert** im Abschnitt **Kapselung** die Option **Enthaltene Datenbanken aktivieren** auf **True**fest.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> Konvertieren einer Datenbank in eine teilweise eigenständige Datenbank  
 Eine Datenbank wird in eine enthaltene Datenbank konvertiert, indem die **CONTAINMENT** -Option geändert wird.  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>Konvertieren einer Datenbank in eine teilweise eigenständige Datenbank mit Transact-SQL  
 Im folgenden Beispiel wird die Datenbank `Accounting` in eine teilweise eigenständige Datenbank konvertiert.  
  
```sql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>Konvertieren einer Datenbank in die teilweise eigenständige Datenbank mit Management Studio  
 Im folgenden Beispiel wird die Datenbank in eine teilweise eigenständige Datenbank konvertiert.  
  
1.  Erweitern Sie im Objekt-Explorer **Datenbanken**, klicken Sie mit der rechten Maustaste auf die zu konvertierende Datenbank, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Ändern Sie auf der Seite **Optionen** die Option **Kapselungstyp** in **Teilweise**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="users"></a> Migrieren von Benutzern zu Benutzern eigenständiger Datenbanken  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Contained Databases](../../relational-databases/databases/contained-databases.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)   
 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)  
  
  
