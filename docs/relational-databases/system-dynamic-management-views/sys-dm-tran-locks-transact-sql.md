---
title: Sys. dm_tran_locks (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_tran_locks
- sys.dm_tran_locks
- sys.dm_tran_locks_TSQL
- dm_tran_locks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_locks dynamic management view
ms.assetid: f0d3b95a-8a00-471b-9da4-14cb8f5b045f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c54a97a7b84dcb4d9873ee2537e31714b6f62172
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="sysdmtranlocks-transact-sql"></a>sys.dm_tran_locks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu derzeit aktiven Sperren-Manager-Ressourcen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück. Jede Zeile stellt eine derzeit aktive Anforderung des Sperren-Managers für eine erteilte oder zu erteilende Sperre dar.  
  
 Die Spalten im Resultset sind in zwei Hauptgruppen unterteilt: Ressourcen und Anforderungen. Die Ressourcengruppe beschreibt die Ressource, für die die Sperranforderung erfolgt. Die Anforderungsgruppe beschreibt die Sperranforderung.  
  
> [!NOTE]  
> Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_tran_locks**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**resource_type**|**nvarchar(60)**|Stellt den Ressourcentyp dar. Die folgenden Werte sind möglich: DATABASE, FILE, OBJECT, PAGE, KEY, EXTENT, RID, APPLICATION, METADATA, HOBT oder ALLOCATION_UNIT.|  
|**resource_subtype**|**nvarchar(60)**|Stellt einen Untertyp des **Resource_type**. Es ist technisch zulässig, eine Untertypsperre abzurufen, ohne dass eine Nicht-Untertypsperre des übergeordneten Typs vorhanden ist. Unterschiedliche Untertypen führen nicht zu Konflikten untereinander oder mit dem übergeordneten Typ des Nicht-Untertyps. Nicht alle Ressourcentypen weisen Untertypen auf.|  
|**resource_database_id**|**int**|ID der Datenbank, zu deren Bereich diese Ressource gehört. Alle Ressourcen, die vom Sperren-Manager verarbeitet werden, erhalten die Datenbank-ID als Bereich.|  
|**resource_description**|**nvarchar(256)**|Beschreibung der Ressource, die nur Informationen enthält, die in anderen Ressourcenspalten nicht verfügbar sind.|  
|**resource_associated_entity_id**|**bigint**|ID der Entität in einer Datenbank, der eine Ressource zugeordnet ist. Hierbei kann es sich je nach Ressourcentyp um eine Objekt-ID, eine HoBt-ID oder eine Zuordnungseinheit-ID handeln.|  
|**resource_lock_partition**|**Int**|ID der Sperrenpartition für eine partitionierte Sperrenressource. Nicht partitionierte Sperrenressourcen haben den Wert 0.|  
|**request_mode**|**nvarchar(60)**|Der Anforderungsmodus. Für erteilte Anforderungen ist dies der erteilte Modus, für wartende Anforderungen ist dies der angeforderte Modus.|  
|**request_type**|**nvarchar(60)**|Der Anforderungstyp. Der Wert ist LOCK.|  
|**request_status**|**nvarchar(60)**|Aktueller Status dieser Anforderung. Mögliche Werte sind GRANTED, CONVERT, WAIT, LOW_PRIORITY_CONVERT, LOW_PRIORITY_WAIT oder ABORT_BLOCKERS. Weitere Informationen zu Wartezeiten mit niedriger Priorität und abbruchsblockern finden Sie unter der *Low_priority_lock_wait* Abschnitt [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md).|  
|**request_reference_count**|**smallint**|Gibt zurück, wie oft derselbe Anforderer diese Ressource ungefähr angefordert hat.|  
|**request_lifetime**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**request_session_id**|**int**|Sitzungs-ID, der diese Anforderung derzeit gehört. Die Sitzungs-ID für den Besitzer kann sich für verteilte und gebundene Transaktionen ändern. Der Wert -2 gibt an, dass die Anforderung einer verwaisten verteilten Transaktion gehört. Der Wert -3 gibt an, dass die Anforderung zu einer verzögerten Wiederherstellungstransaktion gehört, wie z. B. eine Transaktion, für die ein Rollback bei der Wiederherstellung verzögert wurde, weil das Rollback nicht erfolgreich abgeschlossen werden konnte.|  
|**request_exec_context_id**|**int**|Ausführungskontext-ID des Prozesses, der derzeit diese Anforderung besitzt.|  
|**request_request_id**|**int**|Anforderungs-ID (Batch-ID) des Prozesses, der derzeit diese Anforderung besitzt. Dieser Wert wird jedes Mal geändert, wenn sich die aktive MARS-Verbindung (Multiple Active Result Set) für eine Transaktion ändert.|  
|**request_owner_type**|**nvarchar(60)**|Entitätstyp, der die Anforderung besitzt. Sperren-Manager-Anforderungen können im Besitz einer Reihe von Entitäten sein. Folgende Werte sind möglich:<br /><br /> TRANSACTION = Der Besitzer der Anforderung ist eine Transaktion.<br /><br /> CURSOR = Der Besitzer der Anforderung ist ein Cursor.<br /><br /> SESSION = Der Besitzer der Anforderung ist eine Benutzersitzung.<br /><br /> SHARED_TRANSACTION_WORKSPACE = Der Besitzer der Anforderung ist der freigegebene Bereich des Transaktionsarbeitsbereichs.<br /><br /> EXCLUSIVE_TRANSACTION_WORKSPACE = Der Besitzer der Anforderung ist der exklusive Bereich des Transaktionsarbeitsbereichs.<br /><br /> NOTIFICATION_OBJECT = Der Besitzer der Anforderung ist eine interne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponente. Diese Komponente hat vom Sperren-Manager eine Benachrichtigung angefordert, wenn eine andere Komponente darauf wartet, die Sperre zu übernehmen. Die FileTable-Funktion ist eine Komponente, die diesen Wert verwendet.<br /><br /> **Hinweis:** Arbeitsbereiche werden intern verwendet, um Sperren für eingetragene Sitzungen aufzunehmen.|  
|**request_owner_id**|**bigint**|ID des Besitzers dieser Anforderung.<br /><br /> Wenn eine Transaktion der Besitzer der Anforderung ist, enthält dieser Wert die Transaktions-ID.<br /><br /> Wenn eine FileTable der Besitzer der Anforderung, weist **Request_owner_id** verfügt über einen der folgenden Werte.<br /><br /> <br /><br /> -4: eine FileTable hat eine Datenbanksperre übernommen.<br /><br /> -3: eine FileTable hat eine Tabellensperre übernommen.<br /><br /> Anderer Wert: der Wert stellt ein Dateihandle dar. Dieser Wert wird auch als **Fcb_id** in der dynamischen verwaltungssicht [dm_filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).|  
|**request_owner_guid**|**uniqueidentifier**|GUID des Besitzers dieser Anforderung. Wird nur von einer verteilten Transaktion verwendet, wobei der Wert dem MS DTC-GUID für diese Transaktion entspricht.|  
|**request_owner_lockspace_id**|**nvarchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Dieser Wert stellt die sperrenbereich-ID des anforderers dar. Die Sperrenbereich-ID bestimmt, ob zwei Anforderer miteinander kompatibel sind und ob ihnen Sperren in Modi erteilt werden können, die ansonsten zu Konflikten miteinander führen würden.|  
|**lock_owner_address**|**varbinary(8)**|Speicheradresse der internen Datenstruktur, mit der diese Anforderung nachverfolgt wird. Diese Spalte kann verknüpft werden, die mit **Resource_address** Spalte **dm_os_waiting_tasks**.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> <br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
 
## <a name="remarks"></a>Hinweise  
 Der Anforderungsstatus GRANTED gibt an, dass dem Anforderer für eine Ressource eine Sperre erteilt wurde. Der Anforderungsstatus WAITING gibt an, dass die Anforderung noch nicht erteilt wurde. Die folgenden der Anforderungsstatus Waiting Typen werden zurückgegeben, durch die **Request_status** Spalte:  
  
-   Der Anforderungsstatus CONVERT gibt an, dass dem Anforderer bereits eine Anforderung für die Ressource erteilt wurde und dass er derzeit darauf wartet, dass ein Upgrade für die ursprüngliche Anforderung erteilt wird.  
  
-   Der Anforderungsstatus WAIT gibt an, dass der Anforderer derzeit keine erteilte Anforderung für die Ressource besitzt.  
  
 Da **Sys. dm_tran_locks** wird aus internen Sperren-Manager-Datenstrukturen, die Verwaltung dieser Informationen kein zusätzlicher Aufwand für die reguläre Verarbeitung aufgefüllt. Durch das Materialisieren der Sicht ist der Zugriff auf die internen Strukturen des Sperren-Managers erforderlich. Dies kann die reguläre Verarbeitung auf dem Server geringfügig beeinträchtigen. Diese Auswirkungen sollten nicht bemerkbar sein und sollten nur stark ausgelastete Ressourcen betreffen. Die Daten in dieser Sicht entsprechen dem Livestatus des Sperren-Managers. Deshalb können sie jederzeit geändert werden, und Zeilen werden hinzugefügt und entfernt, wenn Sperren eingerichtet und aufgehoben werden. Diese Sicht weist keine Verlaufsinformationen auf.  
  
 Zwei Anforderungen verwenden nur dann dieselbe Ressource, wenn alle Ressourcengruppenspalten identisch sind.  
  
 Sie können das Sperren von Lesevorgängen mit folgenden Tools steuern:  
  
-   SET TRANSACTION ISOLATION LEVEL, um die Ebene von Sperren für eine Sitzung anzugeben. Weitere Informationen finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
-   Sperren von Tabellenhinweisen, um die Ebene von Sperren für einen einzelnen Verweis einer Tabelle in einer FROM-Klausel anzugeben. Informationen zu Syntax und Einschränkungen finden Sie unter [Tabellenhinweise &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Eine Ressource, die unter einer einzelnen Sitzungs-ID ausgeführt wird, kann mehrere erteilte Sperren aufweisen. Unterschiedliche Entitäten, die unter einer Sitzung ausgeführt werden können jeweils besitzen eine Sperre für dieselbe Ressource, und die Informationen werden angezeigt, der **Request_owner_type** und **Request_owner_id** Spalten zurückgegebenes **Sys. dm_tran_locks**. Wenn mehrere Instanzen des gleichen **Request_owner_type** vorhanden sind, die **Request_owner_id** Spalte wird verwendet, um die einzelnen Instanzen voneinander zu unterscheiden. Für verteilte Transaktionen die **Request_owner_type** und **Request_owner_guid** Spalten werden die unterschiedlichen Entitätsinformationen angezeigt.  
  
 Beispielsweise besitzt die Sitzung S1 eine freigegebene Sperre auf **Table1**; und die Transaktion T1, die unter der Sitzung S1 ausgeführt wird, besitzt auch eine freigegebene Sperre für **Table1**. In diesem Fall die **Resource_description** Spalte, die zurückgegebene **Sys. dm_tran_locks** zwei Instanzen derselben Ressource. Die **Request_owner_type** -Spalte zeigt eine Instanz als Sitzung und die andere als eine Transaktion. Darüber hinaus die **Resource_owner_id** Spalte werden verschiedene Werte haben.  
  
 Mehrere Cursor, die unter einer Sitzung ausgeführt werden, können nicht unterschieden werden und werden als eine Einheit behandelt.  
  
 Verteilte Transaktionen, denen kein Sitzungs-ID-Wert zugeordnet ist, sind verwaiste Transaktionen. Diesen wird der Sitzungs-ID-Wert -2 zugewiesen. Weitere Informationen finden Sie unter [KILL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md).  
  
## <a name="resource-details"></a>Ressourcendetails  
 Die folgende Tabelle enthält die Ressourcen, die in angelehnt der **Resource_associated_entity_id** Spalte.  
  
|Ressourcentyp|Ressourcenbeschreibung|Resource_associated_entity_id|  
|-------------------|--------------------------|--------------------------------------|  
|DATABASE|Stellt eine Datenbank dar.|Nicht verfügbar|  
|FILE|Stellt eine Datenbankdatei dar. Bei dieser Datei kann es sich entweder um eine Datendatei oder eine Protokolldatei handeln.|Nicht verfügbar|  
|OBJECT|Stellt ein Datenbankobjekt dar. Bei diesem Objekt kann es sich um eine Datentabelle, eine Sicht, eine gespeicherte Prozedur, eine erweiterte gespeicherte Prozedur oder ein beliebiges Objekt mit einer Objekt-ID handeln.|ObjectID|  
|PAGE|Stellt eine einzelne Seite in einer Datendatei dar.|HoBt-ID. Dieser Wert entspricht **hobt_id**. Die HoBt-ID ist nicht immer für PAGE-Ressourcen verfügbar, weil es sich bei der HoBt-ID um zusätzliche Informationen handelt, die vom Aufrufer bereitgestellt werden können. Dabei sind nicht alle Aufrufer in der Lage, diese Informationen bereitzustellen.|  
|KEY|Stellt eine Zeile in einem Index dar.|HoBt-ID. Dieser Wert entspricht **hobt_id**.|  
|EXTENT|Stellt einen Datendateiblock dar. Ein Block ist eine Gruppe von acht fortlaufenden Seiten.|Nicht verfügbar|  
|RID|Stellt eine physische Zeile in einem Heap dar.|HoBt-ID. Dieser Wert entspricht **hobt_id**. Die HoBt-ID ist nicht immer für RID-Ressourcen verfügbar, weil es sich bei der HoBt-ID um zusätzliche Informationen handelt, die vom Aufrufer bereitgestellt werden können. Dabei sind nicht alle Aufrufer in der Lage, diese Informationen bereitzustellen.|  
|APPLICATION|Stellt eine in einer Anwendung angegebene Ressource dar.|Nicht verfügbar|  
|METADATA|Stellt Metadateninformationen dar.|Nicht verfügbar|  
|HOBT|Stellt einen Heap oder eine B-Struktur dar. Dies sind die grundlegenden Zugriffspfadstrukturen.|HoBt-ID. Dieser Wert entspricht **hobt_id**.|  
|ALLOCATION_UNIT|Stellt zusammenhängende Seiten dar, wie z. B. eine Indexpartition. Jede Zuordnungseinheit deckt eine einzelne IAM-Kette (Index Allocation Map) ab.|Zuordnungseinheit-ID. Dieser Wert entspricht **allocation_unit_id**.|  
  
 In der folgenden Tabelle sind die Untertypen für jeden Ressourcentyp aufgelistet.  
  
|ResourceSubType|Synchronisierte Vorgänge|  
|---------------------|------------------|  
|ALLOCATION_UNIT.BULK_OPERATION_PAGE|Für Massenvorgänge verwendete vorab zugeordnete Seiten.|  
|ALLOCATION_UNIT.PAGE_COUNT|Seitenanzahlstatistiken für Zuordnungseinheiten während verzögerter Löschvorgänge.|  
|DATABASE.BULKOP_BACKUP_DB|Datenbanksicherungen mit Massenvorgängen.|  
|DATABASE.BULKOP_BACKUP_LOG|Datenbankprotokollsicherungen mit Massenvorgängen.|  
|DATABASE.CHANGE_TRACKING_CLEANUP|Cleanuptasks für die Änderungsnachverfolgung.|  
|DATABASE.CT_DDL|Änderungsnachverfolgungs-DDL-Vorgänge auf Datenbank- und Tabellenebene.|  
|DATABASE.CONVERSATION_PRIORITY|Service Broker-Vorgänge mit Konversationspriorität, z. B. CREATE BROKER PRIORITY.|  
|DATABASE.DDL|DDL-Vorgänge (Data Definition Language, Datendefinitionssprache) mit Dateigruppenvorgängen, z. B. Löschvorgängen.|  
|DATABASE.ENCRYPTION_SCAN|TDE-Verschlüsselungssynchronisierung.|  
|DATABASE.PLANGUIDE|Planhinweislisten-Synchronisierung.|  
|DATABASE.RESOURCE_GOVERNOR_DDL|DDL-Vorgänge für Vorgänge der Ressourcenkontrolle, z. B. ALTER RESOURCE POOL.|  
|DATABASE.SHRINK|Datenbankverkleinerungsvorgänge.|  
|DATABASE.STARTUP|Wird zur Synchronisierung des Datenbankstarts verwendet.|  
|FILE.SHRINK|Dateiverkleinerungsvorgänge.|  
|HOBT.BULK_OPERATION|Heapoptimierte Massenladevorgänge mit gleichzeitigen Scanvorgängen unter den folgenden Isolationsstufen: SNAPSHOT, READ UNCOMMITTED und READ COMMITTED mithilfe der Zeilenversionsverwaltung.|  
|HOBT.INDEX_REORGANIZE|Vorgänge zur Heap- oder Indexneuorganisierung.|  
|OBJECT.COMPILE|Kompilierung gespeicherter Prozeduren.|  
|OBJECT.INDEX_OPERATION|Indexvorgänge|  
|OBJECT.UPDSTATS|Statistikupdates für eine Tabelle.|  
|METADATA.ASSEMBLY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROWSET|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_RECV|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_SEND|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_SCOPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Die folgende Tabelle enthält das Format der **Resource_description** Spalte für jeden Ressourcentyp.  
  
|Ressource|Format|Description|  
|--------------|------------|-----------------|  
|DATABASE|Nicht verfügbar|Datenbank-ID steht bereits in der **Resource_database_id** Spalte.|  
|FILE|<file_id>|ID der Datei, die durch diese Ressource dargestellt wird.|  
|OBJECT|<object_id>|ID des Objekts, das durch diese Ressource dargestellt wird. Dieses Objekt kann jedes Objekt, das in aufgeführt sein **sys.objects**, nicht nur eine Tabelle.|  
|PAGE|<file_id>:<page_in_file>|Stellt die Datei-ID und die Seiten-ID der Seite dar, die durch diese Ressource dargestellt wird.|  
|KEY|<hash_value>|Stellt einen Hashwert der Schlüsselspalten aus der Zeile dar, die durch diese Ressource dargestellt wird.|  
|EXTENT|<file_id>:<page_in_files>|Stellt die Datei und die Seiten-ID des Blocks dar, der durch diese Ressource dargestellt wird. Die Block-ID ist mit der Seiten-ID der ersten Seiten des Blocks identisch.|  
|RID|<file_id>:<page_in_file>:<row_on_page>|Stellt die Seiten-ID und die Zeilen-ID der Zeile dar, die durch diese Ressource dargestellt wird. Wenn die zugeordnete Objekt-ID 99 lautet, stellt diese Ressource eine der acht gemischten Seitenslots auf der ersten IAM-Seite einer IAM-Kette dar.|  
|APPLICATION|\<DbPrincipalId >:\<mit maximal 32 Zeichen > :(< Hash_value >)|Stellt die ID des Datenbankprinzipals dar, der für die Bereichsauswahl dieser Anwendungssperrenressource verwendet wird. Außerdem sind bis zu 32 Zeichen aus der Ressourcenzeichenfolge enthalten, die dieser Anwendungssperrenressource entsprechen. In bestimmten Fällen können nur 2 Zeichen angezeigt werden, da die vollständige Zeichenfolge nicht mehr verfügbar ist. Dies tritt nur beim Wiederherstellen der Datenbank für Anwendungssperren auf, die im Rahmen des Wiederherstellungsprozesses erneut abgerufen werden. Der Hashwert stellt einen Hash der vollständigen Ressourcenzeichenfolge dar, die dieser Anwendungssperrenressource entspricht.|  
|HOBT|Nicht verfügbar|HoBt-ID wird als die **Resource_associated_entity_id**.|  
|ALLOCATION_UNIT|Nicht verfügbar|Zuordnungseinheit-ID wird als die **Resource_associated_entity_id**.|  
|METADATA.ASSEMBLY|assembly_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|assembly_id = A, $token_id|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSYMMETRIC_KEY|asymmetric_key_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|audit_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|device_id = D, major_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|audit_specification_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|availability_group_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|certificate_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|object_id = O , compressed_fragment_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROW|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_RECV|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_SEND|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|conversation_priority_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|credential_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|provider_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|data_space_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|endpoint_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|object_id = O, column_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|object_id = O, $hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|fulltext_stoplist_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|index_extension_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|object_id = O, index_id oder stats_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|user_type_id = U, hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|message_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|function_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|class = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|plan_guide_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_HASH|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_SCOPE|scope_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|$qname_scope_id = Q, $qname_hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|remote_service_binding_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|route_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|schema_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|sd_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|$seq_type = S, object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER|server_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|event_session_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|service_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|service_contract_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|message_type_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|object_id = O, stats_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|symmetric_key_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|user_type_id = U|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|xml_collection_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|xml_component_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|object_id = O, $qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Die folgenden XEvents beziehen sich auf Partition **SWITCH** und Neuerstellung von Onlineindizes. Weitere Informationen zur Syntax finden Sie unter [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) und [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Das vorhandene XEvent **Progress_report_online_index_operation** für Onlineindexvorgänge wurde erweitert, Vorgänge durch Hinzufügen von **Partition_number** und **Partition_id**.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-sysdmtranlocks-with-other-tools"></a>A. Verwenden von sys.dm_tran_locks mit anderen Tools  
 Im folgenden Beispiel wird ein Updatevorgang durch eine andere Transaktion blockiert. Mithilfe von **Sys. dm_tran_locks** und anderen Tools werden Informationen zum Sperren von Ressourcen bereitgestellt.  
  
```sql  
USE tempdb;  
GO  
  
-- Create test table and index.  
CREATE TABLE t_lock  
    (  
    c1 int, c2 int  
    );  
GO  
  
CREATE INDEX t_lock_ci on t_lock(c1);  
GO  
  
-- Insert values into test table  
INSERT INTO t_lock VALUES (1, 1);  
INSERT INTO t_lock VALUES (2,2);  
INSERT INTO t_lock VALUES (3,3);  
INSERT INTO t_lock VALUES (4,4);  
INSERT INTO t_lock VALUES (5,5);  
INSERT INTO t_lock VALUES (6,6);  
GO  
  
-- Session 1  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
  
BEGIN TRAN  
    SELECT c1  
        FROM t_lock  
        WITH(holdlock, rowlock);  
  
-- Session 2  
BEGIN TRAN  
    UPDATE t_lock SET c1 = 10  
```  
  
 Mit der folgenden Abfrage werden Sperrinformationen angezeigt. Der Wert für `<dbid>` ersetzt werden sollte, mit der **Database_id** aus **sys.databases**.  
  
```sql  
SELECT resource_type, resource_associated_entity_id,  
    request_status, request_mode,request_session_id,  
    resource_description   
    FROM sys.dm_tran_locks  
    WHERE resource_database_id = <dbid>  
```  
  
 Die folgende Abfrage gibt Objektinformationen mithilfe des Wertes von `resource_associated_entity_id` aus der vorherigen Abfrage zurück. Die Abfrage muss ausgeführt werden, während Sie mit der Datenbank verbunden sind, die das Objekt enthält.  
  
```  
SELECT object_name(object_id), *  
    FROM sys.partitions  
    WHERE hobt_id=<resource_associated_entity_id>  
```  
  
 Die folgende Abfrage zeigt Blockierungsinformationen an.  
  
```sql  
SELECT   
        t1.resource_type,  
        t1.resource_database_id,  
        t1.resource_associated_entity_id,  
        t1.request_mode,  
        t1.request_session_id,  
        t2.blocking_session_id  
    FROM sys.dm_tran_locks as t1  
    INNER JOIN sys.dm_os_waiting_tasks as t2  
        ON t1.lock_owner_address = t2.resource_address;  
```  
  
 Die Ressourcen werden freigegeben, indem ein Rollback für die Transaktionen ausgeführt wird.  
  
```sql  
-- Session 1  
ROLLBACK;  
GO  
  
-- Session 2  
ROLLBACK;  
GO  
```  
  
### <a name="b-linking-session-information-to-operating-system-threads"></a>B. Verknüpfen von Sitzungsinformationen mit Betriebssystemthreads  
 Das folgende Beispiel gibt Informationen zurück, die eine Sitzungs-ID einer Windows-Thread-ID zuordnen. Die Leistung des Threads kann im Windows-Systemmonitor überwacht werden. Diese Abfrage gibt keine Sitzungs-IDs zurück, die derzeit deaktiviert sind.  
  
```sql  
SELECT STasks.session_id, SThreads.os_thread_id  
    FROM sys.dm_os_tasks AS STasks  
    INNER JOIN sys.dm_os_threads AS SThreads  
        ON STasks.worker_address = SThreads.worker_address  
    WHERE STasks.session_id IS NOT NULL  
    ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_tran_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
