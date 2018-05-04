---
title: Sys. fn_cdc_map_time_to_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f463c01205b574334dd52263cb056f3a2daea62f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Wert der Log Sequence (Number, LSN) aus der **Start_lsn** Spalte in der [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) Systemtabelle für die angegebene Zeit. Sie können diese Funktion verwenden, um Datetime-Bereiche systematisch dem LSN-basierten Bereich von Change Data Capture-Enumerationsfunktionen benötigt zuzuordnen [CDC. fn_cdc_get_all_changes_ < Capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) und [cdc.fn _cdc_get_net_changes_ < Capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) um datenänderungen innerhalb dieses Bereichs zurückzugeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>Argumente  
 **"**< Relational_operator >**"** {größten weniger als | größten kleiner als oder gleich | kleinsten größer | kleinsten größer als oder gleich}  
 Wird verwendet, um einen eindeutigen LSN-Wert in der **cdc.lsn_time_mapping** -Tabelle mit zugeordnetem **tran_end_time** -Wert zu identifizieren, der der Beziehung entspricht, wenn er mit dem Wert *tracking_time* verglichen wird.  
  
 *relational_operator* ist **nvarchar(30)**  
  
 *tracking_time*  
 Der datetime-Wert, mit dem verglichen werden soll. *tracking_time* ist **datetime**  
  
## <a name="return-type"></a>Rückgabetyp  
 **binary(10)**  
  
## <a name="remarks"></a>Hinweise  
 Das folgende Szenario veranschaulicht, wie **sys.fn_cdc_map_time_lsn** verwendet werden kann, um datetime-Bereiche LSN-Bereichen zuzuordnen. Angenommen, ein Consumer möchte täglich Änderungsdaten extrahieren. In diesem Fall interessiert sich der Consumer nur für die Änderungen an einem bestimmten Tag bis einschließlich Mitternacht. Die Untergrenze des Zeitbereichs wäre bis Mitternacht des vorangehenden Tags (nicht einschließlich Mitternacht). Die Obergrenze wäre bis einschließlich Mitternacht des bestimmten Tags. Im folgenden Beispiel wird gezeigt, wie Sie die Funktion **sys.fn_cdc_map_time_to_lsn** verwenden können, um diesen zeitbasierten Bereich dem LSN-basierten Bereich zuzuordnen, der von den Change Data Capture-Enumerationsfunktionen benötigt wird, um alle Änderungen innerhalb dieses Bereichs zurückzugeben.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 Der relationale '`smallest greater than`'-Operator wird verwendet, um auf die Änderungen einzuschränken, die nach Mitternacht am vorangehenden Tag aufgetreten sind. Wenn mehrere Einträge mit unterschiedlichen LSN-Werten der **Tran_end_time** Wert identifiziert, als die untere Grenze in der [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) Tabelle, die Funktion gibt die kleinste LSN, die sicherstellen, dass zurück alle Einträge sind enthalten. Für die obere Grenze wird der relationale '`largest less than or equal to`'-Operator verwendet, um sicherzustellen, dass der Bereich alle Einträge für den Tag enthält, einschließlich der Einträge, die Mitternacht als ihren **tran_end_time** -Wert haben. Wenn mehrere Einträge mit unterschiedlichen LSN-Werten den Wert **tran_end_time** verwenden, der als obere Grenze identifiziert ist, wird die Funktion den größten LSN-Wert zurückgeben, um sicherzustellen, dass alle Einträge enthalten sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `sys.fn_cdc_map_time_lsn` Funktion, um zu bestimmen, ob es keine Zeilen in gibt der [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) Tabelle mit einer **Tran_end_time** -Wert, der größer als oder gleich Mitternacht ist. Mit dieser Abfrage kann beispielsweise bestimmt werden, ob der Aufzeichnungsprozess bereits die Änderungen verarbeitet hat, für die bis Mitternacht des vorangehenden Tags ein Commit ausgeführt wurde, sodass mit dem Extrahieren von Änderungsdaten für diesen Tag fortgefahren werden kann.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>Siehe auch  
 [cdc.lsn_time_mapping &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
