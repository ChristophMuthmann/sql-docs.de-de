---
title: Sys. fn_cdc_increment_lsn (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn
- fn_cdc_increment_lsn
dev_langs: TSQL
helpviewer_keywords:
- fn_cdc_increment_lsn
- sys.fn_cdc_increment_lsn
ms.assetid: e53b6703-358b-4c9a-912a-8f7c7331069b
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c1715fc71449c822db2bb692bc2cce4005cb5a1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysfncdcincrementlsn-transact-sql"></a>sys.fn_cdc_increment_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die nächste Protokollfolgenummer (Log Sequence Number, LSN) in der auf der angegebenen LSN basierenden Reihenfolge zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_cdc_increment_lsn ( lsn_value )  
```  
  
## <a name="arguments"></a>Argumente  
 *lsn_value*  
 LSN-Wert. *lsn_value* ist **binary(10)**  
  
## <a name="return-type"></a>Rückgabetyp  
 **binary(10)**  
  
## <a name="remarks"></a>Hinweise  
 Der von der Funktion zurückgegebene LSN-Wert ist immer größer als der angegebene Wert. Zwischen den beiden Werten befinden sich keine LSN-Werte.  
  
 Wenn Sie einen Änderungsdatenstrom systematisch im Verlauf der Zeit abfragen möchten, können Sie den Abfragefunktionsaufruf immer dann periodisch wiederholen, wenn ein neues Abfrageintervall zum Begrenzen der Änderungen in der Abfrage zurückgegeben wird. Um sicherzustellen, dass keine Daten verloren gehen, wird häufig die obere Grenze der vorherigen Abfrage verwendet, um die untere Grenze der nachfolgenden Abfrage zu generieren. Da es sich beim Abfrageintervall um ein geschlossenes Intervall handelt, muss die neue untere Grenze höher als die vorherige obere Grenze liegen, während sie zugleich niedrig genug liegen muss, um sicherzustellen, dass keine Änderungen mit LSN-Werten zwischen diesem Wert und der alten oberen Grenze vorhanden sind. Es wird die Funktion sys.fn_cdc_increment_lsn verwendet, um diesen Wert zu erhalten.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Datenbankrolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `sys.fn_cdc_increment_lsn` verwendet, um einen neuen unteren Grenzwert für eine Change Data Capture-Abfrage basierend auf der oberen Grenze zu generieren, die von einer vorherigen Abfrage gespeichert wurde und die in der `@save_to_lsn`-Variablen gespeichert ist.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @save_to_lsn binary(10);  
SET @save_to_lsn = <previous_upper_bound_value>;  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * from cdc.fn_cdc_get_all_changes_HumanResources_Employee( @from_lsn, @to_lsn, 'all' );  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [fn_cdc_decrement_lsn &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)   
 [CDC. fn_cdc_get_all_changes_ &#60; Capture_instance &#62;  &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [CDC. fn_cdc_get_net_changes_ &#60; Capture_instance &#62; &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Über Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
