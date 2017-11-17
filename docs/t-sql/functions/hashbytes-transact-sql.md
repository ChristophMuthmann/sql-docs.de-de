---
title: HASHBYTES (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4826936736685a46e8df8604339a7d4a878981ee
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

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
 **"**\<Algorithmus >**"**  
 Identifiziert den für das Hashing der Eingabe zu verwendenden Hashalgorithmus. Dies ist ein erforderliches Argument ohne Standardwert. Die einfachen Anführungszeichen müssen eingegeben werden. Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], alle anderen Algorithmen als SHA2_256 oder SHA2_512 sind veraltet. Ältere Algorithmen (nicht empfohlen) werden weiterhin ausgeführt, aber sie werden eine veraltungsereignis ausgelöst.  
  
 **@input**  
 Gibt eine Variable mit den Daten an, für die das Hashing ausgeführt werden soll. **@input**ist **Varchar**, **Nvarchar**, oder **Varbinary**.  
  
 **"** *input* **"**  
 Gibt einen Ausdruck an, der zu einer Zeichenfolge oder Binärzeichenfolge ausgewertet wird, für die das Hashing ausgeführt werden soll.  
  
 Die Ausgabe entspricht dem Algorithmusstandard: 128 Bits (16 Bytes) für MD2, MD4 und MD5; 160 Bits (20 Bytes) für SHA und SHA1; 256 Bits (32 Bytes) für SHA2_256 und 512 Bits (64 Bytes) für SHA2_512.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Für [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und früher: zulässige Eingabewerte sind auf 8.000 Bytes beschränkt.  
  
## <a name="return-value"></a>Rückgabewert  
 **Varbinary** (maximal 8.000 Byte)  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-return-the-hash-of-a-variable"></a>A: Zurückgeben des Hashcodes einer Variablen  
 Das folgende Beispiel gibt die `SHA1` -Hash der **Nvarchar** in Variablen gespeicherten Daten `@HashThis`.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  

