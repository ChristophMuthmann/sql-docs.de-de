---
title: Sp_addmergearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords:
- sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d60ceb96dfaf5f690a8485c74648707da0ae59ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einer vorhandenen Mergeveröffentlichung einen Artikel hinzu. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, die den Artikel enthält. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=** ] **"***Artikel***"**  
 Der Name des Artikels. Der Name muss innerhalb der Veröffentlichung eindeutig sein. *Artikel* ist **Sysname**, hat keinen Standardwert. *Artikel* muss auf dem lokalen Computer mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und den Regeln für Bezeichner entsprechen.  
  
 [  **@source_object=** ] **"***Source_object***"**  
 Entspricht dem zu veröffentlichenden Datenbankobjekt. *Source_object* ist **Sysname**, hat keinen Standardwert. Weitere Informationen zu den Objekttypen, die mithilfe der Mergereplikation veröffentlicht werden können, finden Sie unter [Veröffentlichen von Daten und Datenbankobjekte](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [ **@type=** ] **'***type***'**  
 Entspricht dem Artikeltyp. *Typ* ist **Sysname**, hat den Standardwert **Tabelle**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Tabelle** (Standard)|Tabelle mit Schema und Daten. Die Replikation überwacht die Tabelle, um die zu replizierenden Daten zu ermitteln.|  
|**nur Func schema**|Funktion vom Typ schema only.|  
|**indizierte Sicht** **nur Schema**|Indizierte Sicht vom Typ schema only.|  
|**Proc Schema nur**|Nur gespeicherte Prozedur mit Schema|  
|**nur Synonymschema**|Nur Synonym mit Schema|  
|**nur Schema anzeigen**|Sicht vom Typ schema only.|  
  
 [  **@description=** ] **"***Beschreibung***"**  
 Eine Beschreibung des Artikels. *Beschreibung* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@column_tracking=** ] **"***Column_tracking***"**  
 Entspricht der Einstellung für die Nachverfolgung auf Spaltenebene. *Column_tracking* ist **nvarchar(10)**, hat den Standardwert "false". **"true"** spaltennachverfolgung aktiviert. **"false"** deaktiviert die spaltennachverfolgung und belässt die konflikterkennung auf Zeilenebene. Wenn die Tabelle bereits in anderen Mergereplikationen veröffentlicht ist, müssen Sie denselben Wert für die Spaltenprotokollierung verwenden, der von bereits bestehenden Artikeln für diese Tabelle verwendet wird. Dieser Parameter ist nur für Tabellenartikel spezifisch.  
  
> [!NOTE]  
>  Falls die Zeilennachverfolgung zur Konflikterkennung verwendet wird (Standardeinstellung), kann die Basistabelle maximal 1.024 Spalten enthalten. Die Spalten müssen jedoch im Artikel gefiltert werden, sodass maximal 246 Spalten veröffentlicht werden. Wenn Spaltennachverfolgung verwendet wird, kann die Basistabelle maximal 246 Spalten enthalten.  
  
 [  **@status=** ] **"***Status***"**  
 Entspricht dem Status des Artikels. *Status* ist **nvarchar(10)**, hat den Standardwert **unsynced**. Wenn **active**, das Anfangsverarbeitungsskript zum Veröffentlichen der Tabelle ausgeführt wird. Wenn **unsynced**, wird das Anfangsverarbeitungsskript zum Veröffentlichen der Tabelle bei der nächsten Ausführung der Momentaufnahme-Agent wird ausgeführt.  
  
 [  **@pre_creation_cmd=** ] **"***Pre_creation_cmd***"**  
 Gibt den Vorgang an, der vom System auszuführen ist, wenn bei Übernahme der Momentaufnahme die Tabelle auf Abonnentenebene vorhanden ist. *Pre_creation_cmd* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Keine**|Wenn die Tabelle bereits auf dem Abonnenten vorhanden ist, wird keine Aktion ausgeführt.|  
