---
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 63065dcee0d1f7784e7be396273785f741ef44c7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt den angegebenen Teil eines Objektnamens zurück. Die Teile eines Objekts, die abgerufen werden können, sind der Objektname, der Besitzername, der Datenbankname und der Servername.  
  
> [!NOTE]  
>  Die PARSENAME-Funktion zeigt nicht an, ob ein Objekt mit dem angegebenen Namen vorhanden ist. PARSENAME gibt lediglich den angegebenen Teil des gegebenen Objektnamens zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>Argumente  
 "*Object_name*"  
 Der Name des Objekts, für das der angegebene Objektteil abgerufen werden soll. *Object_name* ist **Sysname**. Dieser Parameter ist ein optional gekennzeichneter Objektname. Wenn alle Teile des Objektnamens gekennzeichnet sind, besteht dieser Name aus vier Teilen: dem Server-, Datenbank, Besitzer- und Objektnamen.  
  
 *object_piece*  
 Der Objektteil, der zurückgegeben werden soll. *Object_piece* ist vom Typ **Int**, und kann folgende Werte haben:  
  
 1 = Objektname  
  
 2 = Schemaname  
  
 3 = Datenbankname  
  
 4 = Servername  
  
## <a name="return-types"></a>Rückgabetypen  
 **nchar**  
  
## <a name="remarks"></a>Hinweise  
 PARSENAME gibt NULL zurück, wenn eine der folgenden Bedingungen wahr ist:  
  
-   Entweder *Object_name* oder *Object_piece* ist NULL.  
  
-   Ein Syntaxfehler tritt auf.  
  
 Der angeforderte Objektteil hat eine Länge von 0 und ist kein gültiger [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Bezeichner. Ein Objektname mit der Länge 0 macht den gesamten qualifizierten Namen ungültig.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `PARSENAME` verwendet, um Informationen zur `Person`-Tabelle in der `AdventureWorks2012`-Datenbank zurückzugeben.  
  
```  
USE AdventureWorks2012;  
SELECT PARSENAME('AdventureWorks2012..Person', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorks2012..Person', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorks2012..Person', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorks2012..Person', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Object Name
------------------------------
Person

(1 row(s) affected)

Schema Name
------------------------------
(null)

(1 row(s) affected)

Database Name
------------------------------
AdventureWorks2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
 ```
 
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
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
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  


