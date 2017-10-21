---
title: Char und Varchar (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c7bcb0e8ad7f8904703bd6c979b00aa30dd5348
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="char-and-varchar-transact-sql"></a>char und varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Diese Datentypen sind der fester oder variabler Länge.  
  
## <a name="arguments"></a>Argumente  
**Char** [(  *n*  )] fester Länge, nicht-Unicode-Zeichenfolgendaten. *n*definiert die Zeichenfolgenlänge und muss ein Wert zwischen 1 und 8.000 sein. Die Speichergröße beträgt  *n*  Bytes. Das ISO-Synonym für **Char** ist **Zeichen**.
  
**Varchar** [(  *n*   |  **max** )] variabler Länge, nicht-Unicode-Zeichenfolgendaten. *n*definiert die Zeichenfolgenlänge und kann ein Wert zwischen 1 und 8.000 sein. **Max.** gibt an, dass die maximale Speichergröße 2 ^ 31-1 Bytes (2 GB). Die Speicherplatzgröße ist die tatsächliche Länge der eingegebenen Daten + 2 Byte. Die ISO-Synonyme für **Varchar** sind **Charvarying** oder **Charactervarying**.
  
## <a name="remarks"></a>Hinweise  
Wenn  *n*  ist nicht angegeben in einer Datendefinitions- oder variablendeklarationsanweisung, die Standardlänge 1. Wenn  *n*  nicht angegeben wird, wenn die Funktionen CAST und CONVERT verwenden die Standardlänge 30.
  
Objekten, **Char** oder **Varchar** werden die standardsortierung der Datenbank zugewiesen, es sei denn, eine bestimmte Sortierung zugewiesen ist, mithilfe der COLLATE-Klausel. Die Sortierung bestimmt die Codepage, die zum Speichern der Zeichendaten verwendet wird.
  
Wenn Sie Standorte, die mehrere Sprachen zu unterstützen haben, erwägen Sie die Unicode **Nchar** oder **Nvarchar** Datentypen, um Probleme mit der zeichenkonvertierung zu minimieren. Bei Verwendung von **Char** oder **Varchar**, empfehlen wir Folgendes:
- Verwendung **Char** Wenn die Größen der spaltendateneinträge konsistent sind.  
- Verwendung **Varchar** Wenn die Größen der spaltendateneinträge erheblich variieren.  
- Verwendung **varchar(max)** Wenn die Größen der spaltendateneinträge unterschliedlich lang und die Größe möglicherweise 8.000 Byte überschreiten.  
  
Wenn SET ANSI_PADDING auf OFF festgelegt ist, bei der CREATE TABLE- oder ALTER TABLE ausgeführt wird, eine **Char** als NULL, als behandelt wird definierte Spalte **Varchar**.
  
Wenn die Codeseite der zielsortierung Doppelbytezeichen verwendet, ist immer noch die Speichergröße  *n*  Bytes. Abhängig von der Zeichenfolge, die Speichergröße der  *n*  Bytes kann weniger als  *n*  Zeichen.

> [!WARNING]
> Jeder nicht-Null-varchar(max) bzw. nvarchar(max)-Spalte erfordert 24 Byte zusätzliche feste Verteilung, das für das Zeilenlimit von 8.060 Byte während eines Sortiervorgangs zählt. Dies kann zur Erstellung einer impliziten Beschränkung der Anzahl der nicht-Null-varchar(max) bzw. nvarchar(max)-Spalten, die in einer Tabelle erstellt werden können.  
Beim Erstellen der Tabelle (außerhalb der üblichen Warnung darüber, dass die maximale Zeilengröße das zulässige Maximum von 8.060 Bytes überschreitet) oder zum Zeitpunkt der Dateneinfügung wird kein spezieller Fehler ausgegeben. Diese große Zeilengröße kann während einiger normaler Vorgänge Fehler (z. B. Fehler 512) verursachen. Dazu gehören z. B. die Aktualisierung des gruppierten Indexschlüssels oder Teile des vollständigen Spaltensatzes. Bis zum Ausführen eines Vorgangs können Benutzer diese Fehler nicht vorhersehen.
  
##  <a name="_character"></a>Konvertieren von Zeichendaten  
Werden Zeichenausdrücke in einen Zeichendatentyp mit einer anderen Größe konvertiert, dann werden Werte, die für den neuen Datentyp zu lang sind, abgeschnitten. Der **uniqueidentifier** -Typ wird bei der Konvertierung von Zeichenausdrücken als Zeichentyp behandelt und unterliegt daher den Kürzungsregeln für die Konvertierung in einen Zeichentyp. Weitere Informationen finden Sie im Abschnitt "Beispiele" weiter unten.
  
Wenn ein Zeichenausdruck konvertiert in einen Zeichenausdruck eines anderen Datentyp oder die Größe, wie z. B. aus **char(5)** auf **varchar(5)**, oder **char(20)** auf **char(15)**, wird die Sortierung des Eingabewerts dem konvertierten Wert zugewiesen. Wird ein Nichtzeichenausdruck zu einem Zeichendatentyp konvertiert, wird die Standardsortierung der aktuellen Datenbank dem konvertierten Wert zugewiesen. In beiden Fällen können Sie eine bestimmte Sortierung zuweisen, indem Sie mit der [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) Klausel.
  
> [!NOTE]  
>  Codepageübersetzungen werden für unterstützt **Char** und **Varchar** Datentypen, jedoch nicht für **Text** -Datentyp. Wie auch bei früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird der Datenverlust während der Codepageübersetzung nicht gemeldet.  
  
Zeichenausdrücke, die in einen ungefähren konvertiert werden **numerischen** -Datentyp kann optionale Exponentialschreibweise enthalten (den Kleinbuchstaben e oder E Großbuchstaben gefolgt, ein optionales Plus-(+) oder Minuszeichen (-) und dann eine Zahl).
  
Zeichenausdrücke, die in einen exakten konvertiert werden **numerischen** Datentyp bestehen muss aus Ziffern, einem Dezimaltrennzeichen und einem optionalen Plus-(+) oder Minuszeichen (-). Führende Leerzeichen werden ignoriert. Kommas als Trennzeichen (z. B. das Trennzeichen in 123.456,00) sind in der Zeichenfolge nicht zulässig.
  
Zeichenausdrücke, die er konvertiert **Money** oder **Smallmoney** Datentypen können auch einen optionalen Dezimaltrennzeichen und ein Dollarzeichen ($) enthalten. Kommas als Trennzeichen (wie in 123.456,00 $) sind zulässig.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. Anzeigen des Standardwerts von n bei Verwendung in einer Variablendeklaration.  
Das folgende Beispiel zeigt den Standardwert  *n*  ist 1 für die `char` und `varchar` -Datentypen, wenn sie in einer Variablendeklaration verwendet werden.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. Anzeigen des Standardwerts von n, wenn varchar mit CAST und CONVERT verwendet wird.  
Das folgende Beispiel zeigt, dass den Wert von  *n*  30 bei der `char` oder `varchar` Datentypen verwendet werden, mit der `CAST` und `CONVERT` Funktionen.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. Konvertieren von Daten zu Anzeigezwecken  
Im folgenden Beispiel werden zwei Spalten in Zeichentypen konvertiert und ein bestimmtes Format auf die angezeigten Daten angewendet. Ein **Money** Typ wird in Zeichendaten konvertiert und Format 1 wird angewendet, woraufhin die Werte durch Kommas jeder dritten Ziffer links vom Dezimaltrennzeichen und zwei Ziffern rechts vom Dezimaltrennzeichen an. Ein **"DateTime"** Typ wird in Zeichendaten konvertiert und Format 3 wird angewendet, die die Daten im Format tt/mm/jj angezeigt. In der WHERE-Klausel einer **Money** Typ in einen Zeichentyp auszuführenden Zeichenfolgenvergleich umgewandelt wird.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat  
---------------- --------------------- ------------- ----------------------- -----------------  
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11  
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11  
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11  
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11  
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11  
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11  
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11  
```  
  
### <a name="d-converting-uniqueidentifer-data"></a>D. Konvertieren von uniqueidentifier-Daten  
Das folgende Beispiel konvertiert einen `uniqueidentifier` -Wert in einen `char` -Datentyp.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
Im folgenden Beispiel wird das Abschneiden von Daten veranschaulicht, wenn der Wert zu lang für den Datentyp ist, in den er konvertiert wird. Da der **uniqueidentifier** -Typ auf 36 Zeichen beschränkt ist, werden die Zeichen, die diese Länge überschreiten, abgeschnitten.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[nchar und nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Schätzen der Größe einer Datenbank](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  

