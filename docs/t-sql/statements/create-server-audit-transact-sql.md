---
title: CREATE SERVER AUDIT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f3d65d9a711a7fdd18c64d2ed064c28a415e5738
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Erstellt mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Überwachung ein Serverüberwachungsobjekt. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG }  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  
  
## <a name="arguments"></a>Argumente  
 TO { DATEI | ANWENDUNGSPROTOKOLL | SICHERHEITSPROTOKOLL }  
 Legt den Speicherort des Überwachungsziels fest. Die Optionen sind eine Binärdatei, das Windows-Anwendungsprotokoll oder das Windows-Sicherheitsprotokoll. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann nicht in das Windows-Sicherheitsprotokoll schreiben, ohne zusätzliche Einstellungen in Windows zu konfigurieren. Weitere Informationen finden Sie unter [Schreiben von SQL-Serverüberwachungsereignissen in das Sicherheitsprotokoll](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md).  
  
 FILEPATH ='*os_file_path*'  
 Der Pfad des Überwachungsprotokolls. Der Dateiname wird auf der Grundlage des Überwachungsnamens und des Überwachungs-GUID generiert.  
  
 MAXSIZE = { *max_size }*  
 Gibt die maximale Größe an, die die Überwachungsdatei annehmen kann. Der Wert von *max_size* muss eine ganze Zahl gefolgt von MB, GB, TB oder UNLIMITED sein. Die minimale Größe, die Sie für *max_size* angeben können, beträgt 2 MB, und die maximale Größe beträgt 2.147.483.647 TB. Wird UNLIMITED angegeben, kann die Größe der Datei so lange zunehmen, bis auf dem Datenträger kein Speicherplatz mehr verfügbar ist. (0 steht ebenfalls für UNLIMITED.) Die Angabe eines Werts kleiner als 2 MB löst den Fehler MSG_MAXSIZE_TOO_SMALL aus. Der Standardwert ist UNLIMITED.  
  
 MAX_ROLLOVER_FILES =*{ integer* | UNLIMITED }  
 Gibt die maximale Anzahl der Dateien an, die im Dateisystem zusätzlich zur aktuellen Datei beibehalten werden. Der Wert *MAX_ROLLOVER_FILES* muss eine Ganzzahl oder UNLIMITED sein. Der Standardwert ist UNLIMITED. Dieser Parameter wird ausgewertet, sobald die Überwachung neu gestartet wird (z.B. wenn die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] neu gestartet oder die Überwachung deaktiviert und wieder aktiviert wird) oder wenn eine neue Datei benötigt wird, da MAXSIZE erreicht wurde. Wenn die Anzahl der Dateien bei der Auswertung des Werts von *MAX_ROLLOVER_FILES* die Einstellung für *MAX_ROLLOVER_FILES* überschreitet, wird die älteste Datei gelöscht. Wenn die Einstellung für *MAX_ROLLOVER_FILES* 0 lautet, wird folglich bei jeder Auswertung der Einstellung für *MAX_ROLLOVER_FILES* eine neue Datei erstellt. Bei der Auswertung der Einstellung für *MAX_ROLLOVER_FILES* wird nur eine Datei automatisch gelöscht. Wenn der Wert von *MAX_ROLLOVER_FILES* also sinkt, verringert sich die Anzahl der Dateien nur dann, wenn alte Dateien manuell gelöscht werden. Der Maximalwert für die Anzahl der Dateien beträgt 2.147.483.647.  
  
 MAX_FILES =*integer*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die maximale Anzahl von Überwachungsdateien an, die erstellt werden können. Führt kein Rollover zur ersten Datei aus, wenn die Grenze erreicht wird. Wenn die MAX_FILES-Grenze erreicht wird, schlägt jede Aktion fehl, die zusätzliche Überwachungsereignisse nach sich zieht.  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 Diese Option ordnet der Datei auf dem Datenträger den MAXSIZE-Wert zu. Sie gilt nur, wenn MAXSIZE nicht gleich UNLIMITED ist. Der Standardwert ist OFF.  
  
 QUEUE_DELAY =*integer*  
 Gibt den Zeitraum in Millisekunden an, der verstreichen kann, bevor die Verarbeitung von Überwachungsaktionen erzwungen wird. Der Wert 0 steht für eine synchrone Übermittlung. Der minimale festlegbare Abfrageverzögerungswert ist 1000 (1 Sekunde), was auch der Standardwert ist. Der maximale Wert beträgt 2.147.483.647 (2.147.483,647 Sekunden oder 24 Tage, 20 Stunden, 31 Minuten und 23,647 Sekunden). Die Angabe einer ungültigen Zahl löst den Fehler MSG_INVALID_QUEUE_DELAY aus.  
  
 ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }  
 Gibt an, ob die an das Ziel ausgebende Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fehlschlagen lassen, fortsetzen oder beenden soll, wenn das Ziel keine Daten in das Überwachungsprotokoll schreiben kann. Der Standardwert ist CONTINUE.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Vorgänge werden fortgesetzt. Überwachungsdatensätze werden nicht beibehalten. Bei der Überwachung wird weiterhin versucht, Ereignisse zu protokollieren. Sie wird fortgesetzt, wenn die Fehlerbedingung aufgelöst wurde. Durch Auswählen der Continue-Option können unter Umständen nicht überwachte Aktivitäten ausgeführt werden, die gegen Ihre Sicherheitsrichtlinien verstoßen könnten. Verwenden Sie diese Option, wenn die weitere Verwendung von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wichtiger als die Beibehaltung einer vollständigen Überwachung ist.  
  
