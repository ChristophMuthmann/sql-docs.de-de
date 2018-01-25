---
title: DROP EXTERNAL TABLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: "12"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e29508550528b1f98318bec26676707c72f0b5fc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-table-transact-sql"></a>DROP EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Entfernt eine externe PolyBase-Tabelle aus. Dadurch wird die externen Daten nicht gelöscht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>Argumente  
 [ *database_name* . [*schema_name*] . | *schema_name* . ] *table_name*  
 Der One - dreiteilige Name der externen Tabelle zu entfernen. Der Tabellenname kann optional das Schema oder die Datenbank und das Schema einschließen.  
  
## <a name="permissions"></a>Berechtigungen  
  
-   Erfordert **ALTER** Berechtigung für das Schema, zu dem die Tabelle gehört.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Löschen eine externe Tabelle entfernt alle Metadaten der Tabelle verknüpft. Die externen Daten werden nicht gelöscht.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-basic-syntax"></a>A. Verwenden die grundlegende syntax  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. Löschen eine externe Tabelle aus der aktuellen Datenbank  
 Im folgenden Beispiel wird die `ProductVendor1` Tabelle, die Daten, Indizes und alle abhängigen Ansichten aus der aktuellen Datenbank.  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. Löschen einer Tabelle aus einer anderen Datenbank  
 Im folgenden Beispiel wird die `SalesPerson`-Tabelle in der `EasternDivision`-Datenbank gelöscht.  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

