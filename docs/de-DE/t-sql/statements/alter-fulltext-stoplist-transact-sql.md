---
title: ALTER FULLTEXT STOPLIST (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca94694a4cadc855dea5c43906311ebeeef92d42
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 Der Name der Stoppliste, die geändert werden soll. *stoplist_name* darf maximal 128 Zeichen lang sein.  
  
 **'** *stopword* **'**  
 Eine Zeichenfolge, die ein Wort sein kann, das in der angegebenen Sprache eine Bedeutung hat, oder ein Token, das keine sprachliche Bedeutung hat. *stopword* ist auf die maximale Tokenlänge (64 Zeichen) beschränkt. Ein Stoppwort kann als Unicode-Zeichenfolge angegeben werden.  
  
 LANGUAGE *language_term*  
 Gibt die Sprache an, die *stopword* zugeordnet werden soll, das hinzugefügt oder gelöscht wird.  
  
 *language_term* kann als Zeichenfolge, Integer oder Hexadezimalwert entsprechend dem Gebietsschemabezeichner (Locale Identifier, LCID) der Sprache wie folgt angegeben werden:  
  
|Format|Description|  
|------------|-----------------|  
|Zeichenfolge|*language_term* entspricht dem **Alias**-Spaltenwert in der [sys.syslanguages (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) Kompatibilitätssicht. Die Zeichenfolge muss in einfache Anführungszeichen gesetzt werden, z.B. **'***language_term***'**.|  
|Integer|*language_term* ist der LCID der Sprache.|  
|Hexadezimal|*language_term* ist gleich 0x, gefolgt vom Hexadezimalwert des Gebietsschemabezeichners (LCID). Der Hexadezimalwert darf acht Ziffern nicht überschreiten, einschließlich führender Nullen. Wird der Wert im Format DBCS (Double-Byte Character Set, Doppelbyte-Zeichensatz) angegeben, wird er von SQL Server in Unicode konvertiert.|  
  
 ADD **'***stopword***'** LANGUAGE *language_term*  
 Fügt der Stoppliste ein Stoppwort für die durch LANGUAGE *language_term* angegebene Sprache hinzu.  
  
 Wenn die angegebene Kombination von Schlüsselwort und LCID-Wert der Sprache in der Stoppliste nicht eindeutig ist, wird ein Fehler zurückgegeben.  Wenn der LCID-Wert keiner registrierten Sprache entspricht, wird ein Fehler erzeugt.  
  
 DROP { **'***stopword***'** LANGUAGE *language_term* | ALL LANGUAGE *language_term* | ALL }  
 Löscht ein Stoppwort aus der Stoppliste.  
  
 **'** *stopword* **'** LANGUAGE *language_term*  
 Löscht das angegebene Stoppwort für die durch *language_term* angegebene Sprache.  
  
 ALL LANGUAGE *language_term*  
 Löscht alle Stoppwörter für die durch *language_term* angegebene Sprache.  
  
 ALL  
 Löscht alle Stoppwörter aus der Stoppliste.  
  
## <a name="remarks"></a>Remarks  
 CREATE FULLTEXT STOPLIST wird nur bei einem Kompatibilitätsgrad von mindestens 100 unterstützt. Bei Kompatibilitätsgraden von 80 und 90 wird die Systemstoppliste immer der Datenbank zugewiesen.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Festlegen einer Stoppliste als Standardstoppliste der Datenbank ist die ALTER DATABASE-Berechtigung erforderlich. Nur der Besitzer der Stoppliste oder Mitglieder der festen Datenbankrollen **db_owner** oder **db_ddladmin** können eine Stoppliste in anderer Hinsicht ändern.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Stoppliste `CombinedFunctionWordList` dahingehend geändert, dass zuerst für Spanisch und dann für Französisch das Wort 'en' hinzugefügt wird.  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
