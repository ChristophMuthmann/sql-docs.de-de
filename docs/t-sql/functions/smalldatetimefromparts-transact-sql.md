---
title: SMALLDATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90be7b0ad4f7fcc7677f820e374705636891d458
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt eine **Smalldatetime** Wert für das angegebene Datum und die Uhrzeit.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
## <a name="arguments"></a>Argumente  
 *Jahr*  
 Ganzzahliger Ausdruck, der ein Jahr angibt.  
  
 *Monat*  
 Ganzzahliger Ausdruck, der einen Monat angibt.  
  
 *Tag*  
 Ganzzahliger Ausdruck, der einen Tag angibt.  
  
 *Stunde*  
 Ganzzahliger Ausdruck, der die Stunden angibt.  
  
 *Minute*  
 Ganzzahliger Ausdruck, der die Minuten angibt.  
  
## <a name="return-types"></a>Rückgabetypen  
 **smalldatetime**  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktionen verhält sich wie einen Konstruktor für einen vollständig initialisierten **Smalldatetime** Wert. Wenn die Argumente nicht gültig sind, wird ein Fehler ausgegeben. Wenn erforderliche Argumente den Wert NULL haben, wird NULL zurückgegeben.  
  
 Diese Funktion kann remote auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Servern oder höher ausgeführt werden. Sie werden nicht in der Remoteausführung auf Servern, auf denen eine Version unter [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="examples"></a>Beispiele  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  
  


