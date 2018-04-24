---
title: delete (XML DML) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- delete keyword
- delete statement [XML DML]
- deleting nodes
ms.assetid: b22c93a4-b84d-4356-af4c-6013322a4b71
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a3f4fbaa3652c34e0fc2a15115459cd1b6bb7769
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="delete-xml-dml"></a>delete (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Löscht Knoten aus einer XML-Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
delete Expression  
```  
  
## <a name="arguments"></a>Argumente  
 *Ausdruck*  
 Ein XQuery-Ausdruck, der die zu löschenden Knoten identifiziert. Alle durch den Ausdruck ausgewählten Knoten sowie alle Knoten oder Werte, die darin enthalten sind, werden gelöscht. Wie unter [insert (XML DML)](../../t-sql/xml/insert-xml-dml.md) beschrieben, muss dabei auf einen im Dokument vorhandenen Knoten verwiesen werden. Es darf sich nicht um einen konstruierten Knoten handeln. Der Ausdruck darf nicht der Stammknoten (/) sein. Wenn der Ausdruck eine leere Sequenz zurückgibt, wird nichts gelöscht, und es werden keine Fehler zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-deleting-nodes-from-a-document-stored-in-an-untyped-xml-variable"></a>A. Löschen von Knoten aus einem in einer nicht typisierten XML-Variablen gespeicherten Dokument  
 Das folgende Beispiel veranschaulicht das Löschen verschiedener Knoten aus einem Dokument. Zuerst wird einer Variablen vom Typ **xml** eine XML-Instanz zugewiesen. Anschließend löschen XML DML-Anweisungen verschiedene Knoten aus dem Dokument.  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<?Instructions for=TheWC.exe ?>   
<Root>  
 <!-- instructions for the 1st work center -->  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Some text 1  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
SELECT @myDoc  
  
-- delete an attribute  
SET @myDoc.modify('  
  delete /Root/Location/@MachineHours  
')  
SELECT @myDoc  
  
-- delete an element  
SET @myDoc.modify('  
  delete /Root/Location/step[2]  
')  
SELECT @myDoc  
  
-- delete text node (in <Location>  
SET @myDoc.modify('  
  delete /Root/Location/text()  
')  
SELECT @myDoc  
  
-- delete all processing instructions  
SET @myDoc.modify('  
  delete //processing-instruction()  
')  
SELECT @myDoc  
```  
  
### <a name="b-deleting-nodes-from-a-document-stored-in-an-untyped-xml-column"></a>B. Löschen von Knoten aus einem in einer nicht typisierten XML-Spalte gespeicherten Dokument  
 Im folgenden Beispiel entfernt die XML DML-Anweisung für **delete** das zweite untergeordnete Element von <`Features`> aus dem in der Spalte gespeicherten Dokument.  
  
```  
CREATE TABLE T (i int, x xml)  
go  
INSERT INTO T VALUES(1,'<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>')  
go  
-- verify the contents before delete  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
-- delete the second feature  
UPDATE T  
SET x.modify('delete /Root/ProductDescription/Features/*[2]')  
-- verify the deletion  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die [modify()-Methode (XML-Datentyp)](../../t-sql/xml/modify-method-xml-data-type.md) wird verwendet, um das XML DML-Schlüsselwort für **delete** anzugeben.  
  
-   Die [query()-Methode (xml-Datentyp)](../../t-sql/xml/query-method-xml-data-type.md) wird verwendet, um das Dokument abzufragen.  
  
### <a name="c-deleting-nodes-from-a-typed-xml-column"></a>C. Löschen von Knoten aus einer typisierten XML-Spalte  
 Im folgenden Beispiel werden Knoten aus dem in einer typisierten **xml** -Spalte gespeicherten XML-Dokument mit den Fertigungsanweisungen gelöscht.  
  
 In diesem Beispiel erstellen Sie zunächst eine Tabelle (T) mit einer typisierten **xml** -Spalte in der AdventureWorks-Datenbank. Anschließend kopieren Sie eine XML-Instanz der Fertigungsanweisungen aus der Instructions-Spalte der ProductModel-Tabelle in Tabelle T und löschen einen oder mehrere Knoten aus dem Dokument.  
  
```  
use AdventureWorks  
go  
drop table T  
go  
create table T(ProductModelID int primary key,   
Instructions xml (Production.ManuInstructionsSchemaCollection))  
go  
insert  T   
select ProductModelID, Instructions  
from Production.ProductModel  
where ProductModelID=7  
go  
select Instructions  
from T  
--1) insert <Location 1000/>. Note: <Root> must be singleton in the query  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  insert <MI:Location LocationID="1000"  LaborHours="1000" >  
           These are manu steps at location 1000.   
           <MI:step>New step1 instructions</MI:step>  
           Instructions for step 2 are here  
           <MI:step>New step 2 instructions</MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
  
-- delete an attribute  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/@LaborHours)   
')  
go  
select Instructions  
from T  
-- delete text in <location>  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/text())   
')  
go  
select Instructions  
from T  
-- delete 2nd manu step at location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/MI:step[2])   
')  
go  
select Instructions  
from T  
-- cleanup  
drop table T  
go  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;Data Modification Language&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
