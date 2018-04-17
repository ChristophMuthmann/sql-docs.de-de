---
title: Sp_batch_params (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9843453dce8234e97b40e3ca3be45ed1e48d7c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spbatchparams-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Rowset, das Informationen zu den Parametern, die in enthaltenen enthält eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch. **Sp_batch_params** nur analysiert den angegebenen Batch und gibt Informationen zu eingebetteten Parameterwerten zurück. Hiermit wird der Batch nicht ausgeführt, und die Ausführungsumgebung wird nicht geändert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@tsqlbatch =**] **"***Tsqlbatch***"**  
 Ist eine Unicode-Zeichenfolge, enthält eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung oder eines Batches, die für die Parameterwerte Informationen sind, werden sollen. *TSqlBatch* ist **nvarchar(max)** oder implizit in **nvarchar(max)**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**PARAMETERNAME**|**sysname**|Name des Parameters, den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Batch gefunden hat|  
|**COLUMN_TYPE**|**smallint**|Dieses Feld gibt einen der folgenden Werte zurück:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> Diese Spalte hat immer den Wert 0.|  
|**DATA_TYPE**|**smallint**|Der Datentyp des Parameters (ein ganzzahliger Code für einen ODBC-Datentyp). Wenn dieser Datentyp keinem ISO-Datentyp zugeordnet werden kann, lautet der Wert NULL. Den Namen des systemeigenen Datentyps wird zurückgegeben, der **TYPE_NAME** Spalte. Dieser Wert ist immer NULL.|  
|**TYPE_NAME**|**sysname**|Die Zeichenfolgendarstellung des Datentyps gemäß der Darstellung durch das zugrunde liegende DBMS. Dieser Wert ist NULL.|  
|**PRECISION**|**int**|Die Anzahl von signifikanten Stellen. Der Rückgabewert für die **Genauigkeit** Spalte hat die Basis 10.|  
|**LENGTH**|**int**|Die Übertragungsgröße der Daten. Dieser Wert ist NULL.|  
|**SKALIERUNG**|**smallint**|Die Anzahl der Ziffern rechts vom Dezimalzeichen Dieser Wert ist NULL.|  
|**BASIS**|**smallint**|Die Basis für die Darstellung numerischer Datentypen. Dieser Wert ist NULL.|  
|**NULL-WERTE ZULÄSST**|**smallint**|Gibt die NULL-Zulässigkeit an:<br /><br /> 1 = Parameterdatentyp mit NULL-Werten ist zulässig.<br /><br /> 0 = NULL-Werte sind nicht zulässig.<br /><br /> Dieser Wert ist NULL.|  
|**SQL_DATA_TYPE**|**smallint**|Der Wert des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyps, wie er im TYPE-Feld des Deskriptors angezeigt wird. Diese Spalte ist identisch mit der **DATA_TYPE** Spalte, mit Ausnahme der **"DateTime"** und ISO **Intervall** Datentypen. Diese Spalte gibt immer einen Wert zurück. Dieser Wert ist NULL.|  
|**SQL_DATETIME_SUB**|**smallint**|Die **"DateTime"** oder ISO **Intervall** subcode, wenn der Wert der **SQL_DATA_TYPE** SQL_DATETIME oder SQL_INTERVAL. Bei allen Datentypen außer **"DateTime"** und ISO **Intervall**, ist diese Spalte NULL. Dieser Wert ist NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Maximale Länge in Bytes, der eine **Zeichen** oder **binäre** -Datentypparameter. Bei allen anderen Datentypen gibt diese Spalte einen NULL-Wert zurück. Dieser Wert ist immer NULL.|  
|**ORDINAL_POSITION**|**int**|Die Ordnungsposition des Parameters innerhalb des Batches. Wenn der Parametername mehrmals wiederholt wird, enthält diese Spalte die Ordnungszahl des ersten Vorkommens. Der erste Parameter hat die Ordnungszahl 1. Diese Spalte gibt immer einen Wert zurück.|  
  
## <a name="permissions"></a>Berechtigungen  
 Berechtigung zum Ausführen von **Sp_batch_params** erteilt **öffentlichen**.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie eine Abfrage an `sp_batch_params` übergeben wird. Im Resultset wird die Liste der eingebetteten Parameterwerte aufgezählt.  
  
```  
DECLARE @SQLString nvarchar(500);  
/* Build the SQL string */  
SET @SQLString =  
     N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
     WHERE BusinessEntityID = @BusinessEntityID';  
EXECUTE sp_batch_params @SQLString;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von gespeicherten Prozeduren](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Ausführen von gespeicherten Prozeduren: Themen zur Vorgehensweise &#40;ODBC&#41;](http://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [Ausführen von gespeicherten Prozeduren & #40; OLE DB & #41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
