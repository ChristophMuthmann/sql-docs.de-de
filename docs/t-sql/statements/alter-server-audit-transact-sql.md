---
title: ALTER SERVER AUDIT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
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
- ALTER_SERVER_AUDIT_TSQL
- ALTER SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT statement
ms.assetid: 63426d31-7a5c-4378-aa9e-afcf4f64ceb3
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7bedbd1b8244c337fc0d325eff850dd89b7c7160
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-server-audit--transact-sql"></a>ALTER SERVER AUDIT (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Ändert ein Serverüberwachungsobjekt mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit-Funktion. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER SERVER AUDIT audit_name  
{  
    [ TO { { FILE ( <file_options> [, ...n] ) } | APPLICATION_LOG | SECURITY_LOG } ]  
    [ WITH ( <audit_options> [ , ...n] ) ]   
    [ WHERE <predicate_expression> ]  
}  
| REMOVE WHERE  
| MODIFY NAME = new_audit_name  
[ ; ]  
  
<file_options>::=  
{  
      FILEPATH = 'os_file_path'   
    | MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED }   
    | MAX_ROLLOVER_FILES = { integer | UNLIMITED }   
    | MAX_FILES = integer   
    | RESERVE_DISK_SPACE = { ON | OFF }   
}  
  
<audit_options>::=  
{  
      QUEUE_DELAY = integer   
    | ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }   
    | STATE = = { ON | OFF }   
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
 TO { FILE | APPLICATION_LOG | SECURITY }  
 Legt den Speicherort des Überwachungsziels fest. Die Optionen sind eine Binärdatei, das Windows-Anwendungsprotokoll oder das Windows-Sicherheitsprotokoll.  
  
 FILEPATH **= '***os_file_path***'**  
 Der Pfad der Überwachungsliste. Der Dateiname wird auf der Grundlage des Überwachungsnamens und des Überwachungs-GUID generiert.  
  
 MAXSIZE **=***max_size*  
 Gibt die maximale Größe an, die die Überwachungsdatei annehmen kann. Der *max_size*-Wert muss ein Integer gefolgt von **MB**, **GB**, **TB** oder **UNLIMITED** sein. Die minimale Größe, die Sie für *max_size* angeben können, beträgt 2 **MB**, und die maximale Größe beträgt 2.147.483.647 **TB**. Wird **UNLIMITED** angegeben, kann die Größe der Datei so lange zunehmen, bis auf dem Datenträger kein Speicherplatz mehr verfügbar ist. Die Angabe eines Werts kleiner als 2 MB löst den Fehler MSG_MAXSIZE_TOO_SMALL aus. Der Standardwert ist **UNLIMITED**.  
  
 MAX_ROLLOVER_FILES **=***integer* | **UNLIMITED**  
 Gibt die maximale Anzahl der Dateien an, die im Dateisystem beibehalten werden. Bei der Einstellung MAX_ROLLOVER_FILES=0 gibt es keine Begrenzung für die Anzahl der Rolloverdateien, die erstellt werden. Der Standardwert ist 0. Der Maximalwert für die Anzahl der Dateien beträgt 2.147.483.647.  
  
 MAX_FILES =*integer*  
 Gibt die maximale Anzahl von Überwachungsdateien an, die erstellt werden können. Führt keinen Rollover zur ersten Datei aus, wenn die Grenze erreicht wird. Wenn die MAX_FILES-Grenze erreicht wird, schlägt jede Aktion, die zusätzliche Überwachungsereignisse nach sich zieht, fehl.  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 RESERVE_DISK_SPACE **=** { ON | OFF }  
 Diese Option ordnet der Datei auf dem Datenträger den MAXSIZE-Wert zu. Dieser Wert wird nur dann übernommen, wenn MAXSIZE nicht gleich UNLIMITED ist. Der Standardwert ist OFF.  
  
 QUEUE_DELAY **=***integer*  
 Gibt den Zeitraum in Millisekunden an, der verstreichen kann, bevor die Verarbeitung von Überwachungsaktionen erzwungen wird. Der Wert 0 steht für eine synchrone Übermittlung. Der minimale festlegbare Abfrageverzögerungswert ist 1000 (1 Sekunde), was auch der Standardwert ist. Der maximale Wert beträgt 2.147.483.647 (2.147.483,647 Sekunden oder 24 Tage, 20 Stunden, 31 Minuten und 23,647 Sekunden). Die Angabe eines ungültigen Werts löst den Fehler MSG_INVALID_QUEUE_DELAY aus.  
  
 ON_FAILURE **=** { CONTINUE | SHUTDOWN | FAIL_OPERATION}  
 Gibt an, ob die an das Ziel ausgebende Instanz fehlschlagen, fortgesetzt oder beendet werden soll, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Daten in das Überwachungsprotokoll schreiben kann.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Vorgänge werden fortgesetzt. Überwachungsdatensätze werden nicht beibehalten. Bei der Überwachung wird weiterhin versucht, Ereignisse zu protokollieren. Sie wird fortgesetzt, wenn die Fehlerbedingung aufgelöst wurde. Durch Auswählen der Continue-Option können unter Umständen nicht überwachte Aktivitäten ausgeführt werden, die gegen Ihre Sicherheitsrichtlinien verstoßen könnten. Verwenden Sie diese Option, wenn die weitere Verwendung von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wichtiger als die Beibehaltung einer vollständigen Überwachung ist.  
  
