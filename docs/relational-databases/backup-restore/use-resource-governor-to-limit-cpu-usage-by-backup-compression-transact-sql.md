---
title: "Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle (Transact-SQL) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a5cd10ed1fc52431898748772038883b3bc4851
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Standardmäßig steigt die CPU-Nutzung durch die Sicherung mit Komprimierung erheblich, und die bei der Komprimierung zusätzlich benötigten CPU-Ressourcen können sich negativ auf gleichzeitig ausgeführte Vorgänge auswirken. Daher ist es u.U. sinnvoll, in einer Sitzung, bei der die CPU-Nutzung durch den[Resource Governor](../../relational-databases/resource-governor/resource-governor.md) eingeschränkt ist, eine komprimierte Sicherung mit niedriger Priorität zu erstellen, wenn CPU-Konflikte bestehen. In diesem Thema wird ein Szenario dargestellt, in dem die Sitzungen eines bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzers klassifiziert werden, indem diese einer Arbeitsauslastungsgruppe der Ressourcenkontrolle zugeordnet werden, die die CPU-Nutzung in solchen Fällen einschränkt.  
  
> [!IMPORTANT]  
>  In einem Szenario für Ressourcenkontrolle kann die Klassifizierung der Sitzungen auf einem Benutzernamen, einem Anwendungsnamen oder einem beliebigen anderen Element basieren, anhand dessen Verbindungen voneinander unterschieden werden können. Weitere Informationen finden Sie unter [Resource Governor Classifier Function](../../relational-databases/resource-governor/resource-governor-classifier-function.md) und [Resource Governor Workload Group](../../relational-databases/resource-governor/resource-governor-workload-group.md).  
  
##  <a name="Top"></a> Dieses Thema enthält die folgenden Szenarien, die nacheinander dargestellt werden:  
  
