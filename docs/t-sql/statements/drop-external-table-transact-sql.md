---
title: DROP EXTERNAL TABLE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: feb9edbfae458d45f1d956c7ccbdf604cbfbea33
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-external-table-transact-sql"></a>DROP EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Entfernt eine externe PolyBase-Tabelle aus einer Datenbank. Dadurch werden externe Daten nicht gelöscht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>Argumente  
 [ *database_name* . [*schema_name*] . | *schema_name* . ] *table_name*  
 Der ein- bis dreiteilige Name der externen Tabelle, die entfernt werden soll. Der Tabellenname kann optional das Schema oder die Datenbank und das Schema enthalten.  
  
## <a name="permissions"></a>Berechtigungen  
  
-   Erfordert die Berechtigung **ALTER** für das Schema, zu dem die Tabelle gehört.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Das Löschen einer externen Tabelle entfernt alle Metadaten, die mit der Tabelle verknüpft sind. Externe Daten werden nicht gelöscht.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-basic-syntax"></a>A. Verwenden einer grundlegenden Syntax  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. Löschen einer externen Tabelle aus der aktuellen Datenbank  
 Im folgenden Beispiel werden die `ProductVendor1`-Tabelle, ihre Daten, ihre Indizes und alle davon abhängigen Sichten aus der aktuellen Datenbank entfernt.  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. Löschen einer Tabelle aus einer anderen Datenbank  
 Im folgenden Beispiel wird die `SalesPerson`-Tabelle in der `EasternDivision`-Datenbank gelöscht.  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

