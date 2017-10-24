---
title: USER_ID (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a40853c10e17969c78ef88e4b75995e77b8a1bac
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="userid-transact-sql"></a>USER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die ID eines Datenbankbenutzers zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Benutzer*  
 Der zu verwendende Benutzername. *Benutzer* ist **Nchar**. Wenn eine **Char** -Wert angegeben wird, wird es implizit in konvertiert **Nchar**. Die Klammern sind erforderlich.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Wenn *Benutzer* wird weggelassen wird, wird der aktuelle Benutzer verwendet. Wenn der Parameter das Wort NULL enthält, wird NULL zurückgegeben. Wird USER_ID nach der Ausführung von EXECUTE AS aufgerufen, gibt USER_ID die ID des Kontexts nach dem Identitätswechsel zurück.  
  
 Wenn ein Windows-Prinzipal, der keinem spezifischen Datenbankbenutzer zugeordnet ist, über die Mitgliedschaft in einer Gruppe auf eine Datenbank zugreift, gibt USER_ID den Wert 0 (die ID von public) zurück. Falls ein solcher Prinzipal ein Objekt ohne Angabe eines Schemas erstellt, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen impliziten Benutzer und ein Schema, das dem Windows-Prinzipal zugeordnet ist. Der in diesem Szenario erstellte Benutzer kann nicht zum Herstellen einer Verbindung mit der Datenbank verwendet werden. Bei Aufrufen von USER_ID durch einen Windows-Prinzipal, der einem impliziten Benutzer zugeordnet ist, wird die ID des impliziten Benutzers zurückgegeben.  
  
 USER_ID kann in einer Auswahlliste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die ID für den `AdventureWorks2012`-Benutzer `Harold` zurückgegeben.  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [USER_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40; Transact-SQL &#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

