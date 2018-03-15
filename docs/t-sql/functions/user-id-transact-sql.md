---
title: USER_ID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_ID
- USER_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- USER_ID function
- identification numbers [SQL Server]
- IDs [SQL Server], databases
- users [SQL Server], database ID numbers
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
ms.assetid: 67fd29bc-eda9-4d4d-b148-5d3659181a43
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c8c8e07d6d58b6615ff5e4528556bf08e0b72c13
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="userid-transact-sql"></a>USER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die ID eines Datenbankbenutzers zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *user*  
 Der zu verwendende Benutzername. *user* ist vom Datentyp **nchar**. Falls ein **char**-Wert angegeben wird, wird dieser implizit in **nchar** konvertiert. Die Klammern sind erforderlich.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 Wenn *user* nicht angegeben ist, wird der aktuelle Benutzer verwendet. Wenn der Parameter das Wort NULL enthält, wird NULL zurückgegeben. Wird USER_ID nach der Ausführung von EXECUTE AS aufgerufen, gibt USER_ID die ID des Kontexts nach dem Identitätswechsel zurück.  
  
 Wenn ein Windows-Prinzipal, der keinem spezifischen Datenbankbenutzer zugeordnet ist, über die Mitgliedschaft in einer Gruppe auf eine Datenbank zugreift, gibt USER_ID den Wert 0 (die ID von public) zurück. Falls ein solcher Prinzipal ein Objekt ohne Angabe eines Schemas erstellt, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen impliziten Benutzer und ein Schema, das dem Windows-Prinzipal zugeordnet ist. Der in diesem Szenario erstellte Benutzer kann nicht zum Herstellen einer Verbindung mit der Datenbank verwendet werden. Bei Aufrufen von USER_ID durch einen Windows-Prinzipal, der einem impliziten Benutzer zugeordnet ist, wird die ID des impliziten Benutzers zurückgegeben.  
  
 USER_ID kann in einer Auswahlliste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die ID für den `AdventureWorks2012`-Benutzer `Harold` zurückgegeben.  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40;Transact-SQL&#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
