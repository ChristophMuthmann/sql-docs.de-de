---
title: Erstellen von FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STOPLIST_TSQL
- FULLTEXT STOPLIST
- STOPLIST
- FULLTEXT_STOPLIST_TSQL
- CREATE FULLTEXT STOPLIST
- CREATE_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- CREATE FULLTEXT STOPLIST statement
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 0669b1d0-46cc-4fac-8df7-5f7fa7af5db4
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6877dccd56d4f90a5600b095b1294ec1ccd6eb3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine neue Volltextstoppliste in der aktuellen Datenbank.  
  
 Stoppwörter werden über Objekte mit dem Namen in Datenbanken verwaltet *Stopplisten*. Eine Stoppliste ist eine Liste mit Stoppwörtern, die, wenn sie einem Volltextindex zugeordnet ist, auf Volltextabfragen für diesen Index angewendet wird. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST und DROP FULLTEXT STOPLIST werden nur bei einem Kompatibilitätsgrad von 100 unterstützt. Bei Kompatibilitätsgraden von 80 und 90 werden diese Anweisungen nicht unterstützt. Bei allen Kompatibilitätsgraden wird die Systemstopliste jedoch automatisch neuen Volltextindizes zugeordnet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumente  
 *stoplist_name*  
 Der Name der Stoppliste. *Stoplist_name* kann maximal 128 Zeichen sein. *Stoplist_name* muss innerhalb aller Stopplisten in der aktuellen Datenbank eindeutig sein und den Regeln für Bezeichner entsprechen.  
  
 *Stoplist_name* wird verwendet, wenn der Volltextindex erstellt wird.  
  
 *database_name*  
 Der Name der Datenbank, in denen die Stoppliste gemäß *Source_stoplist_name* befindet. Wenn nicht angegeben, *Database_name* Standardwerte auf die aktuelle Datenbank.  
  
 *source_stoplist_name*  
 Gibt an, dass die neue Stoppliste durch Kopieren einer vorhandenen Stoppliste erstellt wird. Wenn *Source_stoplist_name* ist nicht vorhanden, oder der Datenbankbenutzer verfügt nicht über die richtigen Berechtigungen, CREATE FULLTEXT STOPLIST schlägt fehl. Wenn eine in den Stoppwörtern der Quellstoppliste angegebene Sprache in der aktuellen Datenbank nicht registriert ist, wird CREATE FULLTEXT STOPLIST erfolgreich ausgeführt. Allerdings werden Warnungen zurückgegeben, und die entsprechenden Stoppwörter werden nicht hinzugefügt.  
  
 SYSTEM STOPLIST  
 Gibt an, dass die neue Stoppliste aus der Stoppliste erstellt wird, wird standardmäßig in der [Ressourcendatenbank](../../relational-databases/databases/resource-database.md).  
  
 Autorisierung *Owner_name*  
 Gibt den Namen eines Datenbankprinzipals als Besitzer der Stoppliste an. *Owner_name* muss der Name eines Prinzipals, der der aktuelle Benutzer angehört, oder der aktuelle Benutzer muss IMPERSONATE-Berechtigung verfügen, auf *Owner_name*. Wird kein Wert angegeben, wird der aktuelle Benutzer zum Besitzer.  
  
## <a name="remarks"></a>Hinweise  
 Der Ersteller einer Stoppliste ist deren Besitzer.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Erstellen einer STOPLIST sind CREATE FULLTEXT CATALOG-Berechtigungen erforderlich. Der Besitzer der Stoppliste kann für eine Stoppliste explizit CONTROL-Berechtigung erteilen, damit Benutzer Wörter hinzufügen und ändern und die Stoppliste löschen können.  
  
> [!NOTE]  
>  Um eine Stoppliste mit einem Volltextindex verwenden zu können, ist die REFERENCE-Berechtigung erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>A. Erstellen einer neuen Volltextstoppliste  
 Im folgenden Beispiel wird eine neue Volltextstoppliste mit dem Namen `myStoplist` erstellt.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>B. Kopieren einer Volltextstoppliste aus einer vorhandenen Volltextstoppliste  
 Im folgenden Beispiel wird eine neue Volltextstoppliste mit dem Namen `myStoplist2` erstellt, indem eine vorhandene AdventureWorks-Stoppliste mit dem Namen `Customers.otherStoplist` kopiert wird.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>C. Kopieren einer Volltextstoppliste aus der Volltextstoppliste des Systems  
 Im folgenden Beispiel wird eine neue Volltextstoppliste mit dem Namen `myStoplist3` durch Kopieren aus der Stystemstoppliste erstellt.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [fulltext_stoplists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [fulltext_stopwords &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  

