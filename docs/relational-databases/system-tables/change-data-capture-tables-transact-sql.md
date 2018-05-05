---
title: Ändern Sie die Data Capture-Tabellen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2a4f5aecfebeac24b8e3559d0cdbc770c68acb88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="change-data-capture-tables-transact-sql"></a>Change Data Capture-Tabellen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Change Data Capture ermöglicht eine Änderungsnachverfolgung für Tabellen, sodass DML (Data Manipulation Language)- und DDL (Data Definition Language)-Änderungen an den Tabellen inkrementell in ein Data Warehouse geladen werden können. In den Themen in diesem Abschnitt werden die Systemtabellen beschrieben, in denen die von Change Data Capture-Vorgängen verwendeten Informationen gespeichert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [cdc.<capture_instance>_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
 Gibt eine Zeile für jede Änderung an einer aufgezeichneten Spalte in der zugeordneten Quelltabelle zurück.  
  
 [cdc.captured_columns](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
 Gibt eine Zeile für jede in einer Aufzeichnungsinstanz nachverfolgte Spalte zurück.  
  
 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
 Gibt eine Zeile pro Änderungstabelle in der Datenbank zurück.  
  
 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)  
 Gibt eine Zeile für jede Änderung an der Datendefinitionssprache (DDL) zurück, die an Tabellen vorgenommen wurde, die für Change Data Capture aktiviert wurden.  
  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)  
 Gibt eine Zeile für jede Transaktion zurück, für die Zeilen in einer Änderungstabelle aufgezeichnet sind. Diese Tabelle wird verwendet, um die Commitwerte der Protokollfolgenummer (Log Sequence Number, LSN) mit dem Commitzeitpunkt der Transaktion zu verknüpfen.  
  
 [cdc.index_columns](../../relational-databases/system-tables/cdc-index-columns-transact-sql.md)  
 Gibt eine Zeile für jede Indexspalte zurück, die einer Änderungstabelle zugeordnet ist.  
  
 [cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 Gibt die Konfigurationsparameter für Change Data Capture-Agentaufträge zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Ändern Sie die Data Capture-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
