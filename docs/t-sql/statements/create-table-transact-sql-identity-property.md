---
title: IDENTITY (Eigenschaft) (Transact-SQL) | Microsoft Docs
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
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1eb7f960210ec89a66f1307d8476e6d47494861f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql-identity-property"></a>Erstellen der Tabelle (Transact-SQL) IDENTITY (Eigenschaft)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Erstellt eine Identitätsspalte in einer Tabelle. Diese Eigenschaft wird in den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen CREATE TABLE und ALTER TABLE verwendet.  
  
> [!NOTE]  
>  Die IDENTITY-Eigenschaft unterscheidet sich von der SQL-DMO **Identität** Eigenschaft, die die Zeile Identity-Eigenschaft einer Spalte verfügbar macht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IDENTITY [ (seed , increment) ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Startwert*  
 Der Wert, der für die erste in die Tabelle geladene Zeile verwendet wird.  
  
 *Inkrement*  
 Der inkrementelle Wert, der zum Identitätswert der zuvor geladenen Zeile addiert wird.  
  
 Sie müssen entweder sowohl den Ausgangswert als auch den inkrementellen Wert oder keinen von beiden angeben. Wurden Ausgangswert und inkrementeller Wert nicht angegeben, ist der Standardwert (1,1).  
  
## <a name="remarks"></a>Hinweise  
 Identitätsspalten können zum Generieren von Schlüsselwerten verwendet werden. Die Identitätseigenschaft für eine Spalte garantiert Folgendes:  
  
-   Jeder neue Wert wird auf Grundlage des aktuellen Ausgangswerts und Inkrements generiert.  
  
-   Jeder neue Wert für eine bestimmte Transaktion unterscheidet sich von anderen gleichzeitigen Transaktionen für die Tabelle.  
  
 Die Identitätseigenschaft für eine Spalte garantiert nicht Folgendes:  
  
-   **Eindeutigkeit des Werts** – Eindeutigkeit muss erzwungen werden, mithilfe einer **PRIMÄRSCHLÜSSEL** oder **UNIQUE** Einschränkung oder **UNIQUE** Index.  
  
-   **Aufeinanderfolgende Werte innerhalb einer Transaktion** – eine Transaktion Einfügen mehrerer Zeilen ist nicht unbedingt aufeinander folgender Werte für die Zeilen abgerufen werden, da andere gleichzeitigen einfügungen für die Tabelle auftreten können. Wenn Werte fortlaufend sein müssen, wird die Transaktion verwenden Sie eine exklusive Sperre für die Tabelle oder die **SERIALIZABLE** Isolationsstufe.  
  
-   **Aufeinanderfolgende Werte nach Serverneustart oder anderen Fehlern** –[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann Identitätswerte aus Leistungsgründen Zwischenspeichern und einige der zugewiesenen Werte ist möglich während einer Datenbank Datenbankausfalls oder Serverneustarts verloren gehen. Dies kann zu Lücken im Identitätswert beim Einfügen führen. Wenn Lücken nicht zulässig sind, sollte die Anwendung ihren eigenen Mechanismus verwenden, um Schlüsselwerte zu generieren. Verwendung eines sequenzgenerators mit der **NOCACHE** Option kann einschränken, die Lücken auf Transaktionen, die nie ein Commit ausgeführt werden.  
  
-   **Wiederverwendung von Werten** – für eine bestimmte Identitätseigenschaft mit spezifischem Ausgangswert/Inkrement, die Identität, die Werte werden vom Modul nicht wiederverwendet. Wenn eine bestimmte INSERT-Anweisung fehlschlägt oder für die INSERT-Anweisung ein Rollback ausgeführt wird, gehen die verwendeten Identitätswerte verloren und werden nicht erneut generiert. Es können Lücken entstehen, wenn die nachfolgenden Identitätswerte generiert werden.  
  
 Diese Einschränkungen sind beabsichtigt, um die Leistung zu verbessern. Ferner sind sie in vielen Situationen akzeptabel. Wenn Sie Identitätswerte aufgrund dieser Einschränkungen nicht verwenden können, sollten Sie eine separate Tabelle mit einem aktuellen Wert erstellen und den Zugriff auf die Tabelle und die Nummernzuweisung für die Anwendung verwalten.  
  
 Wenn eine Tabelle mit einer Identitätsspalte für die Replikation veröffentlicht wird, muss die Identitätsspalte entsprechend dem verwendeten Replikationstyp verwaltet werden. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Es kann nur eine Identitätsspalte pro Tabelle erstellt werden.  
  
 In speicheroptimierten Tabellen müssen sowohl der Ausgangswert als auch das Inkrement auf 1,1 festgelegt werden. Festlegen der Ausgangswert oder Inkrement auf einen anderen Wert als 1 Ergebnisse in den folgenden Fehler: die Verwendung von Ausgangswerten und den inkrementellen Werte als 1 werden mit speicheroptimierten Tabellen nicht unterstützt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-identity-property-with-create-table"></a>A. Verwenden der IDENTITY-Eigenschaft mit CREATE TABLE  
 Im folgenden Beispiel wird eine neue Tabelle erstellt. Dabei wird die `IDENTITY`-Eigenschaft zum automatischen Erhöhen der Identifikationsnummer verwendet.  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>B. Verwenden generischer Syntax zum Auffinden von Lücken in Identitätswerten  
 Im folgenden Beispiel wird generische Syntax zum Auffinden von Lücken in Identitätswerten dargestellt. Diese Lücken entstehen, wenn Daten entfernt werden.  
  
> [!NOTE]  
>  Der erste Teil des folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skripts dient lediglich zur Veranschaulichung. Sie können das [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript ausführen, das mit folgendem Kommentar beginnt: `-- Create the img table`.  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_INCR &#40; Transact-SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40; Function &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40; Transact-SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET IDENTITY_INSERT &#40; Transact-SQL &#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
