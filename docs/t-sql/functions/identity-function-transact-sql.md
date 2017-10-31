---
title: IDENTITY (Funktion) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 43d42425842def7572cf7961a89cae355e6b78ae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="identity-function-transact-sql"></a>IDENTITY (Funktion) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird nur in einer SELECT-Anweisung mit einer INTO verwendet *Tabelle* -Klausel, um eine Identitätsspalte in eine neue Tabelle einzufügen. Die IDENTITY-Funktion ähnelt der mit CREATE TABLE und ALTER TABLE verwendeten IDENTITY-Eigenschaft, ist jedoch nicht mit ihr identisch.  
  
> [!NOTE]  
>  Weitere Informationen zu einer automatisch inkrementierten Zahl, die in mehreren Tabellen verwendet oder aus Anwendungen aufgerufen werden kann, ohne dass auf eine Tabelle verwiesen wird, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
## <a name="arguments"></a>Argumente  
 *data_type*  
 Der Datentyp der Identitätsspalte. Gültige Datentypen für eine Identitätsspalte sind beliebige Datentypen aus der ganzzahligen Datentypkategorie, mit Ausnahme von der **Bit** -Datentyp oder **decimal** -Datentyp.  
  
 *Startwert*  
 Der ganzzahlige Wert, der der ersten Zeile in der Tabelle zugewiesen werden soll. Jede weitere Zeile hat den nächsten Identitätswert, was identisch mit den letzten Identitätswert ist sowie die *Inkrement* Wert. Wenn weder *Ausgangswert* noch *Inkrement* angegeben ist, wird standardmäßig auf 1.  
  
 *Inkrement*  
 Ist der ganzzahlige Wert hinzufügen zu den *Ausgangswert* -Wert nachfolgende Zeilen in der Tabelle.  
  
 *Spaltenname*  
 Der Name der Spalte, die in die neue Tabelle eingefügt werden soll.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt dem *Data_type*.  
  
## <a name="remarks"></a>Hinweise  
 Da diese Funktion eine Spalte in einer Tabelle erstellt, muss für die Spalte ein Name in der Auswahlliste angegeben werden. Dies kann auf zwei Arten geschehen:  
  
```  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
  
```  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Zeilen aus der `Contact`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank in eine neue Tabelle namens `NewContact` eingefügt. Die IDENTITY-Funktion bewirkt, dass die Identifikationsnummern in der `NewContact`-Tabelle bei 100 anstatt bei 1 beginnen.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [Wählen Sie @local_variable &#40; Transact-SQL &#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [Sys. identity_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  

