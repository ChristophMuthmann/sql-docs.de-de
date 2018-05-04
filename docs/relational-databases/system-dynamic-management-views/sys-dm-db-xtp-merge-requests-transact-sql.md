---
title: Sys.dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: relational-databases
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f92ac092e3b24023abc26c1ab1893fba87ed228
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]


Verfolgt Zusammenführungsanforderungen für Datenbanken nach. Die Merge-Anforderung kann von SQL Server generiert wurde, oder die Anforderung wurde von einem Benutzer mit vorgenommen [sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md).

> [!NOTE]
> Diese dynamische verwaltungssicht (DMV), sys.dm_db_xtp_merge_requests, bis Microsoft SQL Server 2014 vorhanden ist.
> 
> Aber beginnend mit SQL Server 2016 dieser DMV nicht mehr gültig.

## <a name="columns-in-the-report"></a>Spalten im Bericht

| Spaltenname | Datentyp | Description |
| :-- | :-- | :-- |
| request_state | tinyint | Der Status der Zusammenführungsanforderung:<br/>0 = Requested<br/>1 = Pending<br/>2 = installiert<br/>3 = Abandoned |
| request_state_desc | nvarchar(60) | Die Bedeutung für den aktuellen Status der Anforderung:<br/><br/>Angeforderte - ist eine zusammenführungsanforderung vorhanden.<br/>Ausstehende - ist die Zusammenführung verarbeitet.<br/>Installiert – ist die Zusammenführung abgeschlossen.<br/>Abgebrochene - konnte die Zusammenführung nicht abgeschlossen, möglicherweise aufgrund fehlender Speicher. |
| destination_file_id | GUID | Der eindeutige Bezeichner der Zieldatei für die Zusammenführung der Quelldateien. |
| lower_bound_tsn | bigint | Der minimale Zeitstempel für die als Ziel verwendete zusammengeführte Datei. Der niedrigste Transaktionszeitstempel aller zusammenzuführenden Quelldateien. |
| upper_bound_tsn | bigint | Der maximale Zeitstempel für die als Ziel verwendete zusammengeführte Datei. Der höchste Transaktionszeitstempel aller zusammenzuführenden Quelldateien. |
| collection_tsn | bigint | Der Zeitstempel, bei dem die aktuelle Zeile gesammelt werden kann.<br/><br/>Eine Zeile mit dem Status "Installed" wird entfernt, wenn checkpoint_tsn größer als collection_tsn ist.<br/><br/>Wenn checkpoint_tsn kleiner als collection_tsn ist, wird eine Zeile mit dem Status "Abandoned" entfernt. |
| checkpoint_tsn | bigint | Die Zeit, zu der der Prüfpunkt gestartet wurde.<br/><br/>Alle Löschvorgänge, die von Transaktionen mit einem niedrigeren Zeitstempel ausgeführt werden, werden in der neuen Datendatei berücksichtigt. Die übrigen Löschvorgänge werden in die als Ziel verwendete Änderungsdatei verschoben. |
| sourcenumber_file_id | GUID | Bis zu 16 interne Datei-IDs, durch die die Quelldateien in der Zusammenführung eindeutig identifiziert werden. |

## <a name="permissions"></a>Berechtigungen

Erfordert die VIEW DATABASE STATE-Berechtigung für die aktuelle Datenbank.

## <a name="see-also"></a>Siehe auch

[Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)


