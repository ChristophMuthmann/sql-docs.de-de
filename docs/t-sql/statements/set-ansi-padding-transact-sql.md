---
title: SET ANSI_PADDING (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 532df95a03b15d545c682d30b3b4d68e10ea5913
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Steuert das Speichern von Werten in der Spalte, wenn die Werte kürzer als die definierte Spaltengröße sind, und das Speichern von Werten mit nachfolgenden Leerzeichen in **char**-, **varchar**-, **binary**- und **varbinary** -Daten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax
  
```
-- Syntax for SQL Server

SET ANSI_PADDING { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_PADDING ON
```

## <a name="remarks"></a>Remarks  
 Spalten, die mit den Datentypen **char**, **varchar**, **binary** und **varbinary** definiert sind, verfügen über eine definierte Größe.  
  
 Diese Einstellung betrifft ausschließlich die Definition neuer Spalten. Nachdem die Spalte erstellt wurde, speichert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Werte gemäß der Einstellung, die beim Erstellen der Spalte festgelegt war. Bestehende Spalten sind von späteren Änderungen dieser Einstellung nicht betroffen.  
  
> [!NOTE]  
>  Es wird empfohlen, für ANSI_PADDING stets den Wert ON festzulegen.  
  
 Die folgende Tabelle zeigt die Auswirkungen der SET ANSI_PADDING-Einstellung, wenn Werte in Spalten vom Datentyp **char**, **varchar**, **binary** und **varbinary** eingefügt werden.  
  
|Einstellung|char(*n*) NOT NULL oder binary(*n*) NOT NULL|char(*n*) NULL oder binary(*n*) NULL|varchar(*n*) oder varbinary(*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|Füllt den ursprünglichen Wert (mit nachfolgenden Leerräumen für **char**-Spalten und nachfolgenden Nullen für **binary**-Spalten) bis zur Spaltenlänge auf.|Folgt den gleichen Regeln wie für **char(***n***)** oder **binary(***n***)** NOT NULL, wenn SET ANSI_PADDING auf ON festgelegt ist.|Nachfolgende Leerräume in Zeichenwerten, die in **varchar**-Spalten eingefügt werden, werden nicht abgeschnitten. Nachfolgende Nullen in Binärwerten, die in **varbinary**-Spalten eingefügt werden, werden nicht abgeschnitten. Werte werden nicht bis zur Spaltenlänge aufgefüllt.|  
|OFF|Füllt den ursprünglichen Wert (mit nachfolgenden Leerräumen für **char**-Spalten und nachfolgenden Nullen für **binary**-Spalten) bis zur Spaltenlänge auf.|Folgt den gleichen Regeln wie für **varchar** oder **varbinary**, wenn SET ANSI_PADDING auf OFF festgelegt ist.|Nachfolgende Leerräume in Zeichenwerten, die in eine **varchar**-Spalte eingefügt werden, werden abgeschnitten. Nachfolgende Nullen in Binärwerten, die in eine **varbinary**-Spalte eingefügt werden, werden abgeschnitten.|  
  
> [!NOTE]  
>  Beim Auffüllen werden **char**-Spalten mit Leerräumen und **binary**-Spalten mit Nullen aufgefüllt. Wenn ein Abschneiden stattfindet, werden bei **char**-Spalten die abschließenden Leerräume abgeschnitten und bei **binary**-Spalten die abschließenden Nullen.  
  
 Für SET ANSI_PADDING muss beim Erstellen oder Ändern von Indizes für berechnete Spalten oder indizierte Sichten die Einstellung ON festgelegt werden. Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie in den Überlegungen zum Verwenden der SET-Anweisungen unter [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 Die Standardeinstellung für SET ANSI_PADDING ist ON. Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client und der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] legen für ANSI_PADDING beim Herstellen einer Verbindung automatisch ON fest. Diese Einstellung kann in ODBC-Datenquellen, in ODBC-Verbindungsattributen oder in OLE DB-Verbindungseigenschaften konfiguriert werden, die in der Anwendung festgelegt werden, bevor die Verbindung hergestellt wird. Die Standardeinstellung für SET ANSI_PADDING für Verbindungen von DB-Library-Anwendungen ist OFF.  
  
 Die Einstellung SET ANSI_PADDING hat keine Auswirkungen auf die Datentypen **nchar**, **nvarchar**, **ntext**, **text**, **image**, **varbinary(max)**, **varchar(max)** und **nvarchar(max)**. Diese zeigen immer das Verhalten von SET ANSI_PADDING ON. Das heißt, dass nachfolgende Leerzeichen und Nullen nicht abgeschnitten werden.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
