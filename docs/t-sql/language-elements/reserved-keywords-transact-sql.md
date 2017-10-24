---
title: "Reservierte Schlüsselwörter (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efaa21099f422ae812168561351a359fc89f8e0d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="reserved-keywords-transact-sql"></a>Reservierte Schlüsselwörter-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet reservierte Schlüsselwörter zum Definieren, Bearbeiten und Zugreifen auf Datenbanken. Reservierte Schlüsselwörter sind ein Bestandteil der Grammatik der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sprache, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, um [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen und -Batches zu analysieren und zu verstehen. Obwohl es syntaktisch möglich ist, reservierte Schlüsselwörter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als Bezeichner und Objektnamen in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skripts zu verwenden, ist hierzu die Verwendung von Begrenzungsbezeichnern erforderlich.  
  
 In der folgenden Tabelle werden die reservierten Schlüsselwörter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgeführt.  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|AND|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION|FREETEXTTABLE|-Replikation|  
|BACKUP|FROM|RESTORE|  
|BEGIN|FULL|RESTRICT|  
|BETWEEN|FUNCTION|RETURN|  
|BREAK|GOTO|REVERT|  
|BROWSE|GRANT|REVOKE|  
|BULK|GROUP|RIGHT|  
|DURCH|HAVING|ROLLBACK|  
|CASCADE|HOLDLOCK|ROWCOUNT|  
|CASE|IDENTITY|ROWGUIDCOL|  
|CHECK|IDENTITY_INSERT|RULE|  
|CHECKPOINT|IDENTITYCOL|SAVE|  
|CLOSE|IF|SCHEMA|  
|CLUSTERED|IN|SECURITYAUDIT|  
|COALESCE|INDEX|SELECT|  
|COLLATE|INNER|SEMANTICKEYPHRASETABLE|  
|COLUMN|INSERT|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|SHUTDOWN|  
|CONTINUE|KILL|SOME|  
|CONVERT|LEFT|STATISTICS|  
|CREATE|LIKE|SYSTEM_USER|  
|CROSS|LINENO|TABLE|  
|CURRENT|LOAD|TABLESAMPLE|  
|CURRENT_DATE|MERGE|TEXTSIZE|  
|CURRENT_TIME|NATIONAL|THEN|  
|CURRENT_TIMESTAMP|NOCHECK|TO|  
|CURRENT_USER|NONCLUSTERED|NACH OBEN|  
|CURSOR|NICHT|TRAN|  
|DATABASE|NULL|TRANSACTION|  
|DBCC|NULLIF|TRIGGER|  
|DEALLOCATE|OF|TRUNCATE|  
|DECLARE|OFF|TRY_CONVERT|  
|DEFAULT|OFFSETS|TSEQUAL|  
|DELETE|ON|UNION|  
|DENY|OPEN|UNIQUE|  
|DESC|OPENDATASOURCE|UNPIVOT|  
|DISK|OPENQUERY|UPDATE|  
|DISTINCT|OPENROWSET|UPDATETEXT|  
|DISTRIBUTED|OPENXML|USE|  
|DOUBLE|OPTION|Benutzer|  
|DROP|oder|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|mit|  
|EXECUTE|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||  
  
 Darüber hinaus definiert der ISO-Standard eine Liste mit reservierten Schlüsselwörtern. Sie sollten keine dieser in ISO reservierten Schlüsselwörter für Objektnamen und -bezeichner verwenden. Die Liste der reservierten ODBC-Schlüsselwörter, die in der folgenden Tabelle aufgeführt werden, stimmt mit der Liste der reservierten ISO-Schlüsselwörter überein.  
  
> [!NOTE]  
>  Die Liste der reservierten ISO-Schlüsselwörter kann in einigen Fällen stärker eingeschränkt sein als die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in anderen Fällen dagegen weniger. Die Liste reservierter ISO enthält z. B. **INT**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss dies nicht als reserviertes Schlüsselwort erkennen.  
  
 Reservierte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schlüsselwörter können als Bezeichner oder Namen von Datenbanken oder Datenbankobjekten, z. B. Tabellen, Spalten, Sichten usw., verwendet werden. Verwenden Sie entweder Bezeichner in Anführungszeichen oder Begrenzungsbezeichner. Die Verwendung von reservierten Schlüsselwörtern als Namen von Variablen und gespeicherten Prozedurparametern ist nicht eingeschränkt.  
  
