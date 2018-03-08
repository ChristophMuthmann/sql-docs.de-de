---
title: Volltextsuche und semantische Suche von gespeicherten Prozeduren (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], stored procedures
- full-text search [SQL Server], stored procedures
- full-text catalogs [SQL Server], stored procedures
- system stored procedures [SQL Server], full-text search
ms.assetid: 0d185a16-2b16-4958-884f-efe675e2e551
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f33f210b67183f03e1631361082ef8bb97c03cc7
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="full-text-search-and-semantic-search-stored-procedures-transact-sql"></a>Gespeicherte Prozeduren für Volltextsuche und semantische Suche (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die folgenden gespeicherten Systemprozeduren, die zum Implementieren und Abfragen von Volltextindizes und semantischen Indizes verwendet werden.  
  
## <a name="full-text-search-stored-procedures"></a>Gespeicherte Prozeduren für die Volltextsuche  
 [sp_fulltext_catalog](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)  
 Erstellt und löscht einen Volltextkatalog und startet und beendet die Indizierung eines Katalogs. Für eine Datenbank können mehrere Volltextkataloge erstellt werden.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwendung [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md), [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md), und [DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) stattdessen.  
  
 [sp_fulltext_column](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)  
 Gibt an, ob eine bestimmte Spalte einer Tabelle bei der Volltextindizierung berücksichtigt werden soll.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwendung [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) stattdessen.  
  
 [sp_fulltext_database](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)  
 Hat keine Auswirkung auf Volltextkataloge in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen und wird nur für Abwärtskompatibilität unterstützt.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
 Gibt Zuordnungen zwischen dokumentbezeichnern (**DocId**s) und die Volltext-Schlüsselwerte.  
  
 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 Analysiert und lädt die Daten aus einer aktualisierten Thesaurusdatei, die einem Gebietsschemabezeichner (LCID) entspricht, und verursacht die Neukompilierung der Volltextabfragen, die den Thesaurus verwenden.  
  
 [sp_fulltext_pendingchanges](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
 Gibt nicht verarbeitete Änderungen, z. B. ausstehende Einfügungs-, Update- und Löschvorgänge, für eine angegebene Tabelle zurück, die die Änderungsnachverfolgung verwendet.  
  
 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
 Ändert die Servereigenschaften der Volltextsuche für SQL Server.  
  
 [sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)  
 Markiert eine Tabelle für die Volltextindizierung oder hebt die Markierung auf.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwendung [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md), [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md), und [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) stattdessen.  
  
 [sp_help_fulltext_catalog_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql.md)  
 Gibt eine Liste aller Komponenten (Filter, Wörtertrennung und Protokollhandler) zurück, die für alle Volltextkataloge in der aktuellen Datenbank verwendet werden.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_help_fulltext_catalogs](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
 Gibt die ID, den Namen, das Stammverzeichnis, den Status und die Anzahl von volltextindizierten Tabellen für den angegebenen Volltextkatalog zurück.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) stattdessen die Katalogsicht.  
  
 [sp_help_fulltext_catalogs_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)  
 Verwendet einen Cursor, um die ID, den Namen, das Stammverzeichnis, den Status und die Anzahl der volltextindizierten Tabellen für den angegebenen Volltextkatalog zurückzugeben.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) stattdessen die Katalogsicht.  
  
 [sp_help_fulltext_columns](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)  
 Gibt die Spalten zurück, die für die Volltextindizierung angegeben wurden.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) stattdessen die Katalogsicht.  
  
 [sp_help_fulltext_columns_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)  
 Verwendet einen Cursor, um eine Liste der Spalten zurückzugeben, die für die Volltextindizierung angegeben wurden.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) stattdessen die Katalogsicht.  
  
 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
 Gibt Informationen zu registrierten Komponenten wie Wörtertrennung, Filter und Protokollhandler sowie eine Liste der Bezeichner von Datenbanken und Volltextkatalogen zurück, die eine angegebene Komponente verwendet haben.  
  
 [sp_help_fulltext_tables](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)  
 Gibt eine Liste der Tabellen zurück, die für die Volltextindizierung registriert sind.  
  
 [sp_help_fulltext_tables_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)  
 Gibt eine Liste der Tabellen zurück, die für die Volltextindizierung registriert sind.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) stattdessen die Katalogsicht.  
  
## <a name="semantic-search-stored-procedures"></a>Gespeicherte Prozeduren für die semantische Suche  
 [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)  
 Registriert eine im Voraus aufgefüllte semantische Sprachstatistikdatenbank in der aktuellen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)  
 Hebt die Registrierung einer vorhandenen semantischen Sprachstatistikdatenbank in der aktuellen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf und löscht alle zugeordneten Metadaten.  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche und semantische Suche-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)   
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)  
  
  
