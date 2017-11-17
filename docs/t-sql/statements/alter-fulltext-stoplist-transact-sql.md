---
title: ALTER FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 314e41c5b885ee5441dbc4c88db14c22fc50e7b7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fügt ein Stoppwort in die Standard-Volltextstoppliste der aktuellen Datenbank ein oder löscht ein solches Wort daraus.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>Argumente  
 *stoplist_name*  
 Der Name der Stoppliste, die geändert werden soll. *Stoplist_name* kann maximal 128 Zeichen sein.  
  
 **"** *Stoppwort* **"**  
 Eine Zeichenfolge, die ein Wort sein kann, das in der angegebenen Sprache eine Bedeutung hat, oder ein Token, das keine sprachliche Bedeutung hat. *Stoppwort* ist auf die maximale Tokenlänge (64 Zeichen) beschränkt. Ein Stoppwort kann als Unicode-Zeichenfolge angegeben werden.  
  
 Sprache *Language_term*  
 Gibt die Sprache zum Zuordnen der *Stoppwort* hinzugefügt oder gelöscht wird.  
  
 *Language_term* kann als eine Zeichenfolge, ganze Zahl oder Hexadezimalwert entsprechend dem Gebietsschemabezeichner (LCID) der Sprache, die wie folgt angegeben werden:  
  
|Format|Description|  
|------------|-----------------|  
|String|*Language_term* entspricht der **Alias** Spaltenwert in der [sys.syslanguages (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) -kompatibilitätssicht angezeigt. Die Zeichenfolge muss in einfache Anführungszeichen eingeschlossen werden, wie in **"***Language_term***"**.|  
|Integer|*Language_term* ist die LCID der Sprache.|  
|Hexadezimal|*Language_term* ist 0 X, gefolgt vom Hexadezimalwert des Gebietsschemabezeichners. Der Hexadezimalwert darf acht Ziffern nicht überschreiten, einschließlich führender Nullen. Wird der Wert im Format DBCS (Double-Byte Character Set, Doppelbyte-Zeichensatz) angegeben, wird er von SQL Server in Unicode konvertiert.|  
  
 Hinzufügen **"***Stoppwort***"** Sprache *Language_term*  
 Fügt ein Stoppwort für die Stoppliste für die angegebene Sprache Sprache *Language_term*.  
  
 Wenn die angegebene Kombination von Schlüsselwort und LCID-Wert der Sprache in der Stoppliste nicht eindeutig ist, wird ein Fehler zurückgegeben.  Wenn der LCID-Wert keiner registrierten Sprache entspricht, wird ein Fehler erzeugt.  
  
 DROP { **"***Stoppwort***"** Sprache *Language_term* | ALLE Sprachversionen *Language_term* | ALLE}  
 Löscht ein Stoppwort aus der Stoppliste.  
  
 **"** *Stoppwort* **"** Sprache *Language_term*  
 Löscht das angegebene Stoppwort für die angegebene Sprache *Language_term*.  
  
 ALLE Sprachversionen *Language_term*  
 Löscht alle Stoppwörter für die angegebene Sprache *Language_term*.  
  
 ALL  
 Löscht alle Stoppwörter aus der Stoppliste.  
  
## <a name="remarks"></a>Hinweise  
 CREATE FULLTEXT STOPLIST wird nur bei einem Kompatibilitätsgrad von mindestens 100 unterstützt. Bei Kompatibilitätsgraden von 80 und 90 wird die Systemstoppliste immer der Datenbank zugewiesen.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Festlegen einer Stoppliste als Standardstoppliste der Datenbank ist die ALTER DATABASE-Berechtigung erforderlich. Um eine Stoppliste anderer Hinsicht ändern müssen der Besitzer der Stoppliste oder Mitglieder in der **Db_owner** oder **Db_ddladmin** festen Datenbankrollen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Stoppliste `CombinedFunctionWordList` dahingehend geändert, dass zuerst für Spanisch und dann für Französisch das Wort 'en' hinzugefügt wird.  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [fulltext_stoplists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [fulltext_stopwords &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  

