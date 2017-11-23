---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs: TSQL
helpviewer_keywords: CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 695af04a3ee411392cf00be6b6483c9338a4c989
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine von der Crypto API (CAPI) generierte Kryptografie-Zufallszahl aus. Die Ausgabe ist eine hexadezimale Zahl der angegebenen Anzahl von Bytes.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>Argumente  
*length*  
Die Länge der Zahl, die erstellt wird. Das Maximum ist 8000. *length* ist vom Datentyp **int**.
  
*Startwert*  
Optionale Daten, die als zufälliger Ausgangswert verwendet werden sollen.  Es müssen mindestens *length* Bytes an Daten vorhanden sein. *seed* ist **varbinary(8000)**
  
## <a name="returned-types"></a>Rückgabetypen  
**varbinary(8000)**
  
## <a name="permissions"></a>Berechtigungen  
Diese Funktion ist öffentlich und erfordert keine besonderen Berechtigungen.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-generating-a-random-number"></a>A. Generieren einer Zufallszahl  
Im folgenden Beispiel wird eine Zufallszahl mit einer Länge von 50 Bytes generiert.
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
Im folgenden Beispiel wird eine Zufallszahl mit einer Länge von 4 Bytes mit einem Ausgangswert von 4 Bytes generiert.
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>Siehe auch
[RAND &#40; Transact-SQL &#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
