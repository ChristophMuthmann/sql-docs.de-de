---
title: Sysmergearticles (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergearticles
- sysmergearticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticles system table
ms.assetid: e9b1648e-4660-4688-9f56-18b2baf7228c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dbd1d7a476e2e87626efdcef9144a30e801e11d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergearticles-transact-sql"></a>sysmergearticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden in der lokalen Datenbank definierten Mergeartikel. Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name des Artikels.|  
|**Typ**|**tinyint**|Gibt den Artikeltyp an, der einen der folgenden Werte aufweisen kann:<br /><br /> **10** = Tabelle.<br /><br /> **32** = gespeicherte Prozedur (Schema only).<br /><br /> **64** = Sicht oder indizierte Sicht (Schema only).<br /><br /> **128** = User-defined Function (nur Schema).<br /><br /> **160** = Synonym (nur Schema).|  
|**OBJID**|**int**|Der Objektbezeichner.|  
|**sync_objid**|**int**|Die Objekt-ID der Sicht, die das synchronisierte Dataset darstellt.|  
|**view_type**|**tinyint**|Der Typ der Sicht:<br /><br /> **0** = keine Sicht; Verwendung des gesamten Basisobjekts.<br /><br /> **1** = permanente Sicht.<br /><br /> **2** = temporäre Sicht.|  
|**artid**|**uniqueidentifier**|Die eindeutige ID des angegebenen Artikels.|  
|**Beschreibung**|**nvarchar(255)**|Eine kurze Beschreibung des Artikels.|  
|**pre_creation_command**|**tinyint**|Die Standardaktion, die durchgeführt wird, wenn der Artikel in der Abonnementdatenbank erstellt wird:<br /><br /> **0 =** keine - Wenn die Tabelle auf dem Abonnenten bereits wird keine Aktion ausgeführt.<br /><br /> **1** = löschen: die Tabelle vor dem erneuten Erstellen gelöscht.<br /><br /> **2** = Delete-ein Löschvorgang wird basierend auf der WHERE-Klausel im Teilmengenfilter ausgegeben.<br /><br /> **3** = Abschneiden-identisch mit **2**, jedoch werden Seiten statt Zeilen gelöscht. Eine WHERE-Klausel wird jedoch nicht verwendet.|  
|**pubid**|**uniqueidentifier**|Die ID der Veröffentlichung, zu der der aktuelle Artikel gehört.|  
|**Spitzname**|**int**|Die Spitznamenzuordnung zur Identifikation des Artikels.|  
|**column_tracking**|**int**|Zeigt an, dass gibt an, ob die spaltenprotokollierung für den Artikel implementiert wird.|  
|**status**|**tinyint**|Zeigt den Status des Artikels an. Die folgenden Werte sind möglich:<br /><br /> **1** = unsynchronisiert - das Anfangsverarbeitungsskript zum Veröffentlichen der Tabelle wird der nächsten Ausführung der Momentaufnahme-Agent ausgeführt wird.<br /><br /> **2** = aktiv - das Anfangsverarbeitungsskript zum Veröffentlichen der Tabelle ausgeführt wurde.<br /><br /> **5** = New_inactive hinzugefügt werden.<br /><br /> **6** = New_active hinzugefügt werden.|  
|**conflict_table**|**sysname**|Der Name der lokalen Tabelle, die die Konflikt verursachenden Datensätze für den aktuellen Artikel enthält. Diese Tabelle dient nur zu Informationszwecken; ihr Inhalt kann mit benutzerdefinierten Konfliktlösungsroutinen oder direkt vom Administrator geändert oder gelöscht werden.|  
|**creation_script**|**nvarchar(255)**|Das Erstellungsskript für diesen Artikel.|  
|**conflict_script**|**nvarchar(255)**|Das Konfliktskript für diesen Artikel.|  
|**article_resolver**|**nvarchar(255)**|Der benutzerdefinierte Konfliktlöser auf Zeilenebene für diesen Artikel.|  
|**ins_conflict_proc**|**sysname**|Das Verfahren zum Schreiben des Konflikts zum **Conflict_table**.|  
|**insert_proc**|**sysname**|Die Prozedur, die vom Standardkonfliktlöser zum Einfügen von Zeilen während der Synchronisierung verwendet wird.|  
|**update_proc**|**sysname**|Die Prozedur, die vom Standardkonfliktlöser zum Aktualisieren von Zeilen während der Synchronisierung verwendet wird.|  
|**select_proc**|**sysname**|Der Name einer automatisch generierten gespeicherten Prozedur, die der Merge-Agent verwendet, um Sperren einzurichten bzw. um Spalten und Zeilen für einen Artikel zu finden.|  
|**metadata_select_proc**|**sysname**|Der Name der automatisch generierten gespeicherten Prozedur, mit der in den Systemtabellen der Mergereplikation auf Metadaten zugegriffen wird.|  
|**delete_proc**|**sysname**|Die Prozedur, die vom Standardkonfliktlöser zum Löschen von Zeilen während der Synchronisierung verwendet wird.|  
|**schema_option**|**Binary(8)**|Für die unterstützten Werte *Schema_option*, finden Sie unter [Sp_addmergearticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|Der Name der auf dem Abonnenten erstellten Tabelle.|  
|**destination_owner**|**sysname**|Der Name des Besitzers des Zielobjekts.|  
|**resolver_clsid**|**nvarchar(50)**|Die ID des benutzerdefinierten Konfliktlösers.|  
|**subset_filterclause**|**nvarchar(1000)**|Die Filterklausel für diesen Artikel.|  
|**missing_col_count**|**int**|Die Anzahl der fehlenden Spalten.|  
|**missing_cols**|**varbinary(128)**|Das Bitmap der fehlenden Spalten.|  
|**excluded_cols**|**varbinary(128)**|Das Bitmap der Spalten, die vom Artikel ausgeschlossen werden, wenn dieser an den Abonnenten gesendet wird.|  
|**excluded_col_count**|**int**|Die Anzahl der ausgeschlossenen Spalten.|  
|**Spalten**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|Die Bitmaps der Spalten, die aus der Quelltabelle gelöscht wurden.|  
|**resolver_info**|**nvarchar(255)**|Der Speicherplatz für zusätzliche vom benutzerdefinierten Konfliktlöser benötigte Informationen.|  
|**view_sel_proc**|**nvarchar(290)**|Der Name einer gespeicherten Prozedur, die der Merge-Agent zum ersten Auffüllen eines Artikels in einer dynamisch gefilterten Veröffentlichung und zum Auflisten von geänderten Zeilen in einer beliebigen gefilterten Veröffentlichung verwendet.|  
|**gen_cur**|**int**|Die Generierungsnummer für lokale Änderungen an der Basistabelle eines Artikels.|  
|**vertical_partition**|**int**|Gibt an, ob die Spaltenfilterung für einen Tabellenartikel aktiviert ist. **0** zeigt an, dass keine vertikale Filterung und alle Spalten veröffentlicht.|  
|**identity_support**|**int**|Gibt an, ob die automatische Verarbeitung der Identitätsbereiche aktiviert ist. **1** bedeutet, dass der Identitätsbereiche aktiviert ist, und **0** bedeutet, dass keine identitätsbereichsunterstützung vorhanden ist.|  
|**before_image_objid**|**int**|Die Objekt-ID der Nachverfolgungstabelle. Die Nachverfolgungstabelle enthält bestimmte Schlüsselspaltenwerte, wenn eine Veröffentlichung erstellt wird  *@keep_partition_changes*   =  **"true"**.|  
|**before_view_objid**|**int**|Die Objekt-ID einer Sichttabelle. Die Sicht ist für eine Tabelle festgelegt, die überwacht, ob eine Zeile zu einem bestimmten Abonnenten gehört hat, bevor sie gelöscht oder aktualisiert wurde. Gilt nur, wenn eine Veröffentlichung mit erstellt  *@keep_partition_changes*   =  **"true".**|  
|**verify_resolver_signature**|**int**|Gibt an, ob eine digitale Signatur überprüft wird, bevor ein Konfliktlöser in einer Mergereplikation verwendet wird:<br /><br /> **0** = Signatur wird nicht überprüft.<br /><br /> **1** = Signatur wird überprüft, um festzustellen, ob sie aus einer vertrauenswürdigen Quelle stammt.|  
|**allow_interactive_resolver**|**bit**|Gibt an, ob die Verwendung des interaktiven Konfliktlösers für einen Artikel aktiviert ist. **1** gibt an, dass der interaktive Konfliktlöser für den Artikel verwendet wird.|  
|**fast_multicol_updateproc**|**bit**|Gibt an, ob der Merge-Agent aktiviert wurde, um in einer UPDATE-Anweisung Änderungen auf mehrere Spalten in derselben Zeile anzuwenden.<br /><br /> **0** = Probleme, die für jede Spalte ein getrenntes UPDATE geändert.<br /><br /> **1** = gibt eine UPDATE-Anweisung die Updates aus mehreren Spalten in einer einzelnen Anweisung verursacht.|  
|**check_permissions**|**int**|Die Bitmap der Berechtigungen auf Tabellenebene, die überprüft, wenn der Merge-Agent Änderungen an den Verleger anwendet. *Check_permissions* kann einen der folgenden Werte aufweisen:<br /><br /> **0 x 00 =** Berechtigungen werden nicht überprüft.<br /><br /> **0 x 10 =** Berechtigungen auf dem Verleger geprüft, bevor auf einem Abonnenten ausgeführte Einfügevorgänge hochgeladen werden können.<br /><br /> **0 x 20 =** Berechtigungen auf dem Verleger geprüft, bevor die Aktualisierungen, die auf einem Abonnenten hochgeladen werden können.<br /><br /> **0 x 40 =** Berechtigungen auf dem Verleger geprüft, bevor auf einem Abonnenten ausgeführte Löschvorgänge hochgeladen werden können.|  
|**maxversion_at_cleanup**|**int**|Die höchste Generierung, für die ein Cleanup der Metadaten ausgeführt wird.|  
|**processing_order**|**int**|Gibt die Verarbeitungsreihenfolge von Artikeln in einer Mergeveröffentlichung an. ein Wert von **0** ergaben, dass der Artikel nicht sortiert ist und die Artikel in der Reihenfolge vom niedrigsten zum höchsten Wert verarbeitet werden. Wenn zwei Artikel denselben Wert haben, werden sie gleichzeitig verarbeitet. Weitere Informationen finden Sie unter [Angeben der Verarbeitungsreihenfolge von Mergeartikeln](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).|  
|**upload_options**|**tinyint**|Definiert Einschränkungen für Updates, die auf einem Abonnenten mit Clientabonnement vorgenommen wurden. Dabei sind folgende Werte möglich.<br /><br /> **0** = es gibt keine Einschränkungen für Updates, die auf einem Abonnenten mit clientabonnement vorgenommen; alle Änderungen an den Verleger hochgeladen werden.<br /><br /> **1** = Änderungen auf einem Abonnenten mit clientabonnement sind zulässig, jedoch nicht an den Verleger hochgeladen werden.<br /><br /> **2** = Änderungen sind auf einem Abonnenten mit clientabonnement nicht zulässig.<br /><br /> Weitere Informationen finden Sie unter [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).|  
|**published_in_tran_pub**|**bit**|Gibt an, dass ein Artikel in einer Mergeveröffentlichung auch in einer Transaktionsveröffentlichung veröffentlicht wird.<br /><br /> **0** = der Artikel ist nicht in einem Transaktionsartikel veröffentlicht.<br /><br /> **1** = der Artikel wird auch in einem Transaktionsartikel veröffentlicht.|  
|**Lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**NCHAR(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|Muss hinzugefügt werden.|  
|**delete_tracking**|**bit**|Gibt an, ob Löschungen repliziert werden.<br /><br /> **0** = Löschvorgänge werden nicht repliziert.<br /><br /> **1** = löschungen werden repliziert, dies ist das Standardverhalten für die Mergereplikation.<br /><br /> Wenn der Wert der *Delete_tracking* ist **0**, auf dem Abonnenten gelöschte Zeilen müssen manuell entfernt werden, auf dem Verleger und auf dem Verleger gelöschte Zeilen müssen manuell entfernt werden, auf dem Abonnenten.<br /><br /> Hinweis: Der Wert **0** führt zu einer Nichtkonvergenz.|  
|**compensate_for_errors**|**bit**|Gibt an, ob kompensierende Aktionen ausgeführt werden, wenn während der Synchronisierung Fehler auftreten.<br /><br /> **0** = kompensierende Aktionen sind deaktiviert.<br /><br /> **1** = Änderungen, die auf einem Abonnenten oder Verleger führen immer zu kompensierenden Aktionen, um diese Änderungen rückgängig machen, ist das Standardverhalten für die Mergereplikation angewendet werden kann.<br /><br /> Hinweis: Der Wert **0** führt zu einer Nichtkonvergenz.|  
|**pub_range**|**bigint**|Die Größe des Identitätsbereichs für den Verleger.|  
|**Bereich**|**bigint**|Die Bereichsgröße der aufeinander folgenden Identitätswerte, die Abonnenten bei einer Anpassung zugewiesen würden.|  
|**Schwellenwert**|**int**|Als Prozentsatz angegebener Schwellenwert für den Identitätsbereich.|  
|**stream_blob_columns**|**bit**|Gibt an, ob beim Replizieren von BLOB-Spalten (Binary Large Object) eine Datenstromoptimierung verwendet wird. **1** bedeutet, dass die Optimierung versucht wird.|  
|**preserve_rowguidcol**|**bit**|Gibt an, ob die Replikation eine vorhandene ROWGUID-Spalte verwendet. Der Wert **1** bedeutet, dass eine vorhandene ROWGUIDCOL-Spalte verwendet wird. **0** bedeutet, dass die Replikation die ROWGUIDCOL-Spalte hinzugefügt wurde.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sp_addmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [Sp_helpmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)  
  
  
