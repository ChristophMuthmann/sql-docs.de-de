---
title: Sp_recompile (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs: TSQL
helpviewer_keywords: sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e802de07e5113d9cf12ba65df56153646361f715
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sprecompile-transact-sql"></a>sp_recompile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass gespeicherte Prozeduren, Trigger und benutzerdefinierte Funktionen beim nächsten Ausführen erneut kompiliert werden. Dazu wird der vorhandene Plan aus dem Prozedurcache gelöscht, sodass beim nächsten Ausführen der Prozedur oder des Triggers das Erstellen eines neuen Plans erzwungen wird. In einer [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]-Auflistung wird das Ereignis SP:CacheInsert anstelle des Ereignisses SP:Recompile protokolliert.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @objname=] '*Objekt*"  
 Der qualifizierte oder nicht qualifizierte Name einer gespeicherten Prozedur, eines Triggers, einer Tabelle, einer Sicht oder einer benutzerdefinierten Funktion in der aktuellen Datenbank. *Objekt* ist **nvarchar(776)**, hat keinen Standardwert. Wenn *Objekt* ist der Name einer gespeicherten Prozedur, Trigger oder eine benutzerdefinierte Funktion, die gespeicherte Prozedur-Triggers oder Funktion wird beim nächsten Ausführen kompiliert werden. Wenn *Objekt* ist der Name einer Tabelle oder Sicht, alle gespeicherten Prozeduren, Trigger oder benutzerdefinierte Funktionen, die die Tabelle oder Sicht verweisen werden kompiliert, wenn Sie das nächste Mal, die sie ausgeführt werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Zahl ungleich Null (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_recompile sucht nur in der aktuellen Datenbank nach einem Objekt.  
  
 Die Abfragen, die von gespeicherten Prozeduren, Triggern oder benutzerdefinierten Funktionen durchgeführt werden, werden nur bei der Prozedur- oder Triggerkompilierung optimiert. Wenn Sie Indizes bearbeiten oder andere Änderungen an der Datenbank vornehmen, die sich auf Statistiken beziehen, kann dies die Effizienz von gespeicherten Prozeduren, Triggern und benutzerdefinierten Funktionen beeinträchtigen. Durch das erneute Kompilieren der gespeicherten Prozeduren und Trigger, die auf eine Tabelle zugreifen, können solche Abfragen wieder optimiert werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kompiliert gespeicherte Prozeduren, Trigger und benutzerdefinierten Funktionen automatisch neu, wenn dies von Vorteil ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für das angegebene Objekt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden gespeicherte Prozeduren, Trigger und benutzerdefinierten Funktionen, die auf die `Customer`-Tabelle zugreifen, beim nächsten Ausführen erneut kompiliert.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
