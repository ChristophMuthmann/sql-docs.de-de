---
title: COLUMNPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: c6c2af8d231f03c40ee87d3468977c3b66cbeeb4
ms.contentlocale: de-de
ms.lasthandoff: 10/05/2017

---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt Informationen über eine Spalte oder einen Parameter zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>Argumente  
*id*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , die den Bezeichner (ID) der Tabelle oder Prozedur enthält.
  
*Spalte*  
Ein Ausdruck, der den Namen der Spalte oder des Parameters enthält.
  
*Eigenschaft*  
Ist ein Ausdruck, der für die zurückgegebenen Informationen enthält *Id*, und kann einen der folgenden Werte sein.
  
|Wert|Description|Rückgabewert|  
|---|---|---|
|**AllowsNull**|Null-Werte zulässt.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**ColumnId**|Spalten-ID-Wert entspricht **column_id**.|Column ID<br /><br /> **Hinweis:** mehrere Spalten abgefragt werden, können Lücken in der Reihenfolge der Spalten-ID-Werte angezeigt.|  
|**FullTextTypeColumn**|Der TYPE-Spalte in der Tabelle, die die Dokumenttypinformationen enthält die *Spalte*.|Die ID der Volltexttypspalte TYPE COLUMN für die Spalte, die als zweiter Parameter dieser Eigenschaft übergeben wurde.|  
|**Ist berechnet**|Die Spalte ist eine berechnete Spalte.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsCursorType**|Der Prozedurparameter ist vom Typ CURSOR.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsDeterministic**|Die Spalte ist deterministisch. Diese Eigenschaft gilt nur für berechnete Spalten und Sichtspalten.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig. Keine berechnete Spalte oder Sichtspalte.|  
|**IsFulltextIndexed**|Die Spalte wurde für die Volltextindizierung registriert.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsIdentity**|Die Spalte verwendet die IDENTITY-Eigenschaft.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsIdNotForRepl**|In der Spalte wird die IDENTITY_INSERT-Einstellung überprüft.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsIndexable**|Diese Spalte kann indiziert werden.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsOutParam**|Der Prozedurparameter ist ein Ausgabeparameter.|1 = "TRUE"<br /><br /> 0 = False NULL = Eingabe ist nicht gültig|  
|**IsPrecise**|Diese Spalte ist eine genaue Spalte. Diese Eigenschaft wird nur auf deterministische Spalten angewendet.|1 = "TRUE"<br /><br /> 0 = False NULL = Eingabe ist nicht gültig Keine deterministische Spalte|  
|**IsRowGuidCol**|Spalte hat die **"uniqueidentifier"** -Datentyp und mit der ROWGUIDCOL-Eigenschaft definiert ist.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsSystemVerified**|Die Determinismus- und Genauigkeitseigenschaften der Spalte können von [!INCLUDE[ssDE](../../includes/ssde-md.md)] überprüft werden. Diese Eigenschaft gilt nur für berechnete Spalten und Spalten von Sichten.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsXmlIndexable**|Die XML-Spalte kann in einem XML-Index verwendet werden.|1 = "TRUE"<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**Genauigkeit**|Die Länge des Datentyps der Spalte oder des Parameters.|Die Länge des angegebenen Spaltendatentyps.<br /><br /> -1 = **Xml** oder große Werttypen<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**Dezimalstellen**|Dezimalstellen des Datentyps der Spalte oder des Parameters.|Die Dezimalstellen<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**StatisticalSemantics**|Spalte ist für die semantische Indizierung aktiviert.|1 = "TRUE"<br /><br /> 0 = FALSE|  
|**SystemDataAccess**|Die Spalte wird von einer Funktion abgeleitet, die auf Daten in den Systemkatalogen oder virtuellen Tabellen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreift. Diese Eigenschaft gilt nur für berechnete Spalten und Spalten von Sichten.|1 = True (gibt schreibgeschützten Zugriff an)<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**UserDataAccess**|Die Spalte wird von einer Funktion abgeleitet, die auf Daten in Benutzertabellen zugreift, einschließlich Sichten und temporäre Tabellen, die in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind. Diese Eigenschaft gilt nur für berechnete Spalten und Spalten von Sichten.|1 = True (gibt schreibgeschützten Zugriff an)<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**UsesAnsiTrim**|Bei der Erstellung der Tabelle wurde für ANSI_PADDING die Einstellung ON festgelegt. Diese Eigenschaft gilt nur für Spalten oder Parameter vom Typ **Char** oder **Varchar**.|1 = "TRUE"<br /><br /> 0 = "FALSE"<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsSparse**|Spalte ist eine Sparsespalte. Weitere Informationen finden Sie unter [Verwenden von Spalten mit geringer Dichte](../../relational-databases/tables/use-sparse-columns.md).|1 = "TRUE"<br /><br /> 0 = "FALSE"<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsColumnSet**|Spalte ist ein Spaltensatz. Weitere Informationen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).|1 = "TRUE"<br /><br /> 0 = "FALSE"<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**"Generatedalwaystype"**|Spaltenwert wird vom System generiert werden. Entspricht **sys.columns.generated_always_type**|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = nicht immer generierten<br /><br /> 1 = Generated always as Zeile starten<br /><br /> 2 – generated always als Zeilenende|  
|**"IsHidden"**|Spaltenwert wird vom System generiert werden. Entspricht **sys.columns.is_hidden**|**Gilt für**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = nicht ausgeblendete<br /><br /> 1 = ausgeblendet|  
  
## <a name="return-types"></a>Rückgabetypen
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.
  
Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. COLUMNPROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Hinweise  
Beim Prüfen einer deterministischen Eigenschaft einer Spalte prüfen Sie zuerst, ob die Spalte eine berechnete Spalte ist. **IsDeterministic** gibt für nicht berechnete Spalten NULL zurück. Berechnete Spalten können als Indexspalten angegeben werden.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel gibt die Länge der Spalte `LastName` zurück.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>Siehe auch
[Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  

