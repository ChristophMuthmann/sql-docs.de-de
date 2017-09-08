---
title: '@@DBTS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f044c71018186baaf2bd5c27076b78aae139b34f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbts-transact-sql"></a>@@DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den aktuellen Wert vom Datentyp **timestamp** für die aktuelle Datenbank zurück. Dieser timestamp-Wert ist in der Datenbank definitiv nur einmal vorhanden.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
@@DBTS  
```  
  
## <a name="return-types"></a>Rückgabetypen
**varbinary**
  
## <a name="remarks"></a>Hinweise  
@@DBTS gibt den zuletzt verwendeten Timestampwert der aktuellen Datenbank zurück. Ein neuer Timestampwert wird generiert, wenn eine Zeile mit einer **timestamp** -Spalte eingefügt oder aktualisiert wird.
  
Der @@DBTS Funktion ist nicht von Änderungen in den Transaktionsisolationsstufen betroffen.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel gibt die aktuelle **Zeitstempel** aus der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>Siehe auch
[Konfigurationsfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[Cursorparallelität &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  

