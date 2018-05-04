---
title: Sys. dm_tran_version_store (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d543c994c5d5ede69a5ddf347ef15d5a719bf72
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtranversionstore-transact-sql"></a>sys.dm_tran_version_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine virtuelle Tabelle zurück, die alle Versionsdatensätze im Versionsspeicher anzeigt. Die Ausführung von**sys.dm_tran_version_store** ist ineffizient, da der gesamte Versionsspeicher abgefragt wird und dieser sehr groß sein kann.  
  
 Jeder Versionsdatensatz wird als Binärdaten zusammen mit Protokollierungs- oder Statusinformationen gespeichert. Ähnlich wie Datensätze in Datenbanktabellen werden die Versionsspeicherdatensätze in 8192 Bytes umfassenden Seiten gespeichert. Falls ein Datensatz größer ist als 8192 Bytes, wird er in zwei unterschiedliche Datensätze geteilt.  
  
 Da der Versionsdatensatz als Binärdaten gespeichert wird, treten keine Probleme mit unterschiedlichen Sortierungen aus unterschiedlichen Datenbanken auf. Suchen Sie mit **sys.dm_tran_version_store** die vorherigen Versionen der Zeilen in der binären Darstellung, so, wie sie im Versionsspeicher vorhanden sind.  
  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Sequenznummer der Transaktion, die die Datensatzversion generiert.|  
|**version_sequence_num**|**bigint**|Sequenznummer des Versionsdatensatzes. Dieser Wert ist in der die Version generierenden Transaktion eindeutig.|  
|**database_id**|**int**|Datenbank-ID des Versionsdatensatzes.|  
|**rowset_id**|**bigint**|Rowset-ID des Datensatzes.|  
|**status**|**tinyint**|Gibt an, ob ein Versionsdatensatz auf zwei Datensätze aufgeteilt wurde. Falls der Wert 0 beträgt, wird der Datensatz in einer Seite gespeichert. Falls der Wert 1 beträgt, ist der Datensatz auf zwei Datensätze aufgeteilt, die in zwei unterschiedlichen Seiten gespeichert sind.|  
|**min_length_in_bytes**|**smallint**|Maximale Länge des Datensatzes (in Bytes).|  
|**record_length_first_part_in_bytes**|**smallint**|Länge des ersten Teiles des Versionsdatensatzes (in Bytes).|  
|**record_image_first_part**|**varbinary(8000)**|Binäres Image des ersten Teiles des Versionsdatensatzes.|  
|**record_length_second_part_in_bytes**|**smallint**|Länge des zweiten Teiles des Versionsdatensatzes (in Bytes).|  
|**record_image_second_part**|**varbinary(8000)**|Binäres Image des zweiten Teiles des Versionsdatensatzes.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Testszenario verwendet, in dem vier gleichzeitige Transaktionen, die jeweils durch eine Transaktionssequenznummer (XSN) identifiziert werden, in einer Datenbank ausgeführt werden, für die die Optionen ALLOW_SNAPSHOT_ISOLATION und READ_COMMITTED_SNAPSHOT auf ON festgelegt sind. Die folgenden Transaktionen werden ausgeführt:  
  
-   XSN-57 ist ein Updatevorgang auf der serialisierbaren Isolationsstufe.  
  
-   XSN-58 entspricht XSN-57.  
  
-   XSN-59 ist ein Select-Vorgang auf der Momentaufnahmeisolationsstufe.  
  
-   XSN-60 entspricht XSN-59.  
  
 Die folgende Abfrage wird ausgeführt.  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 Die Ausgabe zeigt an, dass XSN-57 drei Zeilenversionen aus einer Tabelle und XSN-58 eine Zeilenversion aus einer anderen Tabelle erstellt hat.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
