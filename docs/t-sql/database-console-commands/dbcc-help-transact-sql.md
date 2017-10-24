---
title: DBCC HELP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fd6f0e7ef5c74c3a3f8fc2af9424a2996dfcd98
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Gibt Syntaxinformationen für den angegebenen DBCC-Befehl zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
 *dbcc_statement* | *@dbcc_statement_var*  
 Der Name des DBCC-Befehls, für den Syntaxinformationen angefordert werden. Geben Sie nur den Teil des DBCC-Befehls an, der auf DBCC folgt, z. B. CHECKDB anstelle von DBCC CHECKDB.  
  
 ?  
 Gibt alle DBCC-Befehle zurück, für die Hilfe verfügbar ist.  
  
 WITH NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="result-sets"></a>Resultsets  
DBCC HELP gibt ein Resultset zurück, das die Syntax für den angegebenen DBCC-Befehl anzeigt.
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .
  
## <a name="examples"></a>Beispiele  
### <a name="a-using-dbcc-help-with-a-variable"></a>A. Verwenden von DBCC HELP mit einer Variablen  
Mit dem folgenden Beispiel werden die Syntaxinformationen für DBCC `CHECKDB` zurückgegeben.
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>B. Verwenden von DBCC HELP mit ? Option  
Mit dem folgenden Beispiel werden alle DBCC-Anweisungen zurückgegeben, für die Hilfe zur Verfügung steht.
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

