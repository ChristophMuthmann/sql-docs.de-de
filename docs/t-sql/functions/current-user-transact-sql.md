---
title: CURRENT_USER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_USER
- CURRENT_USER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- niladic functions
- CURRENT_USER
- users [SQL Server], names
ms.assetid: 29248949-325b-4063-9f55-5a445fb35c6e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9edbc344723da335de150f5e829820eaef1d983e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="currentuser-transact-sql"></a>CURRENT_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt den Namen des aktuellen Benutzers zurück. Diese Funktion entspricht USER_NAME().
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CURRENT_USER  
```  

## <a name="return-types"></a>Rückgabetypen
**sysname**
  
## <a name="remarks"></a>Hinweise  
Mit CURRENT_USER wird der Name des aktuellen Sicherheitskontexts zurückgegeben. Wird CURRENT_USER nach dem Kontextwechsel eines Aufrufs von EXECUTE AS ausgeführt, gibt CURRENT_USER den Namen des Kontexts zurück, dessen Identität angenommen wurde. Wenn ein Windows-Prinzipal über die Mitgliedschaft in einer Gruppe auf die Datenbank zugegriffen hat, wird der Name des Windows-Prinzipals anstelle des Namens der Gruppe zurückgegeben.
  
Um den Benutzernamen des aktuellen Benutzers zurückzugeben, finden Sie unter [SUSER_NAME &#40; Transact-SQL &#41; ](../../t-sql/functions/suser-name-transact-sql.md) und [SYSTEM_USER &#40; Transact-SQL &#41; ](../../t-sql/functions/system-user-transact-sql.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-currentuser-to-return-the-current-user-name"></a>A. Verwenden von CURRENT_USER zur Rückgabe des aktuellen Benutzernamens  
Im folgenden Beispiel wird der Name des aktuellen Benutzers zurückgegeben.
  
```sql
SELECT CURRENT_USER;  
GO  
```  
  
### <a name="b-using-currentuser-as-a-default-constraint"></a>B. Verwenden von CURRENT_USER als DEFAULT-Einschränkung  
Im folgenden Beispiel wird eine Tabelle erstellt, die `CURRENT_USER` als `DEFAULT`-Einschränkung für die `order_person`-Spalte in einer Zeile mit Verkaufszahlen verwendet.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'orders22')  
   DROP TABLE orders22;  
GO  
SET NOCOUNT ON;  
CREATE TABLE orders22  
(  
order_id int IDENTITY(1000, 1) NOT NULL,
cust_id  int NOT NULL,
order_date smalldatetime NOT NULL DEFAULT GETDATE(),
order_amt money NOT NULL,
order_person char(30) NOT NULL DEFAULT CURRENT_USER
);  
GO  
```  
  
Der folgende Code fügt einen Datensatz in die Tabelle ein. Der Benutzer, der diese Anweisungen ausführt, heißt `Wanida`.
  
```sql
INSERT orders22 (cust_id, order_amt)  
VALUES (5105, 577.95);  
GO  
SET NOCOUNT OFF;  
GO  
```  
  
In der folgenden Abfrage werden alle Informationen aus der `orders22`-Tabelle ausgewählt.
  
```sql
SELECT * FROM orders22;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
order_id    cust_id     order_date           order_amt    order_person
----------- ----------- -------------------- ------------ ------------
1000        5105        2005-04-03 23:34:00  577.95       Wanida
  
(1 row(s) affected)
```
  
### <a name="c-using-currentuser-from-an-impersonated-context"></a>C. Verwenden von CURRENT_USER aus einem Kontext, dessen Identität angenommen wurde  
Im folgenden Beispiel führt Benutzer `Wanida` den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code aus.
  
```sql
SELECT CURRENT_USER;  
GO  
EXECUTE AS USER = 'Arnalfo';  
GO  
SELECT CURRENT_USER;  
GO  
REVERT;  
GO  
SELECT CURRENT_USER;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Wanida
Arnalfo
Wanida
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-currentuser-to-return-the-current-user-name"></a>D: Verwenden von CURRENT_USER zur Rückgabe des aktuellen Benutzernamens  
Im folgenden Beispiel wird der Name des aktuellen Benutzers zurückgegeben.
  
```sql
SELECT CURRENT_USER;  
```  
  
## <a name="see-also"></a>Siehe auch
[USER_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)  
[SYSTEM_USER &#40; Transact-SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


