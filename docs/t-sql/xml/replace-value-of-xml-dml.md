---
title: (XML DML) Replace Value of | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- update keyword
- replacement values [XML DML]
- updating node values
- replace value of XML DML statement
ms.assetid: c310f6df-7adf-493b-b56b-8e3143b13ae7
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7b559d81e2cca495885f740092ac182a4554a012
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="replace-value-of-xml-dml"></a>replace value of (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Aktualisiert den Wert eines Knotens im Dokument.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
replace value of Expression1   
with Expression2  
```  
  
## <a name="arguments"></a>Argumente  
 *Expression1*  
 Gibt einen Knoten an, dessen Wert aktualisiert werden soll. Der Ausdruck darf nur einen einzelnen Knoten angeben. Das heißt, *Expression1* muss ein statisches Singleton sein. Wenn das XML typisiert ist, muss der Typ des Knotens ein simple-Typ sein. Wenn mehrere Knoten ausgewählt werden, wird ein Fehler ausgelöst. Wenn *Expression1* eine leere Sequenz zurückgibt, tritt keine Wertersetzung auf, und es werden keine Fehler zurückgegeben. *Expression1* muss ein einzelnes Element zurückgeben, das einfach typisierten Inhalt besitzt (list- oder atomic-Typen) oder ein Textknoten bzw. ein Attributknoten ist. *Expression1* kann nicht dem union-Typ bzw. einem komplexen Typ angehören oder eine Verarbeitungsanweisung, ein Dokumentknoten oder ein Kommentarknoten sein. Anderenfalls wird ein Fehler zurückgegeben.  
  
 *Expression2*  
 Gibt den neuen Wert des Knotens an. Dabei kann es sich um einen Ausdruck handeln, der einen einfach typisierten Knoten zurückgibt, weil **data()** implizit verwendet wird. Wenn der Wert eine Werteliste ist, ersetzt die **update** -Anweisung den alten Wert durch die Liste. Beim Ändern einer typisierten XML-Instanz muss *Expression2* den gleichen Typ wie *Expression*1 aufweisen oder ein Untertyp davon sein. Ansonsten wird ein Fehler zurückgegeben. Beim Ändern einer nicht typisierten XML-Instanz muss *Expression2* ein Ausdruck sein, der atomisiert werden kann. Ansonsten wird ein Fehler zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele der XML DML **replace value of** -Anweisung zeigen, wie Knoten in einem XML-Dokument aktualisiert werden.  
  
### <a name="a-replacing-values-in-an-xml-instance"></a>A. Ersetzen von Werten in einer XML-Instanz  
 Im folgenden Beispiel wird eine Dokumentinstanz zuerst einer Variablen des Typs **xml** zugewiesen. Anschließend aktualisieren XML DML **replace value of** -Anweisungen die Werte im Dokument.  
  
```  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Manufacturing steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>';  
SELECT @myDoc;  
  
-- update text in the first manufacturing step  
SET @myDoc.modify('  
  replace value of (/Root/Location/step[1]/text())[1]  
  with     "new text describing the manu step"  
');  
SELECT @myDoc;  
-- update attribute value  
SET @myDoc.modify('  
  replace value of (/Root/Location/@LaborHours)[1]  
  with     "100.0"  
');  
SELECT @myDoc;  
```  
  
 Beachten Sie, dass das zu aktualisierende Ziel höchstens ein Knoten sein darf, der explizit im path-Ausdruck durch Hinzufügen von "[1]" am Ende des Ausdrucks angegeben wird.  
  
### <a name="b-using-the-if-expression-to-determine-replacement-value"></a>B. Verwenden des if-Ausdrucks zum Bestimmen des Ersetzungswerts  
 Sie können den **if** -Ausdruck in Expression2 der **XML DML replace value of** -Anweisung angeben, wie im folgenden Beispiel gezeigt wird. Expression1 gibt an, dass das LaborHours-Attribut aus dem ersten Arbeitsplatz aktualisiert werden soll. Expression2 verwendet einen **if** -Ausdruck zum Bestimmen des neuen Werts des LaborHours-Attributs.  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours=".1"  
            MachineHours=".2" >Manu steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
--SELECT @myDoc  
  
SET @myDoc.modify('  
  replace value of (/Root/Location[1]/@LaborHours)[1]  
  with (  
       if (count(/Root/Location[1]/step) > 3) then  
         "3.0"  
       else  
          "1.0"  
      )  
')  
SELECT @myDoc  
```  
  
### <a name="c-updating-xml-stored-in-an-untyped-xml-column"></a>C. Aktualisieren von XML, das in einer nicht typisierten XML-Spalte gespeichert ist  
 Das folgende Beispiel aktualisiert in einer Spalte gespeichertes XML:  
  
```  
drop table T  
go  
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
-- verify the current <ProductDescription> element  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
-- update the ProductName attribute value  
UPDATE T  
SET x.modify('  
  replace value of (/Root/ProductDescription/@ProductName)[1]  
  with "New Road Bike" ')  
-- verify the update  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
```  
  
### <a name="d-updating-xml-stored-in-a-typed-xml-column"></a>D. Aktualisieren von XML, das in einer typisierten XML-Spalte gespeichert ist  
 Dieses Beispiel ersetzt Werte in einem Dokument mit Fertigungsanweisungen, das in einer typisierten XML-Spalte gespeichert ist.  
  
 In diesem Beispiel erstellen Sie zuerst eine Tabelle (T) mit einer typisierten XML-Spalte in der AdventureWorks-Datenbank. Anschließend kopieren Sie eine XML-Instanz mit Fertigungsanweisungen aus der Instructions-Spalte in der ProductModel-Tabelle in Tabelle T. Die Einfügungen werden dann am XML in Tabelle T vorgenommen.  
  
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
--insert a new location - <Location 1000/>.   
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
insert <MI:Location LocationID="1000"  LaborHours="1000"  LotSize="1000" >  
           <MI:step>Do something using <MI:tool>hammer</MI:tool></MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
go  
-- Now replace manu. tool in location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/MI:step/MI:tool)[1]   
  with   "screwdriver"  
')  
go  
select Instructions  
from T  
-- Now replace value of lot size  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/@LotSize)[1]   
  with   500 cast as xs:decimal ?  
')  
go  
select Instructions  
from T  
```  
  
 Beachten Sie die Verwendung von **cast** beim Ersetzen des LotSize-Werts. Dies ist erforderlich, wenn der Wert einem bestimmten Typ angehören muss. In diesem Beispiel ist eine explizite Umwandlung nicht erforderlich, wenn der Wert 500 lautet.  
  
## <a name="see-also"></a>Siehe auch  
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

