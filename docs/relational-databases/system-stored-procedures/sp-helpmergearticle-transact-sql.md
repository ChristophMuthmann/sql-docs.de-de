---
title: Sp_helpmergearticle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords:
- sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 970c07111ba123be3262f9effb5c87a26bb14960
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergearticle-transact-sql"></a>sp_helpmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu einem Artikel zurück. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Wiederveröffentlichungsabonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, zu der Informationen abgerufen werden sollen. *Veröffentlichung*ist **Sysname**, hat den Standardwert  **%** , womit Informationen zu allen Mergeartikeln in allen Veröffentlichungen in der aktuellen Datenbank zurückgegeben.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name des Artikels, für den Informationen zurückgegeben werden sollen. *Artikel*ist **Sysname**, hat den Standardwert  **%** , womit Informationen zu allen Mergeartikeln in einer bestimmten Veröffentlichung zurückgegeben.  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Artikelbezeichner|  
|**name**|**sysname**|Der Name des Artikels.|  
|**Der Standardwert**|**sysname**|Name des Besitzers des Quellobjekts|  
|**source_object**|**sysname**|Name des Quellobjekts, aus dem der Artikel hinzugefügt werden soll|  
|**Der Standardwert**|**sysname**|Name des Besitzers der Sicht, die den veröffentlichten Artikel definiert|  
|**sync_object**|**sysname**|Name des benutzerdefinierten Objekts, mit dem die Anfangsdaten für die Partition eingerichtet werden|  
|**Beschreibung**|**nvarchar(255)**|Beschreibung des Artikels|  
|**status**|**tinyint**|Status des Artikels. Die folgenden Werte sind möglich:<br /><br /> **1** = inaktiv<br /><br /> **2** = aktiv<br /><br /> **5** = Data Definition Language (DDL) ausstehende Vorgang<br /><br /> **6** = DDL-Vorgang mit einer neu generierten Momentaufnahme<br /><br /> Hinweis: Wenn ein Artikel erneut initialisiert wird, Werte von **5** und **6** erhalten **2**.|  
|**creation_script**|**nvarchar(255)**|Pfad und Name eines optionalen Artikelschemaskripts, mit dem der Artikel in der Abonnementdatenbank erstellt wurde|  
|**conflict_table**|**nvarchar(270)**|Name der Tabelle, in der die Einfüge- oder Updatekonflikte gespeichert werden.|  
|**article_resolver**|**nvarchar(255)**|Benutzerdefinierter Konfliktlöser für den Artikel|  
|**subset_filterclause**|**nvarchar(1000)**|WHERE-Klausel für das horizontale Filtern.|  
|**pre_creation_command**|**tinyint**|Methode zur Voraberstellung. Die folgenden Werte sind möglich:<br /><br /> **0** = keine<br /><br /> **1** = löschen<br /><br /> **2** = löschen<br /><br /> **3** = Abschneiden|  
|**schema_option**|**Binary(8)**|Bitmuster der Option zur Schemaerstellung für den Artikel. Informationen zu dieser bitmusteroption finden Sie unter [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) oder [Sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md).|  
|**Typ**|**smallint**|Artikeltyp. Die folgenden Werte sind möglich:<br /><br /> **10** = Tabelle<br /><br /> **32** = gespeicherte Prozedur<br /><br /> **64** = Sicht oder indizierte Sicht<br /><br /> **128** = benutzerdefinierte Funktion<br /><br /> **160** = nur Synonymschema|  
|**column_tracking**|**int**|Die Einstellung für die nachverfolgung auf Spaltenebene; wobei **1** bedeutet, dass die nachverfolgung auf Spaltenebene aktiviert ist und **0** bedeutet, dass die nachverfolgung auf Spaltenebene deaktiviert ist.|  
|**resolver_info**|**nvarchar(255)**|Name des Artikelkonfliktlösers|  
|**vertical_partition**|**bit**|Wenn der Artikel vertikal partitioniert ist; wobei **1** bedeutet, dass der Artikel vertikal partitioniert ist, und **0** bedeutet, dass er nicht ist.|  
|**destination_owner**|**sysname**|Besitzer des Zielobjekts. Nur anwendbar beim Zusammenführen von gespeicherten Prozeduren, Sichten und Schemaartikeln benutzerdefinierter Funktionen (UDF, User-Defined Function).|  
|**identity_support**|**int**|Wenn die automatische Behandlung der Identitätsbereiche aktiviert ist; wobei **1** aktiviert ist und **0** ist deaktiviert.|  
|**pub_identity_range-Spalte**|**bigint**|Die beim Zuweisen neuer Identitätswerte zu verwendende Bereichsgröße. Weitere Informationen finden Sie im Abschnitt "Mergereplikation" [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identity_range**|**bigint**|Die beim Zuweisen neuer Identitätswerte zu verwendende Bereichsgröße. Weitere Informationen finden Sie im Abschnitt "Mergereplikation" [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**Schwellenwert**|**int**|Prozentwert für Abonnenten, auf denen [!INCLUDE[ssEW](../../includes/ssew-md.md)] oder frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Schwellenwert** steuert, wann der Merge-Agent einen neuen Identitätsbereich zuweist. Wenn der im Schwellenwert angegebene Prozentsatz verwendet wird, erstellt der Merge-Agent einen neuen Identitätsbereich. Weitere Informationen finden Sie im Abschnitt "Mergereplikation" [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**int**|Wenn eine digitale Signatur überprüft wird, bevor ein Konfliktlöser in einer Mergereplikation verwendet; wobei **0** bedeutet, dass die Signatur nicht bestätigt wird, und **1** bedeutet, dass die Signatur überprüft wird, um festzustellen, ob sie aus einer vertrauenswürdigen Quelle stammt.|  
|**destination_object**|**sysname**|Name des Zielobjekts. Nur anwendbar beim Zusammenführen gespeicherter Prozeduren, Sichten und UDF-Schemaartikel.|  
|**allow_interactive_resolver**|**int**|Wenn der interaktive Konfliktlöser für einen Artikel verwendet wird. wobei **1** bedeutet, dass dieser Konfliktlöser verwendet wird, und **0** bedeutet, dass es nicht verwendet wird.|  
|**fast_multicol_updateproc**|**int**|Aktiviert oder deaktiviert den Merge-Agent zum Anwenden von Änderungen auf mehrere Spalten in der gleichen Zeile in einer UPDATE-Anweisung; wobei **1** bedeutet, dass mehrere Spalten in einer Anweisung aktualisiert werden und **0** bedeutet, die UPDATE-Anweisungen trennen sind Probleme für jede aktualisierte Spalte.|  
|**check_permissions**|**int**|Ein Wert für eine ganze Zahl, der das Bitmuster der überprüften Berechtigungen auf Tabellenebene darstellt. Eine Liste der möglichen Werte finden Sie unter [Sp_addmergearticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**processing_order**|**int**|Die Reihenfolge, in der Datenänderungen auf Artikel in einer Veröffentlichung angewendet werden.|  
|**upload_options**|**tinyint**|Definiert Einschränkungen für Updates, die auf einem Abonnenten mit Clientabonnement vorgenommen wurden. Dabei sind folgende Werte möglich.<br /><br /> **0** = es gibt keine Einschränkungen für Updates, die auf einem Abonnenten mit clientabonnement vorgenommen; alle Änderungen an den Verleger hochgeladen werden.<br /><br /> **1** = Änderungen auf einem Abonnenten mit clientabonnement sind zulässig, jedoch nicht an den Verleger hochgeladen werden.<br /><br /> **2** = Änderungen sind auf einem Abonnenten mit clientabonnement nicht zulässig.<br /><br /> Weitere Informationen finden Sie unter [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).|  
|**identityrangemanagementoption**|**int**|Wenn die automatische Behandlung der Identitätsbereiche aktiviert ist; wobei **1** aktiviert ist und **0** ist deaktiviert.|  
|**delete_tracking**|**bit**|Wenn die Löschvorgänge repliziert werden. wobei **1** bedeutet, dass Löschvorgänge repliziert werden, und **0** bedeutet, dass sie nicht sind.|  
|**compensate_for_errors**|**bit**|Gibt an, ob kompensierende Aktionen ausgeführt werden, wenn während der Synchronisierung Fehler auftreten; wobei **1** gibt an, dass kompensierende Aktionen ausgeführt werden, und **0** bedeutet, dass keine kompensierenden Aktionen ausgeführt werden.|  
|**partition_options**|**tinyint**|Definiert die Art und Weise, wie Daten im Artikel partitioniert werden. Dies ermöglicht Leistungsoptimierungen, wenn alle Zeilen nur zu einer einzigen Partition oder zu einem einzigen Abonnement gehören. *Partition_options* kann einen der folgenden Werte sein.<br /><br /> **0** = das Filtern für den Artikel entweder statisch oder ergibt keine eindeutige Teilmenge von Daten für jede Partition, d. h. eine "überlappende" Partition.<br /><br /> **1** = die Partitionen überlappen, und Data Manipulation Language (DML) Updates auf dem Abonnenten vorgenommene können nicht geändert werden die Partition, zu der eine Zeile gehört.<br /><br /> **2** = das Filtern für den Artikel nicht überlappende Partitionen ergibt, aber mehrere Abonnenten können die gleiche Partition erhalten.<br /><br /> **3** = das Filtern für den Artikel nicht überlappende Partitionen ergibt, die für jedes Abonnement eindeutig sind.|  
|**artid**|**uniqueidentifier**|Ein Bezeichner, der den Artikel eindeutig identifiziert|  
|**pubid**|**uniqueidentifier**|Ein Bezeichner, der die Veröffentlichung, in der der Artikel veröffentlicht wird, eindeutig identifiziert|  
|**stream_blob_columns**|**bit**|Gibt an, ob die Datenstromoptimierung beim Replizieren von BLOB-Spalten (Binary Large Object) verwendet wird. **1** bedeutet, dass die Optimierung verwendet wird, und **0** bedeutet, dass die Optimierung nicht verwendet wird.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpmergearticle** wird bei der Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Db_owner** festen Datenbankrolle in der Veröffentlichungsdatenbank die **Replmonitor** Rolle in der Verteilungsdatenbank oder der veröffentlichungszugriffsliste für eine Veröffentlichung kann Ausführen**Sp_helpmergearticle**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Artikeleigenschaften](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Sp_addmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