SHUTDOWN  
Erzwingt, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] heruntergefahren wird, falls [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus irgendeinem Grund keine Daten in das Überwachungsziel schreiben kann. Die Anmeldung, bei der die `CREATE SERVER AUDIT`-Anweisung ausgeführt wird, muss über die `SHUTDOWN`-Berechtigung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügen. Das Verhalten für das Herunterfahren besteht auch dann, wenn die `SHUTDOWN`-Berechtigung später von der ausführenden Anmeldung widerrufen wird. Wenn der Benutzer nicht über diese Berechtigung verfügt, schlägt die Anweisung fehl, und die Überwachung wird nicht erstellt. Verwenden Sie die Option, wenn ein Überwachungsfehler die Sicherheit oder die Integrität des Systems beeinträchtigen konnte. Weitere Informationen finden Sie unter [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md).  
  
 FAIL_OPERATION  
 Datenbankaktionen schlagen fehl, wenn sie überwachte Ereignisse verursachen. Aktionen, die keine überwachten Ereignisse verursachen, können fortgesetzt werden, es können jedoch keine überwachten Ereignisse auftreten. Bei der Überwachung wird weiterhin versucht, Ereignisse zu protokollieren. Sie wird fortgesetzt, wenn die Fehlerbedingung aufgelöst wurde. Verwenden Sie diese Option, wenn die Beibehaltung einer vollständigen Überwachung wichtiger als der Vollzugriff auf [!INCLUDE[ssDE](../../includes/ssde-md.md)] ist.  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

 AUDIT_GUID =*uniqueidentifier*  
 Um Szenarien, wie beispielsweise Datenbankspiegelung unterstützen zu können, benötigt eine Überwachung einen bestimmten GUID, der dem GUID in der gespiegelten Datenbank entspricht. Der GUID kann, nachdem die Überwachung erstellt wurde, nicht mehr geändert werden.  
  
 predicate_expression  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Prädikatausdruck an, mit dessen Hilfe bestimmt wird, ob ein Ereignis verarbeitet werden muss. Die Länge von Prädikatausdrücken ist auf 3000 Zeichen beschränkt, wodurch die Länge von Zeichenfolgenargumenten eingeschränkt wird.  
  
 event_field_name  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ist der Name des Ereignisfelds, das die Prädikatquelle identifiziert. Überwachungsfelder werden in [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) beschrieben. Mit Ausnahme von `file_name`, `audit_file_offset` und `event_time` können alle Felder gefiltert werden.  

> [!NOTE]  
>  Während die Felder `action_id` und `class_type` in sys.fn_get_audit_file den Datentyp **varchar** aufweisen, können sie nur mit Zahlen verwendet werden, wenn sie eine Prädikatquelle für die Filterung darstellen. Führen Sie die folgende Abfrage aus, um die Liste der mit `class_type` zu verwendenden Werte abzurufen:  
> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```


 number  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ein numerischer Typ einschließlich **decimal**. Einschränkungen stellen der verfügbare physische Speicher oder eine Zahl dar, die zu groß ist, um als 64-Bit-Ganzzahl dargestellt werden zu können.  
  
 ' string '  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Entweder eine ANSI- oder Unicode-Zeichenfolge, die vom Prädikatvergleich verlangt wird. Für die Prädikatvergleichsfunktionen wird keine implizite Zeichenfolgentypkonvertierung ausgeführt. Die Übergabe des falschen Typs führt zu einem Fehler.  
  
## <a name="remarks"></a>Remarks  
 Wenn eine Serverüberwachung erstellt wird, befindet sie sich im deaktivierten Zustand.  
  
 Die CREATE SERVER AUDIT-Anweisung liegt im Bereich einer Transaktion. Wird ein Rollback für die Transaktion ausgeführt, so wird auch für die Anweisung ein Rollback durchgeführt.  
  
## <a name="permissions"></a>Berechtigungen  
 Um eine Serverüberwachung zu erstellen, zu ändern oder zu löschen, benötigen Prinzipale die ALTER ANY SERVER AUDIT-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
 Schränken Sie beim Speichern von Überwachungsinformationen in einer Datei den Zugriff auf deren Speicherort ein, um eine Manipulation zu verhindern.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>A. Erstellen einer Serverüberwachung mit einem Dateiziel  
 Im folgenden Beispiel wird eine Serverüberwachung namens `HIPPA_Audit` mit einer Binärdatei als Ziel und ohne weitere Optionen erstellt.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>B. Erstellen einer Serverüberwachung mit einem Windows-Anwendungsprotokollziel und Optionen  
 Im folgenden Beispiel wird eine Serverüberwachung namens `HIPPA_Audit` mit dem Windows-Ereignisprotokoll als Ziel erstellt. Die Warteschlange wird jede Sekunde geschrieben und fährt bei einem Fehler das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Modul herunter.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> C. Erstellen einer Serverüberwachung, die eine WHERE-Klausel enthält  
 Im folgenden Beispiel werden eine Datenbank, ein Schema und zwei Tabellen für das Beispiel erstellt. Die Tabelle mit dem Namen `DataSchema.SensitiveData` enthält vertrauliche Daten. Der Zugriff auf die Tabelle muss bei der Überwachung aufgezeichnet werden. Die Tabelle `DataSchema.GeneralData` beinhaltet keine vertraulichen Daten. Die Datenbank-Überwachungsspezifikation überwacht den Zugriff auf alle Objekte im `DataSchema`-Schema. Die Serverüberwachung wird mit einer WHERE-Klausel erstellt, die die Serverüberwachung ausschließlich auf die `SensitiveData`-Tabelle beschränkt. Bei der Serverüberwachung wird angenommen, dass unter `C:\SQLAudit` ein Überwachungsordner vorhanden ist.  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
