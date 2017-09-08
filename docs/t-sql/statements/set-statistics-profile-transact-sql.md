---
title: Legen Sie STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 69ceaedf2cfe62b20217b4e218568cec1bc2a933
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Zeigt die Profilinformationen für eine Anweisung an. STATISTICS PROFILE unterstützt Ad-hoc-Abfragen, Sichten und gespeicherte Prozeduren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn STATISTICS PROFILE auf ON festgelegt ist, gibt jede ausgeführte Abfrage neben dem regulären Resultset ein weiteres Resultset zurück, das ein Profil der Abfrageausführung zeigt.  
  
 Das zusätzliche Resultset enthält neben den SHOWPLAN_ALL-Spalten für die Abfrage die folgenden weiteren Spalten.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**Zeilen**|Tatsächliche Anzahl der Zeilen, die jeder Operator erzeugt.|  
|**Wird ausgeführt**|Häufigkeit, mit der der Operator ausgeführt wurde.|  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Verwenden von SET STATISTICS PROFILE und zum Anzeigen der Ausgabe müssen Benutzer die folgenden Berechtigungen besitzen:  
  
-   Entsprechende Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   Die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die von den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwiesen wird.  
  
 Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die keine STATISTICS PROFILE-Resultsets erstellen, sind nur die entsprechenden Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen erforderlich. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die STATISTICS PROFILE-Resultsets erstellen, müssen Überprüfungen für die Ausführungsberechtigung für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen und die SHOWPLAN-Berechtigung erfolgreich sein. Andernfalls wird die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungsausführung abgebrochen, und es werden keine Showplaninformationen generiert.  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [Festlegen der STATISTICS TIME &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  