SHUTDOWN  
Erzwingt, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] heruntergefahren wird, falls [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus irgendeinem Grund keine Daten in das Überwachungsziel schreiben kann. Die Anmeldung, bei der die `ALTER`-Anweisung ausgeführt wird, muss über die `SHUTDOWN`-Berechtigung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügen. Das Herunterfahren wird auch dann fortgesetzt, wenn die `SHUTDOWN`-Berechtigung später von der ausführenden Anmeldung widerrufen wird. Wenn der Benutzer nicht über diese Berechtigung verfügt, schlägt die Anweisung fehl, und die Überwachung wird nicht geändert. Verwenden Sie die Option, wenn ein Überwachungsfehler die Sicherheit oder die Integrität des Systems beeinträchtigen konnte. Weitere Informationen finden Sie unter [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md). 
  
 FAIL_OPERATION  
 Datenbankaktionen schlagen fehl, wenn sie überwachte Ereignisse verursachen. Aktionen, die keine überwachten Ereignisse verursachen, können fortgesetzt werden, es können jedoch keine überwachten Ereignisse auftreten. Bei der Überwachung wird weiterhin versucht, Ereignisse zu protokollieren. Sie wird fortgesetzt, wenn die Fehlerbedingung aufgelöst wurde. Verwenden Sie diese Option, wenn die Beibehaltung einer vollständigen Überwachung wichtiger als der Vollzugriff auf [!INCLUDE[ssDE](../../includes/ssde-md.md)] ist.  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].   
  
 STATE **=** { ON | OFF }  
 Aktiviert oder deaktiviert das Sammeln von Datensätzen durch die Überwachung. Wird der Status einer laufenden Überwachung geändert (von ON zu OFF), wird ein Eintrag erstellt, der angibt, dass die Überwachung angehalten wurde, welcher Prinzipal die Überwachung angehalten hat und zu welchem Zeitpunkt sie angehalten wurde.  
  
 MODIFY NAME = *new_audit_name*  
 Ändert den Namen der Überwachung. Kann nicht zusammen mit einer anderen Option verwendet werden.  
  
 predicate_expression  
 Gibt den Prädikatausdruck an, mit dessen Hilfe bestimmt wird, ob ein Ereignis verarbeitet werden muss. Die Länge von Prädikatausdrücken ist auf 3000 Zeichen beschränkt, wodurch die Länge von Zeichenfolgenargumenten eingeschränkt wird.  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 event_field_name  
 Ist der Name des Ereignisfelds, das die Prädikatquelle identifiziert. Überwachungsfelder werden in [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) beschrieben. Mit Ausnahme von `file_name` und `audit_file_offset` können alle Felder überwacht werden.  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 number  
 Ein numerischer Typ einschließlich **decimal**. Einschränkungen stellen der verfügbare physische Speicher oder eine Zahl dar, die zu groß ist, um als 64-Bit-Ganzzahl dargestellt werden zu können.  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ' string '  
 Entweder eine ANSI- oder Unicode-Zeichenfolge, die vom Prädikatvergleich verlangt wird. Für die Prädikatvergleichsfunktionen wird keine implizite Zeichenfolgentypkonvertierung ausgeführt. Die Übergabe des falschen Typs führt zu einem Fehler.  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="remarks"></a>Remarks  
 Sie müssen mindestens eine der Klauseln TO, WITH oder MODIFY NAME angeben, wann Sie ALTER AUDIT aufrufen.  
  
 Sie müssen den Status einer Überwachung auf OFF festlegen, um Änderungen an der Überwachung vornehmen zu können. Wenn ALTER AUDIT ausgeführt wird, während eine Überwachung mit einer anderen Option als STATE=OFF aktiviert ist, erhalten Sie die Fehlermeldung MSG_NEED_AUDIT_DISABLED.  
  
 Sie können Überwachungsspezifikation hinzufügen, ändern und entfernen, ohne eine Überwachung beenden zu müssen.  
  
 Sie können den GUID einer Überwachung nicht ändern, nachdem die Überwachung erstellt wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Um einen Serverüberwachungsprinzipal erstellen, ändern oder löschen zu können, müssen Sie über die Berechtigung ALTER ANY SERVER AUDIT oder CONTROL SERVER verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-a-server-audit-name"></a>A. Ändern eines Serverüberwachungsnamens  
 Im folgenden Beispiel wird der Name der Serverüberwachung `HIPPA_Audit` in `HIPAA_Audit_Old` geändert.  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
