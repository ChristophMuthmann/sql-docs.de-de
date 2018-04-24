---
title: COLUMNPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5c26df937a654289c6a5313631a612bfbd386cc6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt Informationen über eine Spalte oder einen Parameter zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>Argumente  
*id*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md), der den Bezeichner (ID) der Tabelle oder Prozedur enthält.
  
*column*  
Ein Ausdruck, der den Namen der Spalte oder des Parameters enthält.
  
*property*  
Ein Ausdruck, der die Informationen enthält, die für *id* zurückgegeben werden. Die folgenden Werte sind möglich:
  
|value|Description|Zurückgegebener Wert|  
|---|---|---|
|**AllowsNull**|Lässt NULL-Werte zu.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**ColumnId**|Der Wert der Spalten-ID, der **sys.columns.column_id** entspricht.|Column ID<br /><br /> **Hinweis:** Wenn mehrere Spalten abgefragt werden, können Lücken in der Abfolge von Werten für Spalten-IDs auftreten.|  
|**FullTextTypeColumn**|Der TYPE COLUMN-Wert in der Tabelle, der die Dokumenttypinformationen der *Spalte* enthält.|Die ID der Volltexttypspalte TYPE COLUMN für die Spalte, die als zweiter Parameter dieser Eigenschaft übergeben wurde.|  
|**IsComputed**|Die Spalte ist eine berechnete Spalte.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsCursorType**|Der Prozedurparameter ist vom Typ CURSOR.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsDeterministic**|Die Spalte ist deterministisch. Diese Eigenschaft gilt nur für berechnete Spalten und Sichtspalten.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig. Keine berechnete Spalte oder Sichtspalte.|  
|**IsFulltextIndexed**|Die Spalte wurde für die Volltextindizierung registriert.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsIdentity**|Die Spalte verwendet die IDENTITY-Eigenschaft.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsIdNotForRepl**|In der Spalte wird die IDENTITY_INSERT-Einstellung überprüft.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsIndexable**|Diese Spalte kann indiziert werden.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**isoutparam**|Der Prozedurparameter ist ein Ausgabeparameter.|1 = TRUE<br /><br /> 0 = False NULL = Eingabe ist nicht gültig|  
|**IsPrecise**|Diese Spalte ist eine genaue Spalte. Diese Eigenschaft wird nur auf deterministische Spalten angewendet.|1 = TRUE<br /><br /> 0 = False NULL = Eingabe ist nicht gültig Keine deterministische Spalte|  
|**IsRowGuidCol**|Die Spalte hat den Datentyp **uniqueidentifier** und wird über die ROWGUIDCOL-Eigenschaft definiert.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsSystemVerified**|Die Determinismus- und Genauigkeitseigenschaften der Spalte können von [!INCLUDE[ssDE](../../includes/ssde-md.md)] überprüft werden. Diese Eigenschaft gilt nur für berechnete Spalten und Spalten von Sichten.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsXmlIndexable**|Die XML-Spalte kann in einem XML-Index verwendet werden.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**Genauigkeit**|Die Länge des Datentyps der Spalte oder des Parameters.|Die Länge des angegebenen Spaltendatentyps.<br /><br /> –1 = **xml** oder ein Typ für hohe Werte.<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**Dezimalstellen**|Dezimalstellen des Datentyps der Spalte oder des Parameters.|Die Dezimalstellen<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**StatisticalSemantics**|Spalte ist für die semantische Indizierung aktiviert.|1 = TRUE<br /><br /> 0 = FALSE|  
|**SystemDataAccess**|Die Spalte wird von einer Funktion abgeleitet, die auf Daten in den Systemkatalogen oder virtuellen Tabellen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreift. Diese Eigenschaft gilt nur für berechnete Spalten und Spalten von Sichten.|1 = True (gibt schreibgeschützten Zugriff an)<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**UserDataAccess**|Die Spalte wird von einer Funktion abgeleitet, die auf Daten in Benutzertabellen zugreift, einschließlich Sichten und temporäre Tabellen, die in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind. Diese Eigenschaft gilt nur für berechnete Spalten und Spalten von Sichten.|1 = True (gibt schreibgeschützten Zugriff an)<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**UsesAnsiTrim**|Bei der Erstellung der Tabelle wurde für ANSI_PADDING die Einstellung ON festgelegt. Diese Eigenschaft gilt nur für Spalten oder Parameter vom Typ **char** oder **varchar**.|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsSparse**|Spalte ist eine Sparsespalte. Weitere Informationen finden Sie unter [Verwenden von Spalten mit geringer Dichte](../../relational-databases/tables/use-sparse-columns.md).|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsColumnSet**|Spalte ist ein Spaltensatz. Weitere Informationen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**GeneratedAlwaysType**|Entspricht dem vom System generierten Spaltenwert. Entspricht **sys.columns.generated_always_type**|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Nicht immer generiert<br /><br /> 1 = Immer als Zeilenanfang generiert<br /><br /> 2 = Immer als Zeilenende generiert|  
|**IsHidden**|Entspricht dem vom System generierten Spaltenwert. Entspricht **sys.columns.is_hidden**|**Gilt für**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Nicht ausgeblendet<br /><br /> 1 = Ausgeblendet|  
  
## <a name="return-types"></a>Rückgabetypen
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.
  
Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. COLUMNPROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Remarks  
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
[Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen (Transact-SQL))](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  
