---
title: SELECT-Klausel (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT Clause
- SELECT_Clause_TSQL
- DISTINCT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- identity columns [SQL Server], SELECT clause
- SELECT clause
- $IDENTITY keyword
- user-defined types [SQL Server], invoking methods and properties
- SELECT statement [SQL Server], processing orders
- clauses [SQL Server], SELECT
- $ROWGUID keyword
- queries [SQL Server], results
ms.assetid: 2616d800-4853-4cf1-af77-d32d68d8c2ef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 34a1dee420dd8e409df2043f3278a32235656ace
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select-clause-transact-sql"></a>SELECT-Klausel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Spalten von der Abfrage zurückgegeben werden sollen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT [ ALL | DISTINCT ]  
[ TOP ( expression ) [ PERCENT ] [ WITH TIES ] ]   
<select_list>   
<select_list> ::=   
    {   
      *   
      | { table_name | view_name | table_alias }.*   
      | {  
          [ { table_name | view_name | table_alias }. ]  
               { column_name | $IDENTITY | $ROWGUID }   
          | udt_column_name [ { . | :: } { { property_name | field_name }   
            | method_name ( argument [ ,...n] ) } ]  
          | expression  
          [ [ AS ] column_alias ]   
         }  
      | column_alias = expression   
    } [ ,...n ]   
```  
  
## <a name="arguments"></a>Argumente  
 **ALL**  
 Gibt an, dass das Resultset doppelte Zeilen enthalten darf. ALL ist die Standardeinstellung.  
  
 DISTINCT  
 Gibt an, dass im Resultset nur eindeutige Zeilen vorkommen dürfen. NULL-Werte werden für das DISTINCT-Schlüsselwort als gleich angesehen.  
  
 Nach oben (*Ausdruck* ) [PERCENT] [WITH TIES]  
 Gibt an, dass das Resultset der Abfrage nur eine angegebene erste Gruppe oder einen Prozentsatz von Zeilen zurückgibt. *expression* kann eine Anzahl oder ein Prozentsatz der Zeilen sein.  
  
 Für die Abwärtskompatibilität zur Verwendung von TOP *Ausdruck* ohne Klammern in SELECT-Anweisungen unterstützt, aber es wird nicht empfohlen. Weitere Informationen finden Sie unter [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
\<Select_list > die Spalten für das Resultset ausgewählt werden. Die Auswahlliste besteht aus einer Reihe von Ausdrücken, die durch Kommas voneinander getrennt sind. Maximal können in der Auswahlliste 4096 Ausdrücke angegeben werden.  
  
 \*  
 Gibt an, dass alle Spalten aus allen Tabellen und Sichten in der FROM-Klausel zurückgegeben werden sollen. Die Spalten werden wie in der FROM-Klausel angegeben nach Tabellen oder Sichten sortiert sowie in der Reihenfolge zurückgegeben, in der sie in der Tabelle vorhanden sind.  
  
 *table_name* | *view_name* | *table*_*alias*.*  
 Beschränkt den Bereich der \* an der angegebenen Tabelle oder Sicht.  
  
 *column_name*  
 Dies ist der Name einer Spalte, die zurückgegeben werden soll. Qualifizieren *Column_name* um einen mehrdeutigen Verweis zu verhindern, wie z. B. tritt auf, wenn zwei Tabellen erstellt in der FROM-Klausel Spalten mit doppelten Namen haben. Z. B. die Tabellen SalesOrderHeader und SalesOrderDetail in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank beide haben eine Spalte mit dem Namen ModifiedDate. Wenn beide Tabellen in einer Abfrage zusammengeführt werden, kann das modifizierte Datum der Einträge in SalesOrderDetail in der Auswahlliste als SalesOrderDetail.ModifiedDate angegeben werden.  
  
 *expression*  
 Eine Konstante, eine Funktion oder eine beliebige, durch einen oder mehrere Operatoren verknüpfte Kombination von Spaltennamen, Konstanten und Funktionen oder eine Unterabfrage.  
  
 $IDENTITY  
 Gibt die Identitätsspalte zurück. Weitere Informationen finden Sie unter [IDENTITÄTS- &#40; Eigenschaft der &#41; &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql-identity-property.md), [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md), und [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 Falls mehrere Tabellen in der FROM-Klausel eine Spalte mit der IDENTITY-Eigenschaft enthalten, muss $IDENTITY mit dem jeweiligen Tabellennamen gekennzeichnet werden, wie z. B. T1.$IDENTITY.  
  
 $ROWGUID  
 Gibt die ROWGUID-Spalte zurück.  
  
 Falls mehrere Tabellen in der FROM-Klausel eine Spalte mit der ROWGUIDCOL-Eigenschaft enthalten, muss $ROWGUID mit dem jeweiligen Tabellennamen gekennzeichnet werden, wie z. B. T1.$ROWGUID.  
  
 *udt_column_name*  
 Der Name einer Spalte des CLR-benutzerdefinierten Typs, die zurückgegeben werden soll.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gibt Werte für benutzerdefinierte Typen in binärer Darstellung zurück. UDT-Werte in der Zeichenfolge oder XML-Format zurückgeben möchten, verwenden [Umwandlung](../../t-sql/functions/cast-and-convert-transact-sql.md) oder [konvertieren](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 { . | :: }  
 Gibt eine Methode, Eigenschaft oder ein Feld eines CLR-benutzerdefinierten Typs an. Verwenden. für eine (nicht statische) Instanzmethode, Eigenschaft oder ein Feld. Verwenden Sie :: für eine statische Methode, Eigenschaft oder ein Feld. Zum Aufrufen einer Methode, Eigenschaft oder eines Felds eines CLR-benutzerdefinierten Typs müssen Sie über die EXECUTE-Berechtigung für den Typ verfügen.  
  
 *property_name*  
 Ist eine öffentliche Eigenschaft des *Udt_column_name*.  
  
 *field_name*  
 Ist ein öffentlicher Datenmember eines *Udt_column_name*.  
  
 *method_name*  
 Ist eine öffentliche Methode *Udt_column_name* , die ein oder mehrere Argumente annimmt. *keine Variablenargumentlisten verwenden* eine Mutatormethode darf nicht sein.  
  
 Im folgenden Beispiel werden die Werte für die `Location`-Spalte ausgewählt, für die der Typ `point` definiert ist. Die Auswahl erfolgt aus der `Cities`-Tabelle durch Aufruf einer Methode des Typs mit dem Namen `Distance`:  
  
```  
CREATE TABLE dbo.Cities (  
     Name varchar(20),  
     State varchar(20),  
     Location point );  
GO  
DECLARE @p point (32, 23), @distance float;  
GO  
SELECT Location.Distance (@p)  
FROM Cities;  
```  
  
 *column_ alias*  
 Dies ist ein alternativer Name, der den Spaltennamen im Abfrageresultset ersetzt. Für eine Spalte mit dem Namen quantity könnte z. B. ein Alias wie Quantity, Quantity to Date oder Qty angegeben werden.  
  
 Aliasnamen werden auch verwendet, um Namen für die Ergebnisse von Ausdrücken anzugeben, beispielsweise:  
  
 ```sql
 USE AdventureWorks2012;  
 GO  
 SELECT AVG(UnitPrice) AS [Average Price]  
 FROM Sales.SalesOrderDetail;
 ```  
  
 *Spaltenalias* können in einer ORDER BY-Klausel verwendet werden. Sie kann jedoch nicht in einer WHERE-, GROUP BY- oder HAVING-Klausel verwendet werden. Wenn der Abfrageausdruck Teil einer DECLARE CURSOR-Anweisung ist *Spaltenalias* kann nicht in der FOR UPDATE-Klausel verwendet werden.  
  
## <a name="remarks"></a>Hinweise  
 Die Länge der Daten, die für die zurückgegebenen **Text** oder **Ntext** Spalten, die in der select-Liste enthalten sind, wird die kleinste der folgenden festgelegt: die tatsächliche Größe der **Text** Spalte, die Standardeinstellung für TEXTSIZE-Sitzung oder den Grenzwert für die Anwendung hartcodiert. Sie können die Länge des zurückgegebenen Texts für eine Sitzung mit der SET-Anweisung ändern. Standardmäßig ist die Länge von Textdaten, die mit einer SELECT-Anweisung zurückgegeben werden, auf 4.000 Byte begrenzt.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] löst die Ausnahme 511 aus und führt einen Rollback für die derzeit ausgeführte Anweisung aus, wenn eine der folgenden Situationen auftritt:  
  
-   Die SELECT-Anweisung erstellt eine Ergebniszeile oder eine Zeile in der temporären Arbeitstabelle, die 8.060 Byte überschreitet.  
  
-   Die DELETE-, INSERT- oder UPDATE-Anweisung versucht, eine Aktion für eine Zeile durchzuführen, die größer als 8.060 Byte ist.  
  
 Ein Fehler tritt auf, wenn eine mit SELECT INTO oder CREATE VIEW erstellte Spalte keinen Spaltennamen besitzt.  
  
## <a name="see-also"></a>Siehe auch  
 [Wählen Sie die Beispiele &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
