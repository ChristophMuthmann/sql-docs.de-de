---
title: SET ANSI_PADDING (Transact-SQL) | Microsoft Docs
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
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 426cbfe673bafe6e1770745ca16ba23fd068fb67
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Steuert das Speichern von Werten in der Spalte, wenn die Werte kürzer als die definierte Spaltengröße sind, und das Speichern von Werten mit nachfolgenden Leerzeichen in **char**-, **varchar**-, **binary**- und **varbinary** -Daten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_PADDING { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_PADDING ON;  
```  
  
## <a name="remarks"></a>Hinweise  
 Spalten, die mit **Char**, **Varchar**, **binäre**, und **Varbinary** Datentypen haben eine definierte Größe.  
  
 Diese Einstellung betrifft ausschließlich die Definition neuer Spalten. Nachdem die Spalte erstellt wurde, speichert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Werte gemäß der Einstellung, die beim Erstellen der Spalte festgelegt war. Bestehende Spalten sind von späteren Änderungen dieser Einstellung nicht betroffen.  
  
> [!NOTE]  
>  Es wird empfohlen, für ANSI_PADDING stets den Wert ON festzulegen.  
  
 Die folgende Tabelle zeigt die Auswirkungen der SET ANSI_PADDING-Einstellung beim Einfügen von Werten in Spalten mit **Char**, **Varchar**, **binäre**, und  **Varbinary** Datentypen.  
  
|Einstellung|Char (*n*) nicht NULL oder binary (*n*) NOT NULL|Char (*n*) NULL oder binary (*n*) NULL|Varchar (*n*) oder Varbinary (*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|Füllt den ursprünglichen Wert (mit nachfolgenden Leerzeichen für **Char** Spalten und nachfolgenden Nullen für **binäre** Spalten) auf die Länge der Spalte.|Folgt den gleichen Regeln wie für **Char (***n***)** oder **binäre (**  *n*  **)** NOT NULL, wenn SET ANSI_PADDING auf ON festgelegt ist.|Nachfolgende Leerzeichen in Zeichenwerten, die eingefügt **Varchar** Spalten werden nicht abgeschnitten. Nachfolgende Nullen in Binärwerten, die eingefügt **Varbinary** Spalten werden nicht abgeschnitten. Werte werden nicht bis zur Spaltenlänge aufgefüllt.|  
|OFF|Füllt den ursprünglichen Wert (mit nachfolgenden Leerzeichen für **Char** Spalten und nachfolgenden Nullen für **binäre** Spalten) auf die Länge der Spalte.|Folgt den gleichen Regeln wie für **Varchar** oder **Varbinary** Wenn SET ANSI_PADDING OFF festgelegt ist.|Nachfolgende Leerzeichen in Zeichenwerten, die eingefügt eine **Varchar** Spalte werden abgeschnitten. Nachfolgende Nullen in Binärwerten, die eingefügt eine **Varbinary** Spalte werden abgeschnitten.|  
  
> [!NOTE]  
>  Beim Auffüllen werden **Char** Spalten werden mit Leerzeichen aufgefüllt und **binäre** Spalten werden mit Nullen aufgefüllt. Wenn ein Abschneiden stattfindet, **Char** Spalten haben die abschließenden Leerzeichen abgeschnitten, und **binäre** Spalten haben die abschließenden Nullen.  
  
 Für SET ANSI_PADDING muss beim Erstellen oder Ändern von Indizes für berechnete Spalten oder indizierte Sichten die Einstellung ON festgelegt werden. Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie unter "Überlegungen beim Sie mithilfe der SET-Anweisungen in [SET-Anweisungen &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 Die Standardeinstellung für SET ANSI_PADDING ist ON. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_PADDING automatisch auf ON festgelegt wird, wenn eine Verbindung herstellen. Diese Einstellung kann in ODBC-Datenquellen, in ODBC-Verbindungsattributen oder in OLE DB-Verbindungseigenschaften konfiguriert werden, die in der Anwendung festgelegt werden, bevor die Verbindung hergestellt wird. Die Standardeinstellung für SET ANSI_PADDING für Verbindungen von DB-Library-Anwendungen ist OFF.  
  
 SET ANSI_PADDING-Einstellung wirkt sich nicht die **Nchar**, **Nvarchar**, **Ntext**, **Text**, **Image**, **varbinary(max)**, **varchar(max)**, und **nvarchar(max)** Datentypen. Diese zeigen immer das Verhalten von SET ANSI_PADDING ON. Das heißt, dass nachfolgende Leerzeichen und Nullen nicht abgeschnitten werden.  
  
 Ist SET ANSI_DEFAULTS auf ON festgelegt, so ist SET ANSI_PADDING aktiviert.  
  
 Die Einstellung von SET ANSI_PADDING wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie sich die Einstellung auf die einzelnen Datentypen auswirkt.  
  
```  
PRINT 'Testing with ANSI_PADDING ON'  
SET ANSI_PADDING ON;  
GO  
  
CREATE TABLE t1 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',  
   varbinarycol  
FROM t1;  
GO  
  
PRINT 'Testing with ANSI_PADDING OFF';  
SET ANSI_PADDING OFF;  
GO  
  
CREATE TABLE t2 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',  
   varbinarycol  
FROM t2;  
GO  
  
DROP TABLE t1;  
DROP TABLE t2;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
