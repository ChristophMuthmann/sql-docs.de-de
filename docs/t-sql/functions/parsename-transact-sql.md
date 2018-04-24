---
title: PARSENAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5e029bfebb297c58f3643acf55968ab901a3dea8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt den angegebenen Teil eines Objektnamens zurück. Die Teile eines Objekts, die abgerufen werden können, sind der Objektname, der Besitzername, der Datenbankname und der Servername.  
  
> [!NOTE]  
>  Die PARSENAME-Funktion zeigt nicht an, ob ein Objekt mit dem angegebenen Namen vorhanden ist. PARSENAME gibt lediglich den angegebenen Teil des gegebenen Objektnamens zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>Argumente  
 '*object_name*'  
 Der Name des Objekts, für das der angegebene Objektteil abgerufen werden soll. *database_name* ist vom Datentyp **sysname**. Dieser Parameter ist ein optional gekennzeichneter Objektname. Wenn alle Teile des Objektnamens gekennzeichnet sind, besteht dieser Name aus vier Teilen: dem Server-, Datenbank, Besitzer- und Objektnamen.  
  
 *object_piece*  
 Der Objektteil, der zurückgegeben werden soll. *object_piece* ist vom Datentyp **int** und kann folgende Werte haben:  
  
 1 = Objektname  
  
 2 = Schemaname  
  
 3 = Datenbankname  
  
 4 = Servername  
  
## <a name="return-types"></a>Rückgabetypen  
 **nchar**  
  
## <a name="remarks"></a>Remarks  
 PARSENAME gibt NULL zurück, wenn eine der folgenden Bedingungen wahr ist:  
  
-   Entweder für *object_name* oder für *object_piece* wird NULL zurückgegeben.  
  
-   Ein Syntaxfehler tritt auf.  
  
 Der angeforderte Objektteil hat eine Länge von 0 und ist kein gültiger [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner. Ein Objektname mit der Länge 0 macht den gesamten qualifizierten Namen ungültig.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `PARSENAME` verwendet, um Informationen zur `Person`-Tabelle in der `AdventureWorks2012`-Datenbank zurückzugeben.  
  
```  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

