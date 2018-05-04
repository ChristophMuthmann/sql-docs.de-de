---
title: Sp_syscollector_create_collection_set (Transact-SQL) | Microsoft Docs
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
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b958d236f24d36bddca9ed9e51d4cac92aef29e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectorcreatecollectionset-transact-sql"></a>sp_syscollector_create_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen Sammlungssatz. Sie können diese gespeicherte Prozedur verwenden, um einen benutzerdefinierten Sammlungssatz für die Datensammlung zu erstellen.  
  
> [!WARNING]  
>  Falls das als Proxy konfigurierte Windows-Konto einem nicht interaktiven oder interaktiven Benutzer entspricht, der noch nicht angemeldet ist, ist das Profilverzeichnis nicht vorhanden, und die Erstellung des Stagingverzeichnisses schlägt in dem Fall fehl. Verwenden Sie ein Proxykonto auf einem Domänencontroller, müssen Sie also ein interaktives Konto angeben, das mindestens einmal verwendet wurde. So lässt sich sicherstellen, dass das Profilverzeichnis erstellt wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name =** ] "*Namen*"  
 Ist der Name des Sammlungssatzes. *Namen* ist **Sysname** und darf nicht NULL oder eine leere Zeichenfolge sein.  
  
 *Namen* muss eindeutig sein. Wenn Sie eine Liste der aktuellen Namen von Sammlungssätzen abrufen möchten, fragen Sie die syscollector_collection_sets-Systemsicht ab.  
  
 [  **@target =** ] "*Ziel*"  
 Zur künftigen Verwendung reserviert. *Namen* ist **vom Datentyp nvarchar(128)** hat den Standardwert NULL.  
  
 [ **@collection_mode =** ] *collection_mode*  
 Gibt die Art und Weise an, in der die Daten gesammelt und gespeichert werden. *Collection_mode* ist **"smallint"** und kann einen der folgenden Werte aufweisen:  
  
 0 - Modus mit Zwischenspeicherung. Für Datensammlung und -upload werden separate Zeitpläne verwendet. Geben Sie den Modus mit Zwischenspeicherung für eine fortlaufende Sammlung an.  
  
 1 - Modus ohne Zwischenspeicherung. Für Datensammlung und -upload wird der gleiche Zeitplan verwendet. Geben Sie den Modus ohne Zwischenspeicherung für eine Ad-hoc-Sammlung oder eine Momentaufnahmesammlung an.  
  
 Der Standardwert für *Collection_mode* ist 0. Wenn *Collection_mode* ist 0, *Schedule_uid* oder *Schedule_name* muss angegeben werden.  
  
 [  **@days_until_expiration =** ] *Days_until_expiration*  
 Ist die Anzahl der Tage, die gesammelten Daten im Verwaltungs-Datawarehouse gespeichert werden. *Days_until_expiration* ist **"smallint"** hat den Standardwert 730 (zwei Jahre). *Days_until_expiration* muss 0 oder eine positive ganze Zahl sein.  
  
 [ **@proxy_id =** ] *proxy_id*  
 Ist der eindeutige Bezeichner für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Proxykonto. *Proxy_id* ist **Int** hat den Standardwert NULL. Wenn angegeben, *Proxy_name* muss NULL sein. Zum Abrufen *Proxy_id*, Fragen Sie die Sysproxies-Systemtabelle. Die feste Datenbankrolle dc_admin muss über die Berechtigung für den Zugriff auf den Proxy verfügen. Weitere Informationen finden Sie unter [Erstellen eines SQL Server-Agent-Proxys](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988).  
  
 [  **@proxy_name =** ] "*Proxy_name*"  
 Der Name des Proxykontos. *Proxy_name* ist **Sysname** hat den Standardwert NULL. Wenn angegeben, *Proxy_id* muss NULL sein. Zum Abrufen *Proxy_name*, Fragen Sie die Sysproxies-Systemtabelle.  
  
 [  **@schedule_uid =** ] "*Schedule_uid*"  
 Entspricht dem GUID, der auf einen Zeitplan zeigt. *Schedule_uid* ist **"uniqueidentifier"** hat den Standardwert NULL. Wenn angegeben, *Schedule_name* muss NULL sein. Zum Abrufen *Schedule_uid*, Fragen Sie die Sysschedules-Systemtabelle.  
  
 Wenn *Collection_mode* ist auf 0 festgelegt, *Schedule_uid* oder *Schedule_name* muss angegeben werden. Wenn *Collection_mode* ist auf 1 festgelegt, *Schedule_uid* oder *Schedule_name* wird ignoriert, wenn angegeben.  
  
 [  **@schedule_name =** ] "*Schedule_name*"  
 Ist der Name des Zeitplans. *Schedule_name* ist **Sysname** hat den Standardwert NULL. Wenn angegeben, *Schedule_uid* muss NULL sein. Zum Abrufen *Schedule_name*, Fragen Sie die Sysschedules-Systemtabelle.  
  
 [  **@logging_level =** ] *Logging_level*  
 Entspricht dem Protokolliergrad. *Logging_level* ist **"smallint"** mit einem der folgenden Werte:  
  
 0 – Informationen zur Protokollausführung und zu den [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Ereignissen, die Folgendes nachverfolgen:  
  
-   Starten/Beenden von Samlungssätzen  
  
-   Starten/Beenden von Paketen  
  
-   Fehlerinformationen  
  
 1 - Protokollierung Stufe 0 und:  
  
-   Ausführungsstatistiken  
  
-   Kontinuierliche Ausführung der Sammlung  
  
-   Warnungsereignisse von [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 – Protokollierung Stufe 1 sowie ausführliche Ereignisinformationen von [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Der Standardwert für *Logging_level* ist 1.  
  
 [  **@description =** ] "*Beschreibung*"  
 Die Beschreibung für den Sammlungssatz. *Beschreibung* ist **nvarchar(4000)** hat den Standardwert NULL.  
  
 [  **@collection_set_id =** ] *Collection_set_id*  
 Der eindeutige lokale Bezeichner für den Sammlungssatz. *Collection_set_id* ist **Int** mit OUTPUT und ist erforderlich.  
  
 [  **@collection_set_uid =** ] "*Collection_set_uid*"  
 GUID für den Sammlungssatz. *Collection_set_uid* ist **"uniqueidentifier"** mit Ausgabe hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_syscollector_create_collection_set muss im Kontext der msdb-Systemdatenbank ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin (mit EXECUTE-Berechtigung) erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>A. Erstellen eines Sammlungssatzes mit Standardwerten  
 Im folgenden Beispiel wird ein Sammlungssatz erstellt, indem nur die erforderlichen Parameter angegeben werden. `@collection_mode` ist nicht erforderlich, aber für den Standardauflistmodus (zwischengespeichert) muss eine Zeitplan-ID oder ein Zeitplanname angegeben werden.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>B. Erstellen eines Sammlungssatzes mit angegebenen Werten  
 Im folgenden Beispiel wird ein Sammlungssatz erstellt, indem Werte für mehrere Parameter angegeben werden.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Erstellen eines benutzerdefinierten Sammlungssatzes, der einen generischen T-SQL-Abfragesammlertyp verwendet &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
