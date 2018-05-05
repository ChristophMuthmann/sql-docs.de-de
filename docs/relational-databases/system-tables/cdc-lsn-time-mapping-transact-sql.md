---
title: CDC. lsn_time_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 64dfd747bb58ae92161c1c05889f808113e8a77e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cdclsntimemapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Transaktion zurück, für die Zeilen in einer Änderungstabelle aufgezeichnet sind. Diese Tabelle wird verwendet, um die Commitwerte der Protokollfolgenummer (Log Sequence Number, LSN) mit dem Commitzeitpunkt der Transaktion zu verknüpfen. Außerdem können Einträge protokolliert werden, für die keine Einträge in Änderungstabellen aufgezeichnet sind. Auf diese Weise kann die Tabelle den Abschluss der LSN-Verarbeitung in Phasen aufzeichnen, in denen wenige oder keine Änderungsaktivitäten stattfinden.  
  
 Es wird empfohlen, die Systemtabellen nicht direkt abzufragen. Führen Sie stattdessen die [fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) und [fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) Systemfunktionen.  
    
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|LSN der Transaktion, für die ein Commit ausgeführt wurde.|  
|**tran_begin_time**|**datetime**|Startzeit der Transaktion, die der LSN zugeordnet ist.|  
|**tran_end_time**|**datetime**|Zeitpunkt, zu dem die Transaktion beendet wurde.|  
|**tran_id**|**varbinary(10)**|ID der Transaktion.|  
  
## <a name="see-also"></a>Siehe auch  
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [CDC. &#60;Capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