## <a name="odbc-reserved-keywords"></a>Reservierte ODBC-Schlüsselwörter  
 Die folgenden Wörter sind für die Verwendung in ODBC-Funktionsaufrufen reserviert. Diese Wörter schränken nicht die minimale (minimum) SQL-Grammatik ein; damit jedoch die Kompatibilität mit Treibern sichergestellt ist, die die zentrale (core) SQL-Grammatik unterstützen, sollten Sie diese Schlüsselwörter nach Möglichkeit nicht verwenden.  
  
 Dies ist die aktuelle Liste der reservierten ODBC-Schlüsselwörter.  
  
||||  
|-|-|-|  
|**ABSOLUTE**|**EXEC**|**(ÜBERLAPPUNGEN)**|  
|**AKTION**|**EXECUTE**|**MIT LEERSTELLEN AUFFÜLLEN**|  
|**ADA**|**VORHANDEN IST**|**PARTIELLE**|  
|**HINZUFÜGEN**|**EXTERNAL**|**PASCAL-SCHREIBWEISE**|  
|**ALL**|**EXTRAHIEREN**|**POSITION**|  
|**ZUORDNEN**|**"FALSE"**|**GENAUIGKEIT**|  
|**ALTER**|**ABRUFEN VON DATEN**|**VORBEREITEN**|  
|**AND**|**ERSTE**|**BEIBEHALTEN**|  
|**ALLE**|**"FLOAT"**|**PRIMARY**|  
|**SIND**|**FÜR**|**VOR**|  
|**AS**|**FREMDSCHLÜSSEL**|**BERECHTIGUNGEN**|  
|**ASC**|**FORTRAN**|**PROZEDUR**|  
|**ASSERTION**|**GEFUNDEN**|**ÖFFENTLICHE**|  
|**AT**|**FROM**|**LESEN**|  
|**AUTORISIERUNG**|**FULL**|**ECHTE**|  
|**AVG**|**ERHALTEN**|**VERWEISE**|  
|**BEGIN**|**GLOBALE**|**RELATIVE**|  
|**BETWEEN**|**WECHSELN SIE**|**EINSCHRÄNKEN**|  
|**BIT**|**GEHE ZU**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**BEIDE**|**GRUPPE**|**ROLLBACK**|  
|**DURCH**|**HAVING**|**ZEILEN**|  
|**CASCADE**|**STUNDE**|**SCHEMA**|  
|**KASKADIERTE**|**IDENTITÄT**|**FÜHREN SIE EINEN BILDLAUF**|  
|**FALL**|**SOFORTIGE**|**SEKUNDE**|  
|**TYPUMWANDLUNG**|**IN**|**IM ABSCHNITT**|  
|**KATALOG**|**EINSCHLIESSEN**|**SELECT**|  
|**CHAR**|**INDEX**|**SITZUNG**|  
|**CHAR_LENGTH**|**INDIKATOR**|**SESSION_USER**|  
|**ZEICHEN**|**ANFÄNGLICH**|**FESTLEGEN**|  
|**CHARACTER_LENGTH**|**INNERE**|**GRÖSSE**|  
|**KONTROLLKÄSTCHEN**|**EINGABE**|**"SMALLINT"**|  
|**SCHLIESSEN SIE**|**UNTERSCHEIDUNG**|**EINIGE**|  
|**COALESCE**|**INSERT**|**SPEICHERPLATZ**|  
|**COLLATE**|**INT**|**location**|  
|**SORTIERUNG**|**GANZE ZAHL**|**SQLCA**|  
|**SPALTE**|**INTERSECT**|**SQLCODE**|  
|**COMMIT**|**INTERVALL**|**SQLERROR**|  
|**EINE VERBINDUNG HERSTELLEN**|**IN**|**SQLSTATE**|  
|**VERBINDUNG**|**IS**|**SQLWARNING**|  
|**EINSCHRÄNKUNG**|**ISOLATION**|**SUBSTRING**|  
|**EINSCHRÄNKUNGEN**|**JOIN**|**SUMME**|  
|**FORTSETZEN**|**SCHLÜSSEL**|**SYSTEM_USER**|  
|**KONVERTIEREN**|**LANGUAGE**|**TABELLE**|  
|**ENTSPRICHT**|**LETZTE**|**TEMPORÄRE**|  
|**ANZAHL**|**FÜHRENDE**|**KLICKEN SIE DANN**|  
|**ERSTELLEN**|**LEFT**|**ZEIT**|  
|**CROSS**|**EBENE**|**ZEITSTEMPEL**|  
|**AKTUELLE**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**LOKALE**|**TIMEZONE_MINUTE**|  
|**AKTUELLE_ZEIT**|**NIEDRIGERE**|**AN**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**NACHFOLGENDE**|  
|**CURRENT_USER**|**MAX**|**TRANSAKTION**|  
|**CURSOR**|**MIN.**|**ÜBERSETZEN**|  
|**DATUM**|**MINUTE**|**ÜBERSETZUNG**|  
|**TAG**|**MODUL**|**ZUSCHNEIDEN**|  
|**AUFHEBEN DER ZUORDNUNG**|**MONAT**|**"TRUE"**|  
|**DEC**|**NAMEN**|**UNION**|  
|**DEZIMALZAHL**|**NATIONAL**|**EINDEUTIGE**|  
|**DEKLARIEREN**|**NATÜRLICHE**|**UNBEKANNT**|  
|**STANDARDWERT**|**NCHAR**|**UPDATE**|  
|**VERZÖGERT**|**WEITER**|**OBERE**|  
|**VERZÖGERTE**|**NEIN**|**VERWENDUNG**|  
|**DELETE**|**NONE**|**BENUTZER**|  
|**"DESC"**|**NOT**|**MITHILFE VON**|  
|**BESCHREIBEN**|**NULL**|**VALUE**|  
|**DER DESKRIPTOR**|**NULLIF**|**WERTE**|  
|**DIAGNOSE**|**NUMERISCH**|**VARCHAR**|  
|**TRENNEN**|**OCTET_LENGTH**|**VARYING**|  
|**DISTINCT**|**DER**|**ANZEIGEN**|  
|**DOMÄNE**|**ON**|**WENN**|  
|**DOUBLE**|**NUR**|**BEI JEDEM**|  
|**LÖSCHEN**|**ÖFFNEN**|**WHERE**|  
|**ELSE**|**OPTION**|**MIT**|  
|**END**|**OR**|**ARBEITSAUFGABEN**|  
|**END-EXEC**|**REIHENFOLGE**|**SCHREIBEN**|  
|**ESCAPEZEICHEN**|**ÄUSSERE**|**JAHR**|  
|**AUSNAHME:**|**AUSGABE**|**ZONE**|  
|**AUSNAHME**|||  
  
