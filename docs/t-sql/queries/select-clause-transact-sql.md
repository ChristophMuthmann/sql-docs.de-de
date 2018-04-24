---
title: SELECT-Klausel (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e0b0623f0bf5068fc6c29fcf8ead31e1eb039105
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="select-clause-transact-sql"></a>SELECT-Klausel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Spalten an, die von der Abfrage zurückgegeben werden sollen.  
  
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
  
 TOP (*expression* ) [ PERCENT ] [ WITH TIES ]  
 Gibt an, dass das Resultset der Abfrage nur eine angegebene erste Gruppe oder einen Prozentsatz von Zeilen zurückgibt. *expression* kann eine Anzahl oder ein Prozentsatz der Zeilen sein.  
  
 Aus Gründen der Abwärtskompatibilität wird die Verwendung von TOP *expression* ohne Klammern in SELECT-Anweisungen unterstützt, jedoch nicht empfohlen. Weitere Informationen finden Sie unter [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
\< select_list > Die für das Resultset auszuwählenden Spalten. Die Auswahlliste besteht aus einer Reihe von Ausdrücken, die durch Kommas voneinander getrennt sind. Maximal können in der Auswahlliste 4096 Ausdrücke angegeben werden.  
  
 \*  
 Gibt an, dass alle Spalten aus allen Tabellen und Sichten in der FROM-Klausel zurückgegeben werden sollen. Die Spalten werden wie in der FROM-Klausel angegeben nach Tabellen oder Sichten sortiert sowie in der Reihenfolge zurückgegeben, in der sie in der Tabelle vorhanden sind.  
  
 *table_name* | *view_name* | *table*_*alias*.*  
 Beschränkt den Gültigkeitsbereich von \* auf die angegebene Tabelle oder Sicht.  
  
 *column_name*  
 Dies ist der Name einer Spalte, die zurückgegeben werden soll. Kennzeichnen Sie *column_name*, um einen mehrdeutigen Verweis zu verhindern, der vorkommen kann, wenn zwei Tabellen in der FROM-Klausel Spalten mit dem gleichen Namen enthalten. Beispiel: Die beiden Tabellen SalesOrderHeader und SalesOrderDetail in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank haben beide eine Spalte mit dem Namen ModifiedDate. Wenn beide Tabellen in einer Abfrage zusammengeführt werden, kann das modifizierte Datum der Einträge in SalesOrderDetail in der Auswahlliste als SalesOrderDetail.ModifiedDate angegeben werden.  
  
 *expression*  
 Eine Konstante, eine Funktion oder eine beliebige, durch einen oder mehrere Operatoren verknüpfte Kombination von Spaltennamen, Konstanten und Funktionen oder eine Unterabfrage.  
  
 $IDENTITY  
 Gibt die Identitätsspalte zurück. Weitere Informationen finden Sie unter [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md), [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) und [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 Falls mehrere Tabellen in der FROM-Klausel eine Spalte mit der IDENTITY-Eigenschaft enthalten, muss $IDENTITY mit dem jeweiligen Tabellennamen gekennzeichnet werden, wie z. B. T1.$IDENTITY.  
  
 $ROWGUID  
 Gibt die ROWGUID-Spalte zurück.  
  
 Falls mehrere Tabellen in der FROM-Klausel eine Spalte mit der ROWGUIDCOL-Eigenschaft enthalten, muss $ROWGUID mit dem jeweiligen Tabellennamen gekennzeichnet werden, wie z. B. T1.$ROWGUID.  
  
 *udt_column_name*  
 Der Name einer Spalte des CLR-benutzerdefinierten Typs, die zurückgegeben werden soll.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gibt Werte für benutzerdefinierte Typen in binärer Darstellung zurück. Wenn Sie Werte für benutzerdefinierte Typen im Zeichenfolgen- oder XML-Format zurückgeben möchten, verwenden Sie [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) oder [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 { . | :: }  
 Gibt eine Methode, Eigenschaft oder ein Feld eines CLR-benutzerdefinierten Typs an. Verwenden Sie . für eine (nicht statische) Instanzmethode, Eigenschaft oder ein Feld. Verwenden Sie :: für eine statische Methode, Eigenschaft oder ein Feld. Zum Aufrufen einer Methode, Eigenschaft oder eines Felds eines CLR-benutzerdefinierten Typs müssen Sie über die EXECUTE-Berechtigung für den Typ verfügen.  
  
 *property_name*  
 Eine öffentliche Eigenschaft von *udt_column_name*.  
  
 *field_name*  
 Ein öffentliches Datenelement von *udt_column_name*.  
  
 *method_name*  
 Eine öffentliche Methode von *udt_column_name*, die ein oder mehrere Argumente umfassen kann. *method_name* darf keine Mutatormethode sein.  
  
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
  
 *column_alias* kann in einer ORDER BY-Klausel verwendet werden. Sie kann jedoch nicht in einer WHERE-, GROUP BY- oder HAVING-Klausel verwendet werden. Falls der Abfrageausdruck Teil einer DECLARE CURSOR-Anweisung ist, kann *column_alias* nicht in der FOR UPDATE-Klausel verwendet werden.  
  
## <a name="remarks"></a>Remarks  
 Als Länge für die in der Auswahlliste enthaltenen Spalten vom Typ **text** oder **ntext** wird jeweils die kleinste der folgenden Größen zurückgegeben: die tatsächliche Größe der **text**-Spalte, die Standardeinstellung für TEXTSIZE für die Sitzung oder die im Code der Anwendung festgelegte Größenbeschränkung. Sie können die Länge des zurückgegebenen Texts für eine Sitzung mit der SET-Anweisung ändern. Standardmäßig ist die Länge von Textdaten, die mit einer SELECT-Anweisung zurückgegeben werden, auf 4.000 Byte begrenzt.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] löst die Ausnahme 511 aus und führt einen Rollback für die derzeit ausgeführte Anweisung aus, wenn eine der folgenden Situationen auftritt:  
  
-   Die SELECT-Anweisung erstellt eine Ergebniszeile oder eine Zeile in der temporären Arbeitstabelle, die 8.060 Byte überschreitet.  
  
-   Die DELETE-, INSERT- oder UPDATE-Anweisung versucht, eine Aktion für eine Zeile durchzuführen, die größer als 8.060 Byte ist.  
  
 Ein Fehler tritt auf, wenn eine mit SELECT INTO oder CREATE VIEW erstellte Spalte keinen Spaltennamen besitzt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Beispiele für SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