1.  [Einrichten einer Anmeldung und eines Benutzers für Vorgänge mit niedriger Priorität](#setup_login_and_user)  
  
2.  [Konfigurieren der Ressourcenkontrolle zum Einschränken der CPU-Nutzung](#configure_RG)  
  
3.  [Überprüfen der Klassifizierung der aktuellen Sitzung (Transact-SQL)](#verifying)  
  
4.  [Komprimieren von Sicherungen in einer Sitzung mit CPU-Grenzwert](#creating_compressed_backup)  
  
##  <a name="setup_login_and_user"></a> Einrichten einer Anmeldung und eines Benutzers für Vorgänge mit niedriger Priorität  
 Für das Szenario in diesem Thema sind eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung und ein zugehöriger Benutzer für Vorgänge mit niedriger Priorität erforderlich. Mithilfe des Benutzernamens werden die in der Anmeldung ausgeführten Sitzungen klassifiziert und an eine Arbeitsauslastungsgruppe der Ressourcenkontrolle weitergeleitet, die die CPU-Nutzung einschränkt.  
  
 Im folgenden Verfahren werden die Schritte zum Einrichten einer Anmeldung und eines Benutzers zu diesem Zweck beschrieben. Darauf folgt das [!INCLUDE[tsql](../../includes/tsql-md.md)] -Beispiel "Beispiel A: Einrichten einer Anmeldung und eines Benutzers (Transact-SQL)".  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>So richten Sie eine Anmeldung und einen Datenbankbenutzer zum Klassifizieren von Sitzungen ein  
  
1.  Erstellen Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung zum Erstellen komprimierter Sicherungen mit niedriger Priorität.  
  
     **So erstellen Sie eine Anmeldung**  
  
    -   [Erstellen eines Anmeldenamens](../../relational-databases/security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
2.  Sie können dieser Anmeldung die VIEW SERVER STATE-Berechtigung erteilen.  
  
    -   [GRANT (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)  
  
     Weitere Informationen finden Sie unter [GRANT (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md).  
  
3.  Erstellen Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer für diese Anmeldung.  
  
     **So erstellen Sie einen Benutzer**  
  
    -   [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
4.  Fügen Sie den Benutzer der Datenbankrolle db_backupoperator der Datenbank hinzu, damit für die Anmeldung Sitzungen möglich sind und der Benutzer eine Datenbank sichern kann. Wiederholen Sie diesen Schritt für alle Datenbanken, die gesichert werden sollen. Sie können den Benutzer auch anderen festen Datenbankrollen hinzufügen.  
  
     **So fügen Sie einen Benutzer einer festen Datenbankrolle hinzu**  
  
    -   [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
     Weitere Informationen finden Sie unter [GRANT (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md).  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>Beispiel A: Einrichten einer Anmeldung und eines Benutzers (Transact-SQL)  
 Das folgende Beispiel ist nur dann relevant, wenn Sie eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung und einen zugehörigen Benutzer für Sicherungen mit niedriger Priorität erstellen möchten. Alternativ können Sie eine vorhandene Anmeldung und einen vorhandenen Benutzer verwenden, wenn entsprechende vorhanden sind.  
  
> [!IMPORTANT]  
>  Im folgenden Beispiel werden eine Beispielanmeldung und ein Beispielbenutzername, *domain_name*`\MAX_CPU`, verwendet. Ersetzen Sie diese durch die Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung und des zugehörigen Benutzers, die beim Erstellen komprimierter Sicherungen mit niedriger Priorität verwendet werden sollen.  
  
 In diesem Beispiel wird eine Anmeldung für das Windows-Konto *domain_name*`\MAX_CPU` erstellt, und dieser wird anschließend die VIEW SERVER STATE-Berechtigung erteilt. Mit dieser Berechtigung können Sie die Klassifizierung der Sitzungen der Anmeldung durch die Ressourcenkontrolle überprüfen. Im Beispiel wird anschließend ein Benutzer für *domain_name*`\MAX_CPU` erstellt, und dieser wird der festen Datenbankrolle db_backupoperator für die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Beispieldatenbank hinzugefügt. Dieser Benutzername wird von der Klassifizierungsfunktion der Ressourcenkontrolle verwendet.  
  
```sql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;Nach oben&#93;](#Top)  
  
##  <a name="configure_RG"></a> Konfigurieren der Ressourcenkontrolle zum Einschränken der CPU-Nutzung  
  
> [!NOTE]  
>  Stellen Sie sicher, dass die Ressourcenkontrolle aktiviert ist. Weitere Informationen finden Sie unter [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md).  
  
 In diesem Szenario für Ressourcenkontrolle besteht die Konfiguration aus den folgenden grundlegenden Schritten:  
  
1.  Erstellen und konfigurieren Sie einen Ressourcenpool für die Ressourcenkontrolle zum Einschränken der maximalen durchschnittlichen CPU-Bandbreite für alle Anforderungen im Ressourcenpool, wenn CPU-Konflikte bestehen.  
  
2.  Erstellen und konfigurieren Sie eine Arbeitsauslastungsgruppe der Ressourcenkontrolle, die diesen Pool verwendet.  
  
3.  Erstellen Sie eine *Klassifizierungsfunktion*. Dabei handelt es sich um eine benutzerdefinierte Funktion (User-Defined Function, UDF), deren Rückgabewerte von Resource Governor verwendet wird, um Sitzungen zu klassifizieren, sodass diese an die entsprechende Arbeitsauslastungsgruppe weitergeleitet werden.  
  
4.  Registrieren Sie die Klassifizierungsfunktion bei der Ressourcenkontrolle.  
  
5.  Wenden Sie die Änderungen auf die Konfiguration im Arbeitsspeicher der Ressourcenkontrolle an.  
  
> [!NOTE]  
>  Informationen zu Ressourcenpools der von Resource Governor, Arbeitsauslastungsgruppen und Klassifizierung finden Sie unter [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md).  
  
 Die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen für diese Schritte werden unter "So konfigurieren Sie die Ressourcenkontrolle zum Einschränken der CPU-Nutzung" beschrieben, worauf ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Beispiel für die Vorgehensweise folgt.  
  
 **So konfigurieren Sie die Ressourcenkontrolle (SQL Server Management Studio)**  
  
-   [Konfigurieren der Ressourcenkontrolle mit einer Vorlage](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [Erstellen eines Ressourcenpools](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [Erstellen einer Arbeitsauslastungsgruppe](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>So konfigurieren Sie die Ressourcenkontrolle zum Einschränken der CPU-Nutzung (Transact-SQL)  
  
1.  Geben Sie eine [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) -Anweisung aus, um einen Ressourcenpool zu erstellen. Im Beispiel für diese Vorgehensweise wird die folgende Syntax verwendet:  
  
     *CREATE RESOURCE POOL pool_name* WITH ( MAX_CPU_PERCENT = *value* );  
  
     *Value* ist ein ganzzahliger Wert zwischen 1 und 100, der den Prozentsatz der maximalen durchschnittlichen CPU-Bandbreite angibt. Der korrekte Wert hängt von der Umgebung ab. Zur Veranschaulichung wird im Beispiel in diesem Thema der Wert 20 % (MAX_CPU_PERCENT = 20) verwendet.  
  
2.  Geben Sie eine [CREATE WORKLOAD GROUP](../../t-sql/statements/create-workload-group-transact-sql.md) -Anweisung aus, um eine Arbeitsauslastungsgruppe für Vorgänge mit niedriger Priorität zu erstellen, deren CPU-Nutzung kontrolliert werden soll. Im Beispiel für diese Vorgehensweise wird die folgende Syntax verwendet:  
  
     CREATE WORKLOAD GROUP *group_name* USING *pool_name*;  
  
3.  Geben Sie eine [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) -Anweisung aus, um eine Klassifizierungsfunktion zu erstellen, die die im vorherigen Schritt erstellte Arbeitsauslastungsgruppe dem Benutzer mit der Anmeldung mit niedriger Priorität zuordnet. Im Beispiel für diese Vorgehensweise wird die folgende Syntax verwendet:  
  
     CREATE FUNCTION [*schema_name*.]*function_name*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DEKLARIEREN SIE @workload_group_name ALS *sysname*  
  
     IF (SUSER_NAME() = '*user_of_low_priority_login*')  
  
     SET @workload_group_name = '*workload_group_name*'  
  
     RÜCKGABEWERT @workload_group_name  
  
     END  
  
     Informationen zu den Komponenten dieser CREATE FUNCTION-Anweisung finden Sie unter:  
  
    -   [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
    -   [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME ist nur eine von mehreren Systemfunktionen, die in einer Klassifizierungsfunktion verwendet werden können. Weitere Informationen finden Sie unter [Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md).  
  
    -   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
4.  Geben Sie eine [ALTER RESOURCE GOVERNOR](../../t-sql/statements/alter-resource-governor-transact-sql.md) -Anweisung aus, um die Klassifizierungsfunktion bei der Ressourcenkontrolle zu registrieren. Im Beispiel für diese Vorgehensweise wird die folgende Syntax verwendet:  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *schema_name*.*function_name*);  
  
5.  Geben Sie eine weitere ALTER RESOURCE GOVERNOR-Anweisung aus, um die Änderungen folgendermaßen auf die Konfiguration im Arbeitsspeicher der Ressourcenkontrolle anzuwenden:  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>Beispiel B: Konfigurieren der Ressourcenkontrolle (Transact-SQL)  
 Im folgenden Beispiel werden die folgenden Schritte in einer einzelnen Transaktion ausgeführt:  
  
1.  Der `pMAX_CPU_PERCENT_20` -Ressourcenpool wird erstellt.  
  
2.  Die `gMAX_CPU_PERCENT_20` -Arbeitsauslastungsgruppe wird erstellt.  
  
3.  Die `rgclassifier_MAX_CPU()` -Klassifizierungsfunktion, die den im vorherigen Beispiel erstellten Benutzernamen verwendet, wird erstellt.  
  
4.  Die Klassifizierungsfunktion wird bei der Ressourcenkontrolle registriert.  
  
 Nachdem für die Transaktion ein Commit ausgeführt wurde, werden im Beispiel alle Konfigurationsänderungen angewendet, die in der ALTER WORKLOAD GROUP-Anweisung oder der ALTER RESOURCE POOL-Anweisung angefordert wurden.  
  
> [!IMPORTANT]  
>  Im folgenden Beispiel wird der Benutzername des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Beispielbenutzers *domain_name*`\MAX_CPU`verwendet, der unter "Beispiel A: Einrichten einer Anmeldung und eines Benutzers (Transact-SQL)" erstellt wurde. Ersetzen Sie diesen durch den Namen des Benutzers der Anmeldung, die zum Erstellen komprimierter Sicherungen mit niedriger Priorität verwendet werden soll.  
  
```sql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;Nach oben&#93;](#Top)  
  
##  <a name="verifying"></a> Überprüfen der Klassifizierung der aktuellen Sitzung (Transact-SQL)  
 Melden Sie sich optional als der Benutzer an, den Sie in der Klassifizierungsfunktion angegeben haben, und überprüfen Sie die Sitzungsklassifizierung durch Ausgeben der folgenden [SELECT](../../t-sql/queries/select-transact-sql.md) -Anweisung im Objekt-Explorer:  
  
```sql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 Im Ergebnisbereich sollte in der Spalte **Name** mindestens eine Sitzung für den Namen der Arbeitsauslastungsgruppe aufgeführt werden, den Sie in der Klassifizierungsfunktion angegeben haben.  
  
> [!NOTE]  
>  Informationen zu den dynamischen Verwaltungssichten, die von dieser SELECT-Anweisung aufgerufen werden, finden Sie unter [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) und [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 [&#91;Nach oben&#93;](#Top)  
  
##  <a name="creating_compressed_backup"></a> Komprimieren von Sicherungen in einer Sitzung mit CPU-Grenzwert  
 Melden Sie sich zum Erstellen einer komprimierten Sicherung in einer Sitzung mit maximalem CPU-Grenzwert als der Benutzer an, der in der Klassifizierungsfunktion angegeben ist. Geben Sie im Sicherungsbefehl entweder WITH COMPRESSION ([!INCLUDE[tsql](../../includes/tsql-md.md)]) an, oder wählen Sie **Sicherung komprimieren** ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) aus. Informationen zum Erstellen einer komprimierten Datenbanksicherung finden Sie unter [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>Beispiel C: Erstellen einer komprimierten Sicherung (Transact-SQL)  
 Im folgenden [BACKUP](../../t-sql/statements/backup-transact-sql.md) -Beispiel wird eine komprimierte, vollständige Sicherung der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank in der neu formatierten Sicherungsdatei `Z:\SQLServerBackups\AdvWorksData.bak`erstellt.  
  
```sql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;Nach oben&#93;](#Top)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
