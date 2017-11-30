---
title: Sp_syscollector_update_collection_set (Transact-SQL) | Microsoft Docs
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
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs: TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90f034f59bc7430e059fb276ec0111a4af2f807c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spsyscollectorupdatecollectionset-transact-sql"></a>sp_syscollector_update_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird verwendet, um die Eigenschaften eines benutzerdefinierten Sammlungssatzes zu ändern oder einen benutzerdefinierten Sammlungssatz umzubenennen.  
  
> [!WARNING]  
>  Falls das als Proxy konfigurierte Windows-Konto einem nicht interaktiven oder interaktiven Benutzer entspricht, der noch nicht angemeldet ist, ist das Profilverzeichnis nicht vorhanden, und die Erstellung des Stagingverzeichnisses schlägt in dem Fall fehl. Verwenden Sie ein Proxykonto auf einem Domänencontroller, müssen Sie also ein interaktives Konto angeben, das mindestens einmal verwendet wurde. So lässt sich sicherstellen, dass das Profilverzeichnis erstellt wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@collection_set_id =** ] *Collection_set_id*  
 Der eindeutige lokale Bezeichner für den Sammlungssatz. *Collection_set_id* ist **Int** und muss einen Wert aufweisen, wenn *Namen* ist NULL.  
  
 [  **@name =** ] "*Namen*"  
 Ist der Name des Sammlungssatzes. *Namen* ist **Sysname** und muss einen Wert aufweisen, wenn *Collection_set_id* ist NULL.  
  
 [  **@new_name =** ] "*New_name*"  
 Entspricht dem neuen Namen des Sammlungssatzes. *New_name* ist **Sysname**, und kann nicht verwendet, eine leere Zeichenfolge sein. *New_name* muss eindeutig sein. Wenn Sie eine Liste der aktuellen Namen von Sammlungssätzen abrufen möchten, fragen Sie die syscollector_collection_sets-Systemsicht ab.  
  
 [  **@target =** ] "*Ziel*"  
 Zur künftigen Verwendung reserviert.  
  
 [  **@collection_mode =** ] *Collection_mode*  
 Entspricht dem Typ der zu verwendenden Datenauflistung. *Collection_mode* ist **"smallint"** und kann einen der folgenden Werte aufweisen:  
  
 0 - Modus mit Zwischenspeicherung. Für Datensammlung und -upload werden separate Zeitpläne verwendet. Geben Sie den Modus mit Zwischenspeicherung für eine fortlaufende Sammlung an.  
  
 1 - Modus ohne Zwischenspeicherung. Für Datensammlung und -upload wird der gleiche Zeitplan verwendet. Geben Sie den Modus ohne Zwischenspeicherung für eine Ad-hoc-Sammlung oder eine Momentaufnahmesammlung an.  
  
 Ändern Sie im Modus ohne Zwischenspeicherung in den Modus mit Zwischenspeicherung (0), müssen Sie auch angeben entweder *Schedule_uid* oder *Schedule_name*.  
  
 [  **@days_until_expiration=** ] *Days_until_expiration*  
 Ist die Anzahl der Tage, die gesammelten Daten im Verwaltungs-Datawarehouse gespeichert werden. *Days_until_expiration* ist **"smallint"**. *Days_until_expiration* muss 0 oder eine positive ganze Zahl sein.  
  
 [  **@proxy_id =** ] *Proxy_id*  
 Ist der eindeutige Bezeichner für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Proxykonto. *Proxy_id* ist **Int**.  
  
 [  **@proxy_name =** ] "*Proxy_name*"  
 Ist der Name des Proxys. *Proxy_name* ist **Sysname** und NULL-Werte zulässt.  
  
 [  **@schedule_uid**  =] '*Schedule_uid*"  
 Entspricht dem GUID, der auf einen Zeitplan zeigt. *Schedule_uid* ist **"uniqueidentifier"**.  
  
 Zum Abrufen *Schedule_uid*, Fragen Sie die Sysschedules-Systemtabelle.  
  
 Wenn *Collection_mode* ist auf 0 festgelegt, *Schedule_uid* oder *Schedule_name* muss angegeben werden. Wenn *Collection_mode* ist auf 1 festgelegt, *Schedule_uid* oder *Schedule_name* wird ignoriert, wenn angegeben.  
  
 [  **@schedule_name =** ] "*Schedule_name*"  
 Ist der Name des Zeitplans. *Schedule_name* ist **Sysname** und NULL-Werte zulässt. Wenn angegeben, *Schedule_uid* muss NULL sein. Zum Abrufen *Schedule_name*, Fragen Sie die Sysschedules-Systemtabelle.  
  
 [  **@logging_level =** ] *Logging_level*  
 Entspricht dem Protokolliergrad. *Logging_level* ist **"smallint"** mit einem der folgenden Werte:  
  
 0 - Informationen zur Protokollausführung und zu den [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Ereignissen, die Folgendes nachverfolgen:  
  
-   Starten/Beenden von Samlungssätzen  
  
-   Starten/Beenden von Paketen  
  
-   Fehlerinformationen  
  
 1 - Ebene-0-Protokollierung und:  
  
-   Ausführungsstatistiken  
  
-   Kontinuierliche Ausführung der Sammlung  
  
-   Warnungsereignisse von [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - Protokollierung Stufe 1 sowie ausführliche Ereignisinformationen von [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Der Standardwert für *Logging_level* ist 1.  
  
 [  **@description =** ] "*Beschreibung*"  
 Die Beschreibung für den Sammlungssatz. *Beschreibung* ist **nvarchar(4000)**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_syscollector_update_collection_set muss im Kontext der msdb-Systemdatenbank ausgeführt werden.  
  
 Entweder *Collection_set_id* oder *Namen* muss über einen Wert verfügen, können nicht beide NULL sein. Um diese Werte abzurufen, fragen Sie die syscollector_collection_sets-Systemsicht ab.  
  
 Wenn der Sammlungssatz ausgeführt wird, können Sie nur aktualisieren *Schedule_uid* und *Beschreibung*. Um den Sammlungssatz anzuhalten, verwenden Sie [Sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Damit dieser Vorgang ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin oder dc_operator (mit EXECUTE-Berechtigung) erforderlich. Obwohl die dc_operator-Rolle diese gespeicherte Prozedur ausführen kann, können die Eigenschaften von den Mitgliedern dieser Rolle nur begrenzt geändert werden. Die folgenden Eigenschaften können nur von dc_admin geändert werden:  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-renaming-a-collection-set"></a>A. Umbenennen eines Sammlungssatzes  
 Im folgenden Beispiel wird ein benutzerdefinierter Sammlungssatz umbenannt.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. Wechseln vom Auflistmodus ohne Zwischenspeicherung in den Modus mit Zwischenspeicherung  
 Im folgenden Beispiel wird vom Sammlungsmodus ohne Zwischenspeicherung in den Modus mit Zwischenspeicherung gewechselt. Für diesen Wechsel müssen Sie eine Zeitplan-ID oder einen Zeitplannamen angeben.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>C. Ändern von anderen Sammlungssatzparametern  
 Im folgenden Beispiel werden verschiedene Eigenschaften des Sammlungssatzes "Simple collection set test 2" aktualisiert.  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Syscollector_collection_sets &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysschedules &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