|**Löschen**|Ein Löschvorgang wird auf der Grundlage der WHERE-Klausel im Teilmengenfilter ausgegeben.|  
|**Drop** (Standard)|Die Tabelle wird vor dem erneuten Erstellen gelöscht. Zur Unterstützung von erforderlich [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten.|  
|**truncate**|Schneidet die Zieltabelle ab.|  
  
 [  **@creation_script=** ] **"***Creation_script***"**  
 Entspricht dem Pfad und Namen eines optionalen Artikelschemaskripts, mit dem der Artikel in der Abonnementdatenbank erstellt wird. *Creation_script* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Erstellungsskripts werden auf [!INCLUDE[ssEW](../../includes/ssew-md.md)]-Abonnenten nicht ausgeführt.  
  
 [  **@schema_option=** ] *Schema_option*  
 Ist eine Bitmap der Schemagenerierungsoption für den angegebenen Artikel. *Schema_option* ist **binary(8)**, und kann die [| (Bitweises OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) Produkt eine oder mehrere der folgenden Werte sind.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0 x 00**|Deaktiviert die Skripterstellung durch den Momentaufnahme-Agent und verwendet das bereitgestellte Schemaskript zur Voraberstellung eines definiert *Creation_script*.|  
|**0 x 01**|Generiert die Objekterstellung (CREATE TABLE, CREATE PROCEDURE usw.). Dieser Wert ist der Standardwert für alle Artikel mit gespeicherten Prozeduren.|  
|**0 x 10**|Generiert einen entsprechenden gruppierten Index. Auch wenn diese Option nicht festgelegt ist, werden Indizes bezüglich der Primärschlüssel und der UNIQUE-Einschränkungen generiert, falls diese für eine veröffentlichte Tabelle bereits definiert sind.|  
|**0 x 20**|Konvertiert benutzerdefinierte Datentypen (UDT) auf dem Abonnenten in Basisdatentypen. Diese Option kann nicht verwendet werden, wenn eine CHECK- oder DEFAULT-Einschränkung für eine UDT-Spalte vorhanden ist, wenn eine UDT-Spalte Teil des Primärschlüssels ist oder wenn eine berechnete Spalte auf eine UDT-Spalte verweist.|  
|**0 x 40**|Generiert entsprechende nicht gruppierte Indizes. Auch wenn diese Option nicht festgelegt ist, werden Indizes bezüglich der Primärschlüssel und der UNIQUE-Einschränkungen generiert, falls diese für eine veröffentlichte Tabelle bereits definiert sind.|  
|**0 x 80**|Repliziert PRIMARY KEY-Einschränkungen. Alle Indizes bezüglich der Einschränkung werden ebenfalls repliziert, auch wenn Optionen **0 x 10** und **0 x 40** sind nicht aktiviert.|  
|**0 x 100**|Repliziert Benutzertrigger für einen Tabellenartikel, wenn definiert.|  
|**0 x 200**|Repliziert FOREIGN KEY-Einschränkungen. Wenn die Tabelle, auf die verwiesen wird, nicht Teil einer Veröffentlichung ist, werden für eine veröffentlichte Tabelle keine FOREIGN KEY-Einschränkungen repliziert.|  
|**0 x 400**|Repliziert CHECK-Einschränkungen.|  
|**0 x 800**|Repliziert Standards.|  
|**0 x 1000**|Repliziert die Sortierung auf Spaltenebene.|  
|**0 x 2000**|Repliziert erweiterte Eigenschaften, die dem Quellobjekt des veröffentlichten Artikels zugeordnet sind.|  
|**0 x 4000**|Repliziert UNIQUE-Einschränkungen. Alle Indizes bezüglich der Einschränkung werden ebenfalls repliziert, auch wenn Optionen **0 x 10** und **0 x 40** sind nicht aktiviert.|  
|**0 x 8000**|Diese Option ist für Verleger, auf denen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher ausgeführt wird, nicht gültig.|  
|**0 x 10000**|Repliziert CHECK-Einschränkungen als NOT FOR REPLICATION, sodass die Einschränkungen während der Synchronisierung nicht erzwungen werden.|  
|**0 x 20000**|Repliziert FOREIGN KEY-Einschränkungen als NOT FOR REPLICATION, sodass diese Einschränkungen bei der Synchronisierung nicht erzwungen werden.|  
|**0 x 40000**|Repliziert Dateigruppen, die mit einer partitionierten Tabelle oder einem Index verbunden sind.|  
|**0 x 80000**|Repliziert das Partitionsschema für eine partitionierte Tabelle.|  
|**0 x 100000**|Repliziert das Partitionsschema für einen partitionierten Index.|  
|**0 x 200000**|Repliziert Tabellenstatistiken.|  
|**0 x 400000**|Repliziert Standardbindungen.|  
|**0 x 800000**|Repliziert regelbindungen.|  
|**0 x 1000000**|Repliziert den Volltextindex.|  
|**0x2000000**|XML-schemaauflistungen gebunden **Xml** Spalten werden nicht repliziert.|  
|**0x4000000**|Repliziert Indizes für **Xml** Spalten.|  
|**0x8000000**|Erstellt Schemas, die noch nicht auf dem Abonnenten vorhanden sind.|  
|**0 x 10000000**|Konvertiert **Xml** Spalten **Ntext** auf dem Abonnenten.|  
|**0 x 20000000**|Konvertiert, die große Objekttypen Daten (**nvarchar(max)**, **varchar(max)**, und **varbinary(max)**) eingeführten [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Datentypen, die auf unterstütztwerden[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0 x 40000000**|Repliziert Berechtigungen.|  
|**0 x 80000000**|Versucht, Abhängigkeiten von Objekten zu löschen, die nicht Teil der Veröffentlichung sind.|  
|**0 x 100000000**|Mit dieser Option können Sie das FILESTREAM-Attribut replizieren, wenn er für angegeben wird **varbinary(max)** Spalten. Geben Sie diese Option nicht an, wenn Sie Tabellen auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Abonnenten replizieren. Replizieren von Tabellen mit FILESTREAM-Spalten auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] -Abonnenten wird unabhängig von der Festlegung dieser Schemaoption nicht unterstützt. Siehe die verwandte Option **0 x 800000000**.|  
|**0x200000000**|Datum und Uhrzeit-Datentypen konvertiert (**Datum**, **Zeit**, **"DateTimeOffset"**, und **datetime2**) eingeführten [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] an Daten die in früheren Versionen von unterstützten Basisdatentypen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Repliziert die Komprimierungsoption für Daten und Indizes. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0 x 800000000**|Legen Sie diese Option fest, um FILESTREAM-Daten in einer eigenen Dateigruppe auf dem Abonnenten zu speichern. Wenn diese Option nicht festgelegt wird, werden FILESTREAM-Daten in der Standarddateigruppe gespeichert. Bei der Replikation werden keine Dateigruppen erstellt. Daher müssen Sie beim Festlegen dieser Option die Dateigruppe erstellen, bevor Sie die Momentaufnahme auf dem Abonnenten anwenden. Weitere Informationen zum Erstellen von Objekten vor dem Anwenden der Momentaufnahme finden Sie unter [Ausführen von Skripts vor und nach der Momentaufnahme angewendet wird](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Siehe die verwandte Option **0 x 100000000**.|  
|**0x1000000000**|Konvertiert von common Language Runtime (CLR) eine benutzerdefinierte Typen (UDTs) in **varbinary(max)** , sodass Spalten vom Typ UDT auf Abonnenten repliziert werden können, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Konvertiert die **Hierarchyid** Datentyp, **varbinary(max)** sodass Spalten vom Typ **Hierarchyid** repliziert werden können, an die Abonnenten, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Weitere Informationen zur Verwendung von **Hierarchyid** -Spalten in replizierten Tabellen finden Sie unter [Hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Repliziert die gefilterten Indizes in der Tabelle. Weitere Informationen zu gefilterten Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Konvertiert die **Geography** und **Geometrie** Datentypen zu **varbinary(max)** , sodass Spalten dieser Typen auf Abonnenten repliziert werden können, die ausgeführtwerden[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Repliziert Indizes für Spalten vom Typ **Geography** und **Geometrie**.|  
  
 Bei einem Wert von NULL generiert das System automatisch eine gültige Schemaoption für den Artikel. Die **Standardschemaoptionen** Tabelle im Abschnitt "Hinweise" werden die Werte aufgeführt, die ausgewählt wird basierend auf dem Artikeltyp. Außerdem sind nicht alle *Schema_option* sind Werte für alle Replikations- oder Artikeltyp gültig. Die **gültige Schemaoption** in den Hinweisen angegebene Tabelle zeigt die Optionen, die für einen bestimmten Artikeltyp angegeben werden können.  
  
> [!NOTE]  
>  Die *Schema_option* Parameter wirkt sich nur auf Replikationsoptionen für die anfangsmomentaufnahme. Nachdem das anfangsschema vom Momentaufnahme-Agent generiert und auf dem Abonnenten angewendet wurde, für die Replikation von veröffentlichungsschemaänderungen auf dem Abonnenten basierend auf Schema Replikationsregeln ausgeführt und die *Replicate_ddl* im angegebenen parametereinstellung [Sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 [  **@subset_filterclause=** ] **"***Subset_filterclause***"**  
 Entspricht einer WHERE-Klausel, die die horizontale Filterung eines Tabellenartikels ohne das Wort WHERE angibt. *Subset_filterclause* vom **nvarchar(1000)**, Standardwert ist eine leere Zeichenfolge.  
  
> [!IMPORTANT]  
>  Aus Leistungsgründen ist es empfehlenswert, keine Funktionen auf Spaltennamen in Klauseln für parametrisierte Zeilenfilter anzuwenden, wie z. B. `LEFT([MyColumn]) = SUSER_SNAME()`. Bei Verwendung von [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) in einer Filterklausel verwenden und den Wert HOST_NAME überschreiben, müssen Sie möglicherweise Datentypen mithilfe von convert [konvertieren](../../t-sql/functions/cast-and-convert-transact-sql.md). Weitere Informationen zu bewährten Methoden für diesen Fall finden Sie im Abschnitt "Überschreiben des Host_name()-Werts""in [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@article_resolver=** ] **"***Article_resolver***"**  
 Entspricht dem COM-basierte Konfliktlöser, mit dem Konflikte auf Ebene des Tabellenartikels oder der .NET Framework-Assembly gelöst werden. Diese wird aufgerufen, um eine benutzerdefinierte Geschäftslogik auf Ebene des Tabellenartikels auszuführen. *Article_resolver* ist **varchar(255)**, hat den Standardwert NULL. Verfügbare Werte für diesen Parameter sind im Abschnitt zu benutzerdefinierten Konfliktlösern von [!INCLUDE[msCoName](../../includes/msconame-md.md)] aufgelistet. Wenn der bereitgestellte Wert nicht zu den Konfliktlösern von [!INCLUDE[msCoName](../../includes/msconame-md.md)] zählt, dann verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den angegebenen Konfliktlöser anstelle des vom System bereitgestellten Konfliktlösers. Verwendung **Sp_enumcustomresolvers** zum Aufzählen der Liste der verfügbaren benutzerdefinierten Konfliktlöser. Weitere Informationen finden Sie unter [führen Business Logic während der Mergesynchronisierung](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md) und [Advanced Merge Replication Conflict Detection und Auflösung](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 [  **@resolver_info=** ] **"***Resolver_info***"**  
 Wird für die Angabe zusätzlicher Informationen verwendet, die für einen benutzerdefinierten Konfliktlöser erforderlich sind. Einige der [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Konfliktlöser erfordern eine Spalte, die als Eingabe für den Konfliktlöser dient. *Resolver_info* ist **nvarchar(255)**, hat den Standardwert NULL. Weitere Informationen finden Sie unter [Microsoft COM-basierte Konfliktlöser](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 [  **@source_owner=** ] **"***der Standardwert***"**  
 Der Name des Besitzers der *Source_object*. *Der Standardwert* ist **Sysname**, hat den Standardwert NULL. Bei NULL wird der aktuelle Benutzer als Besitzer angenommen.  
  
 [  **@destination_owner=** ] **"***Destination_owner***"**  
 Entspricht dem Besitzer des Objekts in der Abonnementdatenbank (sofern nicht "dbo" angegeben ist). *Destination_owner* ist **Sysname**, hat den Standardwert NULL. Bei NULL wird dbo als Besitzer angenommen.  
  
 [  **@vertical_partition=** ] **"***Column_filter***"**  
 Aktiviert und deaktiviert die Spaltenfilterung für einen Tabellenartikel. *Vertical_partition* ist **nvarchar(5)** hat den Standardwert "false".  
  
 **"false"** zeigt an, dass keine vertikale Filterung und alle Spalten veröffentlicht.  
  
 **"true"** löscht alle Spalten außer dem deklarierten Primärschlüssel und ROWGUID-Spalten. Spalten werden mit hinzugefügt **Sp_mergearticlecolumn**.  
  
 [  **@auto_identity_range=** ] **"***Automatic_identity_range***"**  
 Aktiviert und deaktiviert auf Veröffentlichungsebene die automatische Handhabung von Identitätsbereichen für diesen Tabellenartikel zum Zeitpunkt der Veröffentlichungserstellung. *Auto_identity_range* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** ermöglicht automatische Identitätsbereich Behandlung die, zwar **"false"** deaktiviert sie.  
  
> [!NOTE]  
>  *Auto_identity_range* ist veraltet und wird nur für Abwärtskompatibilität bereitgestellt. Verwenden Sie *Identityrangemanagementoption* zum Verwaltungsoptionen für Identitätsbereiche angeben. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range=** ] *pub_identity_range-Spalte*  
 Steuert die Identitätsbereichsgröße, die einem Abonnenten mit einem Serverabonnement zugeordnet ist, wenn die automatische Identitätsbereichsverwaltung verwendet wird. Dieser Identitätsbereich ist für einen Wiederveröffentlichungsabonnenten für die Zuordnung zu dessen Abonnenten reserviert. *Pub_identity_range* ist **"bigint"**, hat den Standardwert NULL. Sie müssen diesen Parameter angeben, wenn *Identityrangemanagementoption* ist **Auto** oder, wenn *Auto_identity_range* ist **"true"**.  
  
 [  **@identity_range=** ] *Identity_range*  
 Steuert die Größe des Identitätsbereichs, die sowohl dem Verleger als auch dem Abonnenten zugeordnet wird, wenn die automatische Identitätsbereichsverwaltung verwendet wird. *Identity_range* ist **"bigint"**, hat den Standardwert NULL. Sie müssen diesen Parameter angeben, wenn *Identityrangemanagementoption* ist **Auto** oder, wenn *Auto_identity_range* ist **"true"**.  
  
> [!NOTE]  
>  *Identity_range* steuert die identitätsbereichsgröße bei Wiederveröffentlichungsabonnenten, die mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@threshold=** ] *Schwellenwert*  
 Prozentwert, der steuert, wann der Merge-Agent einen neuen Identitätsbereich zuweist. Wenn der Prozentsatz der Werte angegeben, *Schwellenwert* wird verwendet, erstellt der Merge-Agent einen neuen Identitätsbereich. *Schwellenwert für* ist **Int**, hat den Standardwert NULL. Sie müssen diesen Parameter angeben, wenn *Identityrangemanagementoption* ist **Auto** oder, wenn *Auto_identity_range* ist **"true"**.  
  
 [  **@verify_resolver_signature=** ] *Verify_resolver_signature*  
 Gibt an, ob eine digitale Signatur vor dem Verwenden eines Konfliktlösers in der Mergereplikation überprüft wird. *Verify_resolver_signature* ist **Int**, hat den Standardwert 1.  
  
 **0** gibt an, dass die Signatur nicht überprüft wird.  
  
 **1** gibt an, dass die Signatur überprüft wird, um festzustellen, ob sie aus einer vertrauenswürdigen Quelle stammt.  
  
 [  **@destination_object=** ] **"***Destination_object***"**  
 Entspricht dem Namen des Objekts in der Abonnementdatenbank. *Destination_object* ist **Sysname**, hat den Standardwert des **@source_object**. Dieser Parameter kann nur angegeben werden, wenn der Artikel vom Typ schema only ist, wie z. B. ein Artikel für gespeicherte Prozeduren, Sichten und UDFs. Wenn der Artikel angegebene einen Tabellenartikel, der Wert in *@source_object* überschreibt den Wert in *Destination_object*.  
  
 [  **@allow_interactive_resolver=** ] **"***Allow_interactive_resolver***"**  
 Aktiviert oder deaktiviert die Verwendung des interaktiven Konfliktlösers für einen Artikel. *Allow_interactive_resolver* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** ermöglicht die Verwendung des interaktiven Konfliktlösers für den Artikel. **"false"** deaktiviert sie.  
  
> [!NOTE]  
>  Der interaktive Konfliktlöser wird von [!INCLUDE[ssEW](../../includes/ssew-md.md)]-Abonnenten nicht unterstützt.  
  
 [  **@fast_multicol_updateproc=** ] **"***Fast_multicol_updateproc***"**  
 Dieser Parameter wurde als veraltet markiert und wird aus Gründen der Abwärtskompatibilität von Skripts beibehalten.  
  
 [  **@check_permissions=** ] *Check_permissions*  
 Ein Bitmuster der Berechtigungen auf Tabellenebene, die überprüft werden, wenn der Merge-Agent die Änderungen auf dem Verleger anwendet. Wenn der vom Mergeprozess verwendete Benutzername bzw. das Benutzerkonto auf dem Verleger nicht über die entsprechenden Tabellenberechtigungen verfügt, werden die ungültigen Änderungen als Konflikte protokolliert. *Check_permissions* ist **Int**, und kann die [| (Bitweises OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) Produkt eine oder mehrere der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0 x 00** (Standard)|Berechtigungen werden nicht überprüft.|  
|**0 x 10**|Überprüft Berechtigungen auf dem Verleger, bevor auf einem Abonnenten ausgeführte Einfügevorgänge hochgeladen werden können.|  
|**0 x 20**|Überprüft Berechtigungen auf dem Verleger, bevor auf einem Abonnenten ausgeführte Updatevorgänge hochgeladen werden können.|  
|**0 x 40**|Überprüft Berechtigungen auf dem Verleger, bevor auf einem Abonnenten ausgeführte Löschvorgänge hochgeladen werden können.|  
  
 [  **@force_invalidate_snapshot=** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert 0.  
  
 **0** gibt an, dass durch Hinzufügen eines Artikels nicht die Momentaufnahme ungültig werden kann. Wenn die gespeicherte Prozedur erkennt, dass die Änderungen eine neue Momentaufnahme erfordern, tritt ein Fehler auf und es werden keine Änderungen vorgenommen.  
  
 **1** gibt an, dass durch Hinzufügen eines Artikels kann dazu führen, dass die Momentaufnahme ungültig wird, und wenn es sind Abonnements vorhanden, die eine neue Momentaufnahme erfordern die Berechtigung erteilt, für die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme zu generieren. *Force_invalidate_snapshot* festgelegt ist, um **1** beim Hinzufügen eines Artikels einer Veröffentlichung mit einer vorhandenen Momentaufnahme.  
  
 [  **@published_in_tran_pub=** ] **"***Published_in_tran_pub***"**  
 Gibt an, dass ein Artikel in einer Mergeveröffentlichung auch in einer Transaktionsveröffentlichung veröffentlicht wird. *Published_in_tran_pub* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** gibt an, dass der Artikel auch in einer transaktionsveröffentlichung veröffentlicht wird.  
  
 [  **@force_reinit_subscription=** ] *Force_reinit_subscription*  
 Bestätigt, dass die von dieser gespeicherten Prozedur ausgeführte Aktion die erneute Initialisierung vorhandener Abonnements erfordern kann. *Force_reinit_subscription* ist ein **Bit**, hat den Standardwert 0.  
  
 **0** gibt an, dass durch Hinzufügen eines Artikels nicht das Abonnement erneut initialisiert werden kann. Wenn die gespeicherte Prozedur erkennt, dass die Änderung die Neuinitialisierung vorhandener Abonnements erfordert, tritt ein Fehler auf, und es werden keine Änderungen durchgeführt.  
  
 **1** bedeutet, dass am Mergeartikel Änderungen erneute Initialisierung vorhandener Abonnements erneut initialisiert werden, und die Berechtigung für den erneuten Initialisierung der Abonnements erteilt. *Force_reinit_subscription* festgelegt ist, um **1** Wenn *Subset_filterclause* einen parametrisierten Zeilenfilter angibt.  
  
 [  **@logical_record_level_conflict_detection=** ] **"***Logical_record_level_conflict_detection***"**  
 Gibt die Ebene der Konflikterkennung für einen Artikel an, der das Element eines logischen Datensatzes ist. *Logical_record_level_conflict_detection* ist **nvarchar(5)**, hat den Standardwert "false".  
  
 **"true"** gibt an, dass ein Konflikt erkannt wird, wenn Änderungen an einer beliebigen Stelle im logischen Datensatz vorgenommen werden.  
  
 **"false"** gibt an, dass die standardkonflikterkennung verwendet wird, nach den Angaben von *Column_tracking*. Weitere Informationen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Da logische Datensätze von nicht unterstützt werden [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten, geben Sie einen Wert von **"false"** für *Logical_record_level_conflict_detection* um diese Abonnenten zu unterstützen.  
  
 [  **@logical_record_level_conflict_resolution=** ] **"***Logical_record_level_conflict_resolution***"**  
 Gibt die Ebene der Konfliktlösung für einen Artikel an, der das Element eines logischen Datensatzes ist. *Logical_record_level_conflict_resolution* ist **nvarchar(5)**, hat den Standardwert "false".  
  
 **"true"** gibt an, dass der gesamte gewinnende logische Datensatz den verlierenden logischen Datensatz überschrieben.  
  
 **"false"** gibt an, dass gewinnerzeilen nicht auf den logischen Datensatz eingeschränkt sind. Wenn *Logical_record_level_conflict_detection* ist **"true"**, klicken Sie dann *Logical_record_level_conflict_resolution* muss ebenfalls festgelegt werden, um **"true"**. Weitere Informationen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Da logische Datensätze von nicht unterstützt werden [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten, geben Sie einen Wert von **"false"** für *Logical_record_level_conflict_resolution* um diese Abonnenten zu unterstützen.  
  
 [  **@partition_options=** ] *Partition_options*  
 Definiert die Art und Weise, wie Daten im Artikel partitioniert werden. Dies ermöglicht Leistungsoptimierungen, wenn alle Zeilen nur zu einer einzigen Partition oder zu einem einzigen Abonnement gehören. *Partition_options* ist **"tinyint"**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0** (Standardwert)|Das Filtern für den Artikel ist entweder statisch oder ergibt keine eindeutige Untermenge von Daten für jede Partition, d. h. eine "überlappende" Partition.|  
|**1**|Die Partitionen überlappen, und beim Abonnenten vorgenommene Updates der Datenbearbeitungssprache (DML, Data Manipulation Language) können nicht die Partition ändern, zu der eine Zeile gehört.|  
|**2**|Das Filtern für den Artikel ergibt nicht überlappende Partitionen. Mehrere Abonnenten können jedoch die gleiche Partition erhalten.|  
|**3**|Das Filtern für den Artikel ergibt nicht überlappende Partitionen, die für jedes Abonnement eindeutig sind.|  
  
> [!NOTE]  
>  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, und klicken Sie dann auf den Wert des veröffentlicht wurde *Partition_options* muss für beide Artikel gleich sein.  
  
 [  **@processing_order=** ] *Processing_order*  
 Gibt die Verarbeitungsreihenfolge von Artikeln in einer Mergeveröffentlichung an. *Processing_order* ist **Int**, hat den Standardwert 0. **0** gibt an, dass der Artikel nicht sortiert ist, und jeder andere Wert stellt den Ordnungswert der Verarbeitungsreihenfolge von Artikeln für diesen Artikel dar. Artikel werden in der Reihenfolge vom niedrigsten zum höchsten Wert verarbeitet. Wenn zwei Artikel denselben Wert haben, Verarbeitungsreihenfolge von Artikeln hängt von der Reihenfolge des artikelspitznamens in der [Sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) -Systemtabelle. Weitere Informationen finden Sie unter [Angeben der Verarbeitungsreihenfolge von Mergeartikeln](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
 [  **@subscriber_upload_options=** ] *Subscriber_upload_options*  
 Definiert Einschränkungen für Updates, die bei einem Abonnenten mit einem Clientabonnement vorgenommen werden. Weitere Informationen finden Sie unter [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md). *Subscriber_upload_options* ist **"tinyint"**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0** (Standardwert)|Keine Einschränkungen. Auf dem Abonnenten vorgenommene Änderungen werden auf den Verleger hochgeladen.|  
|**1**|Änderungen sind auf dem Abonnenten zulässig, werden jedoch nicht auf den Verleger hochgeladen.|  
|**2**|Änderungen sind auf dem Abonnenten nicht zulässig.|  
  
 Ändern von *Subscriber_upload_options* muss das Abonnement durch Aufrufen von bewirken [Sp_reinitmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md).  
  
> [!NOTE]  
>  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, den Wert des veröffentlicht wurde *Subscriber_upload_options* muss für beide Artikel gleich sein.  
  
 [  **@identityrangemanagementoption=** ] *Identityrangemanagementoption*  
 Gibt an, wie die Identitätsbereichsverwaltung für den Artikel gehandhabt wird. *Identityrangemanagementoption* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Keine**|Deaktiviert die Verwaltung des Identitätsbereichs.|  
|**Manuell**|Markiert die Identitätsspalte mithilfe von NOT FOR REPLICATION, um die manuelle Identitätsbereichsverwaltung zu ermöglichen.|  
|**Auto**|Gibt die automatisierte Verwaltung von Identitätsbereichen an.|  
|Null(Default)|Wird standardmäßig auf **keine**Wenn der Wert der *Auto_identity_range* nicht **"true"**.|  
  
 Für die Abwärtskompatibilität bei den Wert der *Identityrangemanagementoption* NULL ist, den Wert der *Auto_identity_range* aktiviert ist. Jedoch, wenn der Wert der *Identityrangemanagementoption* ist nicht NULL, und klicken Sie dann auf den Wert der *Auto_identity_range* wird ignoriert. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@delete_tracking=** ] **"***Delete_tracking***"**  
 Gibt an, ob Löschungen repliziert werden. *Delete_tracking* ist **nvarchar(5)**, Standardwert ist "true". **"false"** gibt an, dass Löschvorgänge nicht repliziert werden, und **"true"** gibt an, dass Löschvorgänge repliziert werden, dies ist das übliche Verhalten für die Mergereplikation. Wenn *Delete_tracking* festgelegt ist, um **"false"**, auf dem Abonnenten gelöschte Zeilen müssen manuell entfernt werden, auf dem Verleger und auf dem Verleger gelöschte Zeilen müssen manuell entfernt werden, auf dem Abonnenten.  
  
> [!IMPORTANT]  
>  Festlegen von *Delete_tracking* auf **"false"** führt zu einer Nichtkonvergenz. Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, und klicken Sie dann auf den Wert des veröffentlicht wurde *Delete_tracking* muss für beide Artikel gleich sein.  
  
> [!NOTE]  
>  *Delete_tracking* Optionen können nicht festgelegt werden, mithilfe der **Assistenten für neue Veröffentlichung** oder **Veröffentlichungseigenschaften** (Dialogfeld).  
  
 [  **@compensate_for_errors=** ] **"***Compensate_for_errors***"**  
 Zeigt an, ob kompensierende Aktionen ausgeführt werden, wenn während der Synchronisierung Fehler auftreten. *Compensate_for_errors ich*s **nvarchar(5)**, hat den Standardwert "false". Bei Festlegung auf **"true"**, ändert, kann nicht auf einem Abonnenten angewendet werden oder Verlegerebene während der Synchronisierung immer führen zu kompensierenden Aktionen, um die Änderung rückgängig zu machen; allerdings ein Abonnent, kann ein Fehler generiert, falsch konfiguriert Führen Sie die Änderungen an andere Abonnenten und Verlegern rückgängig gemacht werden. **"false"** deaktiviert diese kompensierenden Aktionen, die Fehler dennoch protokolliert werden, wie mit der Kompensierung und nachfolgenden Mergevorgängen weiterhin versucht, die Änderungen bis dies erfolgreich angewendet.  
  
> [!IMPORTANT]  
>  Möglicherweise hat es den Anschein, dass Daten in den betroffenen Zeilen nicht konvergent sind. Beheben Sie jedoch ggf. aufgetretene Fehler, können Änderungen übernommen werden, und die Daten konvergieren. Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, und klicken Sie dann auf den Wert des veröffentlicht wurde *Compensate_for_errors* muss für beide Artikel gleich sein.  
  
 [  **@stream_blob_columns=** ] **"***Stream_blob_columns***"**  
 Gibt an, dass eine Datenstromoptimierung bei der Replikation von Binary Large Object-Spalten verwendet wird. *Stream_blob_columns* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** bedeutet, dass die Optimierung versucht wird. *Stream_blob_columns* festgelegt ist, auf "true", wenn FILESTREAM aktiviert ist. Dadurch werden die Replikation der FILESTREAM-Daten optimal ausgeführt und die Arbeitsspeicherauslastung reduziert. Verwenden Sie zum Erzwingen der FILESTREAM-Tabellenartikel kein blobstreaming **Sp_changemergearticle** festzulegende *Stream_blob_columns* auf "false".  
  
> [!IMPORTANT]  
>  Durch Aktivieren dieser Arbeitsspeicheroptimierung kann die Leistung des Merge-Agents bei der Synchronisierung beeinträchtigt werden. Die Option sollte nur verwendet werden, wenn Spalten mit Megabytes von Daten repliziert werden.  
  
> [!NOTE]  
>  Bestimmte Funktionalitäten der Mergereplikation, z. B. logische Datensätze können weiterhin verhindern, dass die datenstromoptimierung verwendet wird, wenn die Replikation von binary large Object, selbst bei *Stream_blob_columns* festgelegt **"true"**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addmergearticle** wird bei der Mergereplikation verwendet.  
  
 Wenn Sie Objekte veröffentlichen, werden ihre Definitionen auf Abonnenten kopiert. Wenn Sie ein Datenbankobjekt veröffentlichen, das von mindestens einem anderen Objekt abhängig ist, müssen Sie alle Objekte veröffentlichen, auf die verwiesen wird. Wenn Sie beispielsweise eine Sicht veröffentlichen, die von einer Tabelle abhängt, muss auch die Tabelle veröffentlicht werden.  
  
 Wenn Sie einen Wert angeben **3** für *Partition_options*, treten möglicherweise nur ein Abonnement für jede Partition der Daten in diesem Artikel. Wird ein zweites Abonnement erstellt, in dem das Filterkriterium des neuen Abonnements die gleiche Partition ergibt wie das vorhandene Abonnement, wird das vorhandene Abonnement gelöscht.  
  
 Einen Wert von 3 angegeben *Partition_options*, Metadaten wird bereinigt, wenn der Merge-Agent ausgeführt wird und die partitionierte Momentaufnahme läuft schneller ab. Beim Verwenden dieser Option sollten Sie in Erwägung ziehen, vom Abonnenten angeforderte partitionierte Momentaufnahmen zu aktivieren. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Hinzufügen eines Artikels mit einem statischen horizontalen Filter, wobei *Subset_filterclause*, zu eine vorhandene Veröffentlichung mit Artikeln, die parametrisierte Filter verfügen muss, die Abonnements erneut initialisiert werden.  
  
 Beim Angeben von *Processing_order*, es wird empfohlen Lücken zwischen den Werten für die Artikelreihenfolge, sodass sie einfacher in der Zukunft Festlegen neuer Wert zu. Wenn Sie drei Artikel Article1, Article2 und Article3 verfügen, z. B. festgelegt *Processing_order* auf 10, 20 und 30 anstatt 1, 2 und 3. Weitere Informationen finden Sie unter [Angeben der Verarbeitungsreihenfolge von Mergeartikeln](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
## <a name="default-schema-option-table"></a>Tabelle der Standardschemaoptionen  
 Diese Tabelle wird beschrieben, den Standardwert, der von der gespeicherten Prozedur festgelegt wird, wenn für ein Nullwert angegeben ist *Schema_option*, dem Artikeltyp abhängig.  
  
|Artikeltyp|Schemaoptionswert|  
|------------------|-------------------------|  
|**nur Func schema**|**0 x 01**|  
|**nur Schema indizierte Sicht**|**0 x 01**|  
|**Proc Schema nur**|**0 x 01**|  
|**table**|**0x0C034FD1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und späteren Versionen kompatible Veröffentlichungen mit einer Momentaufnahme im einheitlichen Modus.<br /><br /> **0x08034FF1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und späteren Versionen kompatible Veröffentlichungen mit einer Momentaufnahme im Zeichenmodus.|  
|**nur Schema anzeigen**|**0 x 01**|  
  
> [!NOTE]  
>  Wenn die Veröffentlichung frühere Versionen von unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die standardschemaoption für **Tabelle** ist **0x30034FF1**.  
  
## <a name="valid-schema-option-table"></a>Tabelle gültiger Schemaoptionen  
 Die folgende Tabelle beschreibt die zulässigen Werte *Schema_option* je nach Artikeltyp.  
  
|Artikeltyp|Schemaoptionswerte|  
|------------------|--------------------------|  
|**nur Func schema**|**0 x 01** und **0 x 2000**|  
|**nur Schema indizierte Sicht**|**0 x 01**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 1000000**, und **0 x 200000**|  
|**Proc Schema nur**|**0 x 01** und **0 x 2000**|  
|**table**|Alle Optionen|  
|**nur Schema anzeigen**|**0 x 01**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 1000000**, und **0 x 200000**|  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .  
  
## <a name="see-also"></a>Siehe auch  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
