---
title: CREATE FULLTEXT STOPLIST (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f20341683bd9c22e5c133d0a4a52af2687641868
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine neue Volltextstoppliste in der aktuellen Datenbank.  
  
 Stoppwörter werden über Objekte mit dem Namen *Stopplisten* in Datenbanken verwaltet. Eine Stoppliste ist eine Liste mit Stoppwörtern, die, wenn sie einem Volltextindex zugeordnet ist, auf Volltextabfragen für diesen Index angewendet wird. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
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
 Der Name der Stoppliste. *stoplist_name* darf maximal 128 Zeichen lang sein. *stoplist_name* muss innerhalb aller Stopplisten in der aktuellen Datenbank eindeutig sein und den Regeln für Bezeichner entsprechen.  
  
 *stoplist_name* wird verwendet, wenn der Volltextindex erstellt wird.  
  
 *database_name*  
 Der Name der Datenbank, in der sich die durch *source_stoplist_name* festgelegte Stoppliste befindet. Wird *database_name* nicht angegeben, wird standardmäßig die aktuelle Datenbank verwendet.  
  
 *source_stoplist_name*  
 Gibt an, dass die neue Stoppliste durch Kopieren einer vorhandenen Stoppliste erstellt wird. Wenn *source_stoplist_name* nicht vorhanden ist oder der Datenbankbenutzer nicht die entsprechende Berechtigung besitzt, wird für CREATE FULLTEXT STOPLIST ein Fehler ausgegeben. Wenn eine in den Stoppwörtern der Quellstoppliste angegebene Sprache in der aktuellen Datenbank nicht registriert ist, wird CREATE FULLTEXT STOPLIST erfolgreich ausgeführt. Allerdings werden Warnungen zurückgegeben, und die entsprechenden Stoppwörter werden nicht hinzugefügt.  
  
 SYSTEM STOPLIST  
 Gibt an, dass die neue Stoppliste aus der Stoppliste erstellt wird, die standardmäßig in der [Ressourcendatenbank](../../relational-databases/databases/resource-database.md) enthalten ist.  
  
 AUTHORIZATION *owner_name*  
 Gibt den Namen eines Datenbankprinzipals als Besitzer der Stoppliste an. *owner_name* muss der Name eines Prinzipals sein, dessen Mitglied der aktuelle Benutzer ist, oder der aktuelle Benutzer benötigt die IMPERSONATE-Berechtigung für *owner_name*. Wird kein Wert angegeben, wird der aktuelle Benutzer zum Besitzer.  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
