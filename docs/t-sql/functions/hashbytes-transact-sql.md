---
title: HASHBYTES (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs:
- TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 63552f4b6fb61b3b24d4d670b9ea255d8e417699
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den MD2-, MD4-, MD5-, SHA-, SHA1- oder SHA2-Hash der zugehörigen Eingabe in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>Argumente  
 **'**\<algorithm>**'**  
 Identifiziert den für das Hashing der Eingabe zu verwendenden Hashalgorithmus. Dies ist ein erforderliches Argument ohne Standardwert. Die einfachen Anführungszeichen müssen eingegeben werden. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] gelten alle anderen Algorithmen als SHA2_256 und SHA2_512 als veraltet. Ältere Algorithmen (nicht empfohlen) funktionieren weiterhin, lösen jedoch ein Veraltungsereignis aus.  
  
 **@input**  
 Gibt eine Variable mit den Daten an, für die das Hashing ausgeführt werden soll. **@input** ist **varchar**, **nvarchar** oder **varbinary**.  
  
 **'** *input* **'**  
 Gibt einen Ausdruck an, der zu einer Zeichenfolge oder Binärzeichenfolge ausgewertet wird, für die das Hashing ausgeführt werden soll.  
  
 Die Ausgabe entspricht dem Algorithmusstandard: 128 Bits (16 Bytes) für MD2, MD4 und MD5; 160 Bits (20 Bytes) für SHA und SHA1; 256 Bits (32 Bytes) für SHA2_256 und 512 Bits (64 Bytes) für SHA2_512.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Bei [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und früher sind zulässige Eingabewerte auf 8.000 Byte beschränkt.  
  
## <a name="return-value"></a>Rückgabewert  
 **varbinary** (maximal 8.000 Byte)  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-return-the-hash-of-a-variable"></a>A: Zurückgeben des Hashcodes einer Variablen  
 Im folgenden Beispiel wird der `SHA1`-Hash der in der `@HashThis`-Variablen gespeicherten **nvarchar**-Daten zurückgegeben.  
  
```  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
  
```  
  
### <a name="b-return-the-hash-of-a-table-column"></a>B: Zurückgeben des Hashcodes einer Tabellenspalte  
 Im folgenden Beispiel wird der SHA1-Hash der Werte in der Spalte `c1` der Tabelle `Test1` zurückgegeben.  
  
```  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
