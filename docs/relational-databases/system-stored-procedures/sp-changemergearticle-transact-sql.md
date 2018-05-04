---
title: Sp_changemergearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2015
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
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b778c6bad14bb756ddb8a8e24b1d7e95a87956d4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangemergearticle-transact-sql"></a>sp_changemergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Mergeartikels. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung, in der der Artikel vorhanden ist. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name des zu ändernden Artikels. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@property=**] **"***Eigenschaft***"**  
 Entspricht der für den angegebenen Artikel und die entsprechende Veröffentlichung zu ändernden Eigenschaft. *Eigenschaft* ist **nvarchar(30)**, und kann einen der Werte aufgeführt werden in der Tabelle.  
  
 [  **@value=**] **"***Wert***"**  
 Ist der neue Wert für die angegebene Eigenschaft. *Wert* ist **nvarchar(1000)**, und kann einen der Werte aufgeführt werden in der Tabelle.  
  
 Diese Tabelle beschreibt die Eigenschaften von Artikeln und die Werte für diese Eigenschaften.  
  
|Eigenschaft|Werte|Description|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|Aktiviert die Verwendung eines interaktiven Konfliktlösers für den Artikel.|  
||**false**|Deaktiviert die Verwendung eines interaktiven Konfliktlösers für den Artikel.|  
|**article_resolver**||Benutzerdefinierter Konfliktlöser für den Artikel Gilt nur für einen Tabellenartikel.|  
|**Check_permissions** (Bitmap)|**0 x 00**|Berechtigungen auf Tabellenebene werden nicht überprüft.|  
||**0 x 10**|Berechtigungen auf Tabellenebene werden beim Verleger überprüft, bevor beim Abonnenten ausgeführte INSERT-Anweisungen auf den Verleger angewendet werden.|  
||**0 x 20**|Berechtigungen auf Tabellenebene werden beim Verleger überprüft, bevor beim Abonnenten ausgeführte UPDATE-Anweisungen auf den Verleger angewendet werden.|  
||**0 x 40**|Berechtigungen auf Tabellenebene werden beim Verleger überprüft, bevor DELETE-Anweisungen beim Abonnenten auf den Verleger angewendet werden.|  
|**column_tracking**|**true**|Aktiviert die Protokollierung auf Spaltenebene. Gilt nur für einen Tabellenartikel.<br /><br /> Hinweis: Auf Spaltenebene kann nicht verwendet werden, wenn die Veröffentlichung mit mehr als 246 Spalten Tabellen.|  
||**false**|Deaktiviert die Protokollierung auf Spaltenebene und belässt die Konflikterkennung auf der Zeilenebene. Gilt nur für einen Tabellenartikel.|  
|**compensate_for_errors**|**true**|Wenn bei der Synchronisierung Fehler auftreten, werden kompensierende Aktionen ausgeführt. Weitere Informationen finden Sie unter [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
||**false**|Es werden keine kompensierenden Aktionen ausgeführt. Dies ist das Standardverhalten. Weitere Informationen finden Sie unter [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).<br /><br /> **\*\* Wichtige \* \***  Obwohl Daten in den betroffenen Zeilen angezeigt werden möglicherweise nicht konvergent werden als Fehler zu beheben, Änderungen können übernommen werden, und Daten zusammengeführt werden. Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, und klicken Sie dann auf den Wert des veröffentlicht wurde *Compensate_for_errors* muss für beide Artikel gleich sein.|  
|**creation_script**||Pfad und Name eines optionalen Artikelschemaskripts, mit dem der Artikel in der Abonnementdatenbank erstellt wurde|  
|**delete_tracking**|**true**|DELETE-Anweisungen werden repliziert. Dies ist das Standardverhalten.|  
||**false**|DELETE-Anweisungen werden nicht repliziert.<br /><br /> **\*\* Wichtige \* \***  Einstellung **Delete_tracking** auf **"false"** führt zu einer Nichtkonvergenz, und gelöschte Zeilen müssen manuell entfernt werden.|  
|**description**||Beschreibungseintrag für den Artikel.|  
|**destination_owner**||Name des Besitzers des Objekts in der Abonnementdatenbank, wenn nicht **Dbo**.|  
|**identity_range**||**"bigint"** , die beim Zuweisen neuer Identitätswerte, wenn der Artikel zu verwendende Bereichsgröße angibt, die **Identityrangemanagementoption** festgelegt **Auto** oder **Auto_identity_ Bereich** festgelegt **"true"**. Gilt nur für einen Tabellenartikel. Weitere Informationen finden Sie im Abschnitt "Mergereplikation" [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identityrangemanagementoption**|**Manuell**|Deaktiviert die automatische Verwaltung des Identitätsbereichs. Kennzeichnet Identitätsspalten mithilfe von NOT FOR REPLICATION, um die manuelle Handhabung des Identitätsbereichs zu aktivieren. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
||**Keine**|Deaktiviert die gesamte Verwaltung des Identitätsbereichs.|  
|**logical_record_level_conflict_detection**|**true**|Ein Konflikt wird erkannt, wenn an einer beliebigen Stelle im logischen Datensatz Änderungen vorgenommen werden. Erfordert, dass **Logical_record_level_conflict_resolution** festgelegt werden, um **"true"**.|  
||**false**|Standardkonflikterkennung wird verwendet, nach den Angaben von **Column_tracking**.|  
|**logical_record_level_conflict_resolution**|**true**|Der gesamte gewinnende logische Datensatz überschreibt den verlierenden logischen Datensatz.|  
||**false**|Die Gewinnerzeilen sind nicht auf den logischen Datensatz eingeschränkt.|  
|**partition_options**|**0**|Das Filtern für den Artikel ist entweder statisch oder ergibt keine eindeutige Teilmenge von Daten für jede Partition, d. h. eine "überlappende" Partition.|  
||**1**|Die Partitionen überlappen, und beim Abonnenten vorgenommene DML-Updates können nicht die Partition ändern, zu der eine Zeile gehört.|  
||**2**|Das Filtern für den Artikel ergibt nicht überlappende Partitionen. Mehrere Abonnenten können jedoch die gleiche Partition erhalten.|  
||**3**|Das Filtern für den Artikel ergibt nicht überlappende Partitionen, die für jedes Abonnement eindeutig sind.<br /><br /> Hinweis: Wenn Sie einen Wert angeben **3** für **Partition_options**, treten möglicherweise nur ein Abonnement für jede Partition der Daten in diesem Artikel. Wird ein zweites Abonnement erstellt, in dem das Filterkriterium des neuen Abonnements die gleiche Partition ergibt wie das vorhandene Abonnement, wird das vorhandene Abonnement gelöscht.|  
|**pre_creation_command**|**Keine**|Wenn die Tabelle bereits auf dem Abonnenten vorhanden ist, wird keine Aktion ausgeführt.|  
||**Löschen**|Ein Löschvorgang wird auf der Grundlage der WHERE-Klausel im Teilmengenfilter ausgegeben.|  
||**Löschen**|Die Tabelle wird vor dem erneuten Erstellen gelöscht.|  
||**truncate**|Schneidet die Zieltabelle ab.|  
|**processing_order**||**Int** , der die Verarbeitungsreihenfolge von Artikeln in einer Mergeveröffentlichung angibt.|  
|**pub_identity_range-Spalte**||**"bigint"** , die an einen Abonnenten mit einem Serverabonnement zugeordnete werden, wenn der Artikel weist Bereichsgröße angibt, die **Identityrangemanagementoption** festgelegt **Auto** oder **Auto_Close Identity_range** festgelegt **"true"**. Dieser Identitätsbereich ist für einen Wiederveröffentlichungsabonnenten für die Zuordnung zu dessen Abonnenten reserviert. Gilt nur für einen Tabellenartikel. Weitere Informationen finden Sie im Abschnitt "Mergereplikation" [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**published_in_tran_pub**|**true**|Der Artikel wird zusätzlich in einer Transaktionsveröffentlichung veröffentlicht.|  
||**false**|Der Artikel wird nicht zusätzlich in einer Transaktionsveröffentlichung veröffentlicht.|  
|**resolver_info**||Wird für die Angabe zusätzlicher Informationen verwendet, die für einen benutzerdefinierten Konfliktlöser erforderlich sind. Einige der [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Konfliktlöser erfordern eine Spalte, die als Eingabe für den Konfliktlöser dient. **Resolver_info** ist **nvarchar(255)**, hat den Standardwert NULL. Weitere Informationen finden Sie unter [Microsoft COM-basierte Konfliktlöser](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).|  
|**Schema_option** (Bitmap)||Weitere Informationen finden Sie im Abschnitt mit den Hinweisen weiter unten in diesem Thema.|  
||**0 x 00**|Deaktiviert die Skripterstellung durch den Momentaufnahme-Agent und verwendet das Skript im bereitgestellten **Creation_script**.|  
||**0 x 01**|Generiert das Objekterstellungsskript (CREATE TABLE, CREATE PROCEDURE usw.).|  
||**0 x 10**|Generiert einen entsprechenden gruppierten Index.|  
||**0 x 20**|Konvertiert benutzerdefinierte Datentypen auf dem Abonnenten in Basisdatentypen. Die Option kann nicht verwendet werden, wenn eine CHECK- oder DEFAULT-Einschränkung für eine Spalte von einem benutzerdefinierten Typ ( User-defined Type, UDT) vorhanden ist, wenn eine UDT-Spalte Teil des Primärschlüssels ist oder wenn eine berechnete Spalte auf eine UDT-Spalte verweist.|  
||**0 x 40**|Generiert entsprechende nicht gruppierte Indizes.|  
||**0 x 80**|Schließt die deklarative referenzielle Integrität für die Primärschlüssel ein.|  
||**0 x 100**|Repliziert Benutzertrigger für einen Tabellenartikel, wenn definiert.|  
||**0 x 200**|Repliziert FOREIGN KEY-Einschränkungen. Wenn die Tabelle, auf die verwiesen wird, nicht Teil einer Veröffentlichung ist, werden für eine veröffentlichte Tabelle keine FOREIGN KEY-Einschränkungen repliziert.|  
||**0 x 400**|Repliziert CHECK-Einschränkungen.|  
||**0 x 800**|Repliziert Standards.|  
||**0 x 1000**|Repliziert die Sortierung auf Spaltenebene.|  
||**0 x 2000**|Repliziert erweiterte Eigenschaften, die dem Quellobjekt des veröffentlichten Artikels zugeordnet sind.|  
||**0 x 4000**|Repliziert eindeutige Schlüssel, wenn auf einem Tabellenartikel definiert.|  
||**0 x 8000**|Generiert ALTER TABLE-Anweisungen beim Erstellen von Skripts mit Einschränkungen.|  
||**0 x 10000**|Repliziert CHECK-Einschränkungen als NOT FOR REPLICATION, sodass die Einschränkungen während der Synchronisierung nicht erzwungen werden.|  
||**0 x 20000**|Repliziert FOREIGN KEY-Einschränkungen als NOT FOR REPLICATION, sodass diese Einschränkungen bei der Synchronisierung nicht erzwungen werden.|  
||**0 x 40000**|Repliziert Dateigruppen, die mit einer partitionierten Tabelle oder einem Index verbunden sind.|  
||**0 x 80000**|Repliziert das Partitionsschema für eine partitionierte Tabelle.|  
||**0 x 100000**|Repliziert das Partitionsschema für einen partitionierten Index.|  
||**0 x 200000**|Repliziert Tabellenstatistiken.|  
||**0 x 400000**|Repliziert Standardbindungen|  
||**0 x 800000**|Repliziert Regelbindungen.|  
||**0 x 1000000**|Repliziert den Volltextindex.|  
||**0x2000000**|XML-schemaauflistungen gebunden **Xml** Spalten werden nicht repliziert.|  
||**0x4000000**|Repliziert Indizes für **Xml** Spalten.|  
||**0x8000000**|Legt Schemas an, die auf dem Abonnent noch nicht vorhanden sind.|  
||**0 x 10000000**|Konvertiert **Xml** Spalten **Ntext** auf dem Abonnenten.|  
||**0 x 20000000**|Konvertiert, die große Objekttypen Daten (**nvarchar(max)**, **varchar(max)**, und **varbinary(max)**), die in eingeführt wurden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Datentypen, die unterstützt werden auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
||**0 x 40000000**|Berechtigungen für die Replikation.|  
||**0 x 80000000**|Der Versuch, Abhängigkeiten für Objekte zu löschen, die nicht Teil der Veröffentlichung sind.|  
||**0 x 100000000**|Mit dieser Option können Sie das FILESTREAM-Attribut replizieren, wenn er für angegeben wird **varbinary(max)** Spalten. Geben Sie diese Option nicht an, wenn Sie Tabellen auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Abonnenten replizieren. Replizieren von Tabellen mit FILESTREAM-Spalten auf [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] -Abonnenten wird unabhängig von der Festlegung dieser Schemaoption nicht unterstützt. Siehe die verwandte Option **0 x 800000000**.|  
||**0x200000000**|Datum und Uhrzeit-Datentypen konvertiert (**Datum**, **Zeit**, **"DateTimeOffset"**, und **datetime2**), die in eingeführt werden [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Datentypen, die in früheren Versionen von unterstützt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0x400000000**|Repliziert die Komprimierungsoption für Daten und Indizes. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0 x 800000000**|Legen Sie diese Option fest, um FILESTREAM-Daten in einer eigenen Dateigruppe auf dem Abonnenten zu speichern. Wenn diese Option nicht festgelegt wird, werden FILESTREAM-Daten in der Standarddateigruppe gespeichert. Bei der Replikation werden keine Dateigruppen erstellt. Daher müssen Sie beim Festlegen dieser Option die Dateigruppe erstellen, bevor Sie die Momentaufnahme auf dem Abonnenten anwenden. Weitere Informationen zum Erstellen von Objekten vor dem Anwenden der Momentaufnahme finden Sie unter [Ausführen von Skripts vor und nach der Momentaufnahme angewendet wird](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Siehe die verwandte Option **0 x 100000000**.|  
||**0x1000000000**|Konvertiert von common Language Runtime (CLR) eine benutzerdefinierte Typen (UDTs) in **varbinary(max)** , sodass Spalten vom Typ UDT auf Abonnenten repliziert werden können, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x2000000000**|Konvertiert die **Hierarchyid** Datentyp, **varbinary(max)** sodass Spalten vom Typ **Hierarchyid** repliziert werden können, an die Abonnenten, die ausgeführt werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Weitere Informationen zur Verwendung von **Hierarchyid** -Spalten in replizierten Tabellen finden Sie unter [Hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Repliziert die gefilterten Indizes in der Tabelle. Weitere Informationen zu gefilterten Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Konvertiert die **Geography** und **Geometrie** Datentypen zu **varbinary(max)** , sodass Spalten dieser Typen auf Abonnenten repliziert werden können, die ausgeführtwerden[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|Repliziert Indizes für Spalten vom Typ **Geography** und **Geometrie**.|  
||NULL|Das System generiert automatisch eine gültige Schemaoption für den Artikel.|  
|**status**|**Aktive**|Das Anfangsverarbeitungsskript zur Veröffentlichung der Tabelle wird ausgeführt.|  
||**unsynced**|Das Anfangsverarbeitungsskript zum Veröffentlichen der Tabelle wird ausgeführt, wenn der Momentaufnahme-Agent das nächste Mal ausgeführt wird.|  
|**stream_blob_columns**|**true**|Beim Replizieren von BLOB-Spalten (Binary Large Object) wird eine Datenstromoptimierung verwendet. Bestimmte Funktionalitäten der Mergereplikation, wie z. B. logische Datensätze, können jedoch weiterhin verhindern, dass die Datenstromoptimierung verwendet wird. *Stream_blob_columns* festgelegt ist, auf "true", wenn FILESTREAM aktiviert ist. Dadurch werden die Replikation der FILESTREAM-Daten optimal ausgeführt und die Arbeitsspeicherauslastung reduziert. Um FILESTREAM-Tabellenartikel kein blobstreaming zu erzwingen, legen *Stream_blob_columns* auf "false".<br /><br /> **\*\* Wichtige \* \***  durch Aktivieren dieser arbeitsspeicheroptimierung kann die Leistung der Merge-Agent während der Synchronisierung beeinträchtigt. Die Option sollte nur verwendet werden, wenn Spalten mit Megabytes von Daten repliziert werden.|  
||**false**|Beim Replizieren von BLOB-Spalten (Binary Large Object) wird die Optimierung nicht verwendet.|  
|**subscriber_upload_options**|**0**|Keine Einschränkungen für Updates, die bei einem Abonnenten mit einem Clientabonnement vorgenommen werden. Änderungen werden auf den Verleger hochgeladen. Für das Ändern dieser Eigenschaft ist möglicherweise eine erneute Initialisierung von vorhandenen Abonnenten erforderlich.|  
||**1**|Änderungen sind bei einem Abonnenten mit einem Clientabonnement zulässig, werden jedoch nicht auf den Verleger hochgeladen.|  
||**2**|Änderungen sind bei einem Abonnenten mit einem Clientabonnement nicht zulässig.|  
|**subset_filterclause**||WHERE-Klausel für das horizontale Filtern. Gilt nur für einen Tabellenartikel.<br /><br /> **\*\* Wichtige \* \***  aus Leistungsgründen wird empfohlen, dass Sie keine Funktionen auf Spaltennamen in Klauseln für parametrisierte Zeilenfilter, wie z. B. anzuwenden `LEFT([MyColumn]) = SUSER_SNAME()`. Bei Verwendung von [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) in einer Filterklausel verwenden und den Wert HOST_NAME überschreiben, müssen Sie möglicherweise Datentypen mithilfe von convert [konvertieren](../../t-sql/functions/cast-and-convert-transact-sql.md). Weitere Informationen zu bewährten Methoden für diesen Fall finden Sie im Abschnitt "Überschreiben des Host_name()-Werts""in [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
|**threshold**||Prozentwert für Abonnenten, auf denen [!INCLUDE[ssEW](../../includes/ssew-md.md)] oder frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Schwellenwert** steuert, wann der Merge-Agent einen neuen Identitätsbereich zuweist. Wenn der im Schwellenwert angegebene Prozentsatz verwendet wird, erstellt der Merge-Agent einen neuen Identitätsbereich. Wird verwendet, wenn **Identityrangemanagementoption** festgelegt ist, um **automatisch** oder **Auto_identity_range** festgelegt ist, um **"true"**. Gilt nur für einen Tabellenartikel. Weitere Informationen finden Sie im Abschnitt "Mergereplikation" [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**1**|Die digitale Signatur in einem benutzerdefinierten Konfliktlöser wird überprüft, um festzustellen, ob er aus einer vertrauenswürdigen Quelle stammt.|  
||**0**|Die digitale Signatur in einem benutzerdefinierten Konfliktlöser wird nicht überprüft, um festzustellen, ob er aus einer vertrauenswürdigen Quelle stammt.|  
|NULL (Standard)||Gibt die Liste der unterstützten Werte für *Eigenschaft*.|  
  
 [  **@force_invalidate_snapshot =** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Mergeartikel bewirken nicht, die Momentaufnahme ungültig zu sein. Wenn die gespeicherte Prozedur erkennt, dass die Änderungen eine neue Momentaufnahme erfordern, tritt ein Fehler auf und es werden keine Änderungen vorgenommen.  
  
 **1** bedeutet, dass Änderungen am Mergeartikel die Momentaufnahme ungültig werden können, und es sind Abonnements vorhanden, die eine neue Momentaufnahme erfordern würden, erhalten Sie über die Berechtigung für die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme zu generieren.  
  
 Weitere Informationen zu den Eigenschaften, bei deren Änderung die Generierung einer neuen Momentaufnahme erforderlich ist, finden Sie im Abschnitt "Hinweise".  
  
 [  **@force_reinit_subscription =** ] *Force_reinit_subscription*  
 Bestätigt, dass die von dieser gespeicherten Prozedur ausgeführte Aktion die erneute Initialisierung vorhandener Abonnements erfordern kann. *Force_reinit_subscription* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Mergeartikel bewirken nicht, das Abonnement erneut initialisiert werden. Wenn die gespeicherte Prozedur erkennt, dass die Änderung die Neuinitialisierung vorhandener Abonnements erfordert, tritt ein Fehler auf, und es werden keine Änderungen durchgeführt.  
  
 **1** bedeutet, dass am Mergeartikel Änderungen bewirken, dass vorhandene Abonnements erneut initialisiert werden, und die Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
 Weitere Informationen zu den Eigenschaften, bei deren Änderung die erneute Initialisierung aller vorhandenen Abonnements erforderlich ist, finden Sie im Abschnitt "Hinweise".  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changemergearticle** wird bei der Mergereplikation verwendet.  
  
 Da **Sp_changemergearticle** wird verwendet, um die Artikeleigenschaften zu ändern, die ursprünglich mit angegeben wurden [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), finden Sie unter [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Weitere Informationen zu diesen Eigenschaften.  
  
 Ändern die folgenden Eigenschaften erfordert, dass eine neue Momentaufnahme generiert werden, und geben Sie einen Wert von **1** für die *Force_invalidate_snapshot* Parameter:  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 Ändern die folgenden Eigenschaften muss vorhandene Abonnements erneut initialisiert werden, und geben Sie einen Wert von **1** für die *Force_reinit_subscription* Parameter:  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 Einen Wert von 3 angegeben **Partition_options**, Metadaten bereinigt einrichten, wenn der Merge-Agent ausgeführt wird und die partitionierte Momentaufnahme läuft schneller ab. Beim Verwenden dieser Option sollten Sie in Erwägung ziehen, vom Abonnenten angeforderte partitionierte Momentaufnahmen zu aktivieren. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Beim Festlegen der **Column_tracking** -Eigenschaft, wenn die Tabelle bereits in anderen Mergereplikationen veröffentlicht wird die spaltennachverfolgung muss identisch mit dem Wert von bestehenden Artikeln für diese Tabelle verwendet wird. Dieser Parameter ist nur für Tabellenartikel spezifisch.  
  
 Wenn mehrere Veröffentlichungen Artikel basierend auf der gleichen zugrundeliegenden Tabelle veröffentlichen, Ändern der **Delete_tracking** Eigenschaft oder die **Compensate_for_errors** -Eigenschaft für einen Artikel bewirkt, dass die gleiche Änderung mit den anderen Artikeln, die in der gleichen Tabelle basieren hergestellt werden.  
  
 Wenn der vom Mergeprozess verwendete Benutzername bzw. das Benutzerkonto auf dem Verleger nicht über die entsprechenden Tabellenberechtigungen verfügt, werden die ungültigen Änderungen als Konflikte protokolliert.  
  
 Beim Ändern des Werts von **Schema_option**, das System führt ein bitweises Update nicht. Dies bedeutet, dass beim Festlegen der **Schema_option** mit **Sp_changemergearticle**vorhandene biteinstellungen möglicherweise deaktiviert. Um die vorhandenen Einstellungen beizubehalten, sollten Sie ausführen [& (bitweises AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md) zwischen dem Wert festlegen und der aktuelle Wert der *Schema_option*, dem kann bestimmt werden, durch das Ausführen von [Sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md).  
  
> [!CAUTION]  
>  Wenn Sie viele (einem solchen Test Hunderte) von Artikeln in einer Veröffentlichung, und Sie führen **Sp_changemergearticle** für einen Artikel, möglicherweise dauert sehr lange zum Beenden der Ausführung.  
  
## <a name="valid-schema-option-table"></a>Tabelle gültiger Schemaoptionen  
 Die folgende Tabelle beschreibt die zulässigen *Schema_option*Werte, je nach Artikeltyp.  
  
|Artikeltyp|Schemaoptionswerte|  
|------------------|--------------------------|  
|**nur Func schema**|**0 x 01** und **0 x 2000**|  
|**nur Schema indizierte Sicht**|**0 x 01**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 1000000**, und **0 x 200000**|  
|**Proc Schema nur**|**0 x 01** und **0 x 2000**|  
|**table**|Alle Optionen|  
|**nur Schema anzeigen**|**0 x 01**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 1000000**, und **0 x 200000**|  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changemergearticle**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Artikeleigenschaften](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
