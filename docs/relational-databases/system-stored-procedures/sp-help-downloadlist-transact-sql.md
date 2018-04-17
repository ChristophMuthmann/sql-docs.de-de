---
title: Sp_help_downloadlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b891780620de40d8541b7fc42e100b575e6ad7d1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpdownloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet alle Zeilen in der **Sysdownloadlist** -Systemtabelle für den angegebenen Auftrag oder alle Zeilen, wenn kein Auftrag angegeben wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id=** ] *job_id*  
 Die ID des Auftrags, zu dem Informationen zurückgegeben werden sollen. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@operation=** ] **'***operation***'**  
 Der gültige Vorgang für den angegebenen Auftrag. *Vorgang* ist **varchar(64)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**FEHLER**|Servervorgang, der den Zielserver beim Austragen aus dem Master-anfordert **SQLServerAgent** Dienst.|  
|**DELETE**|Auftragsvorgang, mit dem ein gesamter Auftrag entfernt wird|  
|**INSERT**|Auftragsvorgang, der einen gesamten Auftrag einfügt oder einen vorhandenen Auftrag aktualisiert. Dieser Vorgang schließt ggf. alle Auftragsschritte und Zeitpläne ein.|  
|**RE-ENLIST**|Servervorgang, der bewirkt, dass der Zielserver die Eintragsinformationen, einschließlich des Abrufintervalls und der Zeitzone, erneut an die Multiserverdomäne sendet. Der Zielserver downloadet auch erneut die **MSXOperator** Details.|  
|**SET-POLL**|Servervorgang, der festlegt, in welchem Intervall (in Sekunden) die Zielserver die Multiserverdomäne abfragen. Wenn angegeben, *Wert* ist als der erforderliche Intervallwert interpretiert, und ein Wert von **10** auf **28.800**.|  
|**START**|Auftragsvorgang, der den Start der Auftragsausführung anfordert|  
|**BEENDEN**|Auftragsvorgang, der das Beenden der Auftragsausführung anfordert|  
|**ZEITPUNKT DER SYNCHRONISIERUNG**|Servervorgang, der bewirkt, dass der Zielserver die Systemuhr mit der Multiserverdomäne synchronisiert. Dies ist ein kostenaufwendiger Vorgang und sollte deshalb nur selten und in begrenztem Umfang durchgeführt werden.|  
|**UPDATE**|Auftragsvorgang, das aktualisiert nur die **Sysjobs** Informationen für einen Auftrag, nicht die Auftragsschritte oder Zeitpläne. Wird automatisch aufgerufen, indem **Sp_update_job**.|  
  
 [  **@object_type=** ] **"***Object_type***"**  
 Der Typ des Objekts für den angegebenen Auftrag. *Object_type* ist **varchar(64)**, hat den Standardwert NULL. *Object_type* kann JOB oder SERVER sein. Weitere Informationen zu gültigen *Object_type*-Werte finden Sie in [Sp_add_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md).  
  
 [  **@object_name=** ] **"***Object_name***"**  
 Der Name des Objekts. *Object_name* ist **Sysname**, hat den Standardwert NULL. Wenn *Object_type* Wert JOB aufweist, *Object_name*ist der Name des Auftrags. Wenn *Object_type*ist der SERVER, *Object_name*ist der Servername.  
  
 [ **@target_server=** ] **'***target_server***'**  
 Der Name des Zielservers. *Target_server* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL.  
  
 [  **@has_error=** ] *Has_error*  
 Gibt an, ob der Auftrag Fehler bestätigen soll. *Has_error* ist **"tinyint"**, hat den Standardwert NULL, gibt keine Fehler bestätigt werden sollen. **1** gibt an, dass alle Fehler bestätigt werden sollen.  
  
 [ **@status=** ] *status*  
 Der Status für den Auftrag. *Status* ist **"tinyint"**, hat den Standardwert NULL.  
  
 [  **@date_posted=** ] *Date_posted*  
 Das Datum und die Uhrzeit des Zeitpunkts, zu dem alle Einträge, die zu oder nach dem angegebenen Datum und der angegebenen Uhrzeit erstellt wurden, im Resultset enthalten sein sollen. *Date_posted* ist **"DateTime"**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Eindeutige, ganzzahlige ID der Anweisung|  
|**source_server**|**nvarchar(30)**|Computername des Servers, vom dem die Anweisung stammt. In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0, dies ist immer der Computername des Masterservers (MSX).|  
|**operation_code**|**nvarchar(4000)**|Vorgangscode für die Anweisung|  
|**object_name**|**sysname**|Objekt, das von der Anweisung betroffen ist|  
|**object_id**|**uniqueidentifier**|ID des Objekts, das von der Anweisung betroffen (**Job_id** für ein Auftragsobjekt oder 0 x 00 für ein Serverobjekt) oder einen Datenwert, der speziell für die **Operation_code**.|  
|**target_server**|**nvarchar(30)**|Zielserver, der diese Anweisung herunterladen soll|  
|**error_message**|**nvarchar(1024)**|Gegebenenfalls Fehlermeldung vom Zielserver, falls beim Verarbeiten dieser Anweisung ein Problem aufgetreten ist.<br /><br /> Hinweis: Fehlermeldungen blockieren alle weiteren Downloadvorgänge durch den Zielserver.|  
|**date_posted**|**datetime**|Datum, an dem die Anweisung für die Tabelle bereitgestellt wurde|  
|**date_downloaded**|**datetime**|Datum, an dem die Anweisung durch den Zielserver heruntergeladen wurde|  
|**status**|**tinyint**|Status des Auftrags:<br /><br /> **0** = Noch nicht heruntergeladen<br /><br /> **1** = erfolgreich heruntergeladen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen Mitglieder der festen Serverrolle **sysadmin** über die Berechtigungen zum Ausführen dieser Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Zeilen in der `sysdownloadlist`-Tabelle für den Auftrag `NightlyBackups` aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