## <a name="future-keywords"></a>Zukünftige Schlüsselwörter  
 Die folgenden Schlüsselwörter werden möglicherweise in zukünftigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen reserviert, wenn neue Funktionen implementiert werden. Es empfiehlt sich, diese Wörter nicht als Bezeichner zu verwenden.  
  
||||  
|-|-|-|  
|ABSOLUTE|HOST|RELATIVE|  
|ACTION|HOUR|RELEASE|  
|ADMIN|IGNORE|RESULT|  
|AFTER|IMMEDIATE|RETURNS|  
|AGGREGATE|INDICATOR|ROLE|  
|ALIAS|INITIALIZE|ROLLUP|  
|ALLOCATE|INITIALLY|ROUTINE|  
|ARE|INOUT|ROW|  
|ARRAY|INPUT|ROWS|  
|ASENSITIVE|INT|SAVEPOINT|  
|ASSERTION|INTEGER|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|AT|INTERVAL|SEARCH|  
|ATOMIC|ISOLATION|SECOND|  
|BEFORE|ITERATE|SECTION|  
|BINARY|LANGUAGE|SENSITIVE|  
|BIT|LARGE|SEQUENCE|  
|BLOB|LAST|SESSION|  
|BOOLEAN|LATERAL|SETS|  
|BOTH|LEADING|SIMILAR|  
|BREADTH|LESS|SIZE|  
|CALL|LEVEL|SMALLINT|  
|CALLED|LIKE_REGEX|SPACE|  
|CARDINALITY|LIMIT|SPECIFIC|  
|CASCADED|LN|SPECIFICTYPE|  
|CAST|LOCAL|SQL|  
|CATALOG|LOCALTIME|SQLEXCEPTION|  
|CHAR|LOCALTIMESTAMP|SQLSTATE|  
|CHARACTER|LOCATOR|SQLWARNING|  
|CLASS|MAP|START|  
|CLOB|MATCH|STATE|  
|COLLATION|MEMBER|STATEMENT|  
|COLLECT|METHOD|STATIC|  
|COMPLETION|MINUTE|STDDEV_POP|  
|CONDITION|MOD|STDDEV_SAMP|  
|CONNECT|MODIFIES|STRUCTURE|  
|CONNECTION|MODIFY|SUBMULTISET|  
|CONSTRAINTS|MODULE|SUBSTRING_REGEX|  
|CONSTRUCTOR|MONTH|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|NEW|timestamp|  
|CURRENT_CATALOG|NEXT|TIMEZONE_HOUR|  
|CURRENT_DEFAULT_TRANSFORM_GROUP|Nein|TIMEZONE_MINUTE|  
|CURRENT_PATH|Keine|TRAILING|  
|CURRENT_ROLE|NORMALIZE|TRANSLATE_REGEX|  
|CURRENT_SCHEMA|NUMERIC|TRANSLATION|  
|CURRENT_TRANSFORM_GROUP_FOR_TYPE|OBJECT|TREAT|  
|CYCLE|OCCURRENCES_REGEX|TRUE|  
|DATA|OLD|UESCAPE|  
|DATE|ONLY|UNDER|  
|DAY|OPERATION|UNKNOWN|  
|DEC|ORDINALITY|UNNEST|  
|DECIMAL|OUT|USAGE|  
|DEFERRABLE|OVERLAY|USING|  
|DEFERRED|OUTPUT|Value|  
|DEPTH|PAD|VAR_POP|  
|DEREF|Parameter|VAR_SAMP|  
|DESCRIBE|PARAMETERS|VARCHAR|  
|DESCRIPTOR|PARTIAL|VARIABLE|  
|DESTROY|PARTITION|WHENEVER|  
|DESTRUCTOR|PATH|WIDTH_BUCKET|  
|DETERMINISTIC|POSTFIX|WITHOUT|  
|DICTIONARY|PREFIX|WINDOW|  
|DIAGNOSTICS|PREORDER|WITHIN|  
|DISCONNECT|PREPARE|WORK|  
|DOMAIN|PERCENT_RANK|WRITE|  
|DYNAMIC|PERCENTILE_CONT|XMLAGG|  
|EACH|PERCENTILE_DISC|XMLATTRIBUTES|  
|ELEMENT|POSITION_REGEX|XMLBINARY|  
|END-EXEC|PRESERVE|XMLCAST|  
|EQUALS|PRIOR|XMLCOMMENT|  
|EVERY|PRIVILEGES|XMLCONCAT|  
|EXCEPTION|RANGE|XMLDOCUMENT|  
|FALSE|READS|XMLELEMENT|  
|FILTER|real|XMLEXISTS|  
|FIRST|RECURSIVE|XMLFOREST|  
|GLEITKOMMAZAHL|REF|XMLITERATE|  
|FOUND|REFERENCING|XMLNAMESPACES|  
|KOSTENLOS|REGR_AVGX|XMLPARSE|  
|FULLTEXTTABLE|REGR_AVGY|XMLPI|  
|FUSION|REGR_COUNT|XMLQUERY|  
|GENERAL|REGR_INTERCEPT|XMLSERIALIZE|  
|GET|REGR_R2|XMLTABLE|  
|GLOBAL|REGR_SLOPE|XMLTEXT|  
|GO|REGR_SXX|XMLVALIDATE|  
|GROUPING|REGR_SXY|YEAR|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>Siehe auch  
 [SET QUOTED_IDENTIFIER &#40; Transact-SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