MODIFY NAME = HIPAA_Audit_Old;  
GO  
ALTER SERVER AUDIT HIPAA_Audit_Old  
WITH (STATE = ON);  
GO  
```  
  
### <a name="b-changing-a-server-audit-target"></a>B. Ändern eines Serverüberwachungsziels  
 Im folgenden Beispiel wird die Serverüberwachung namens `HIPPA_Audit` in ein Dateiziel geändert.  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
TO FILE (FILEPATH ='\\SQLPROD_1\Audit\',  
          MAXSIZE = 1000 MB,  
          RESERVE_DISK_SPACE=OFF)  
WITH (QUEUE_DELAY = 1000,  
       ON_FAILURE = CONTINUE);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = ON);  
GO  
```  
  
### <a name="c-changing-a-server-audit-where-clause"></a>C. Ändern einer WHERE-Klausel für Serverüberwachung  
 Im folgenden Beispiel wird die in Beispiel C für [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md) erstellte WHERE-Klausel geändert. Mit der neuen WHERE-Klausel wird nach dem benutzerdefinierten Ereignis gefiltert, falls dessen Wert 27 ist.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
WHERE user_defined_event_id = 27;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="d-removing-a-where-clause"></a>D. Entfernen einer WHERE-Klausel  
 Im folgenden Beispiel wird ein WHERE-Klausel-Prädikatausdruck entfernt.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
REMOVE WHERE;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="e-renaming-a-server-audit"></a>E. Umbenennen einer Serverüberwachung  
 Im folgenden Beispiel wird der Name der Serverüberwachung von `FilterForSensitiveData` in `AuditDataAccess` geändert.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
MODIFY NAME = AuditDataAccess;  
GO  
ALTER SERVER AUDIT [AuditDataAccess] WITH (STATE = ON);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
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
 [Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
