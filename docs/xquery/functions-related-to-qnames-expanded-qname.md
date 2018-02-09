---
title: Expanded-QName (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9a00b0b5f6e21f8590c4dee3e1a588d0203f004
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Funktionen im Zusammenhang mit QNames - expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt einen Wert vom Typ xs: QName mit dem angegebenen Namespace-URI in der *$paramURI* und der lokale Name angegeben wird, der *$paramLocal*. Wenn *$paramURI* leere Zeichenfolge oder eine leere Sequenz ist, wird kein Namespace dar.  
  
## <a name="syntax"></a>Syntax  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>Argumente  
 *$paramURI*  
 Der Namespace-URI (Universal Resource Identifier) für QName.  
  
 *$paramLocal*  
 Der lokale Teil des Namens von QName.  
  
## <a name="remarks"></a>Hinweise  
 Die folgenden Informationen gelten für die **expanded-QName()** Funktion:  
  
-   Wenn die *$paramLocal* angegebene Wert ist nicht in der richtigen Form für xs: NCName-Typ, die leere Sequenz zurückgegeben, und stellt einen dynamischen Fehler.  
  
-   Das Konvertieren des Typs xs:QName in andere Typen wird in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nicht unterstützt. Aus diesem Grund die **expanded-QName()** Funktion kann nicht im XML-Konstruktion verwendet werden. Wenn Sie beispielsweise einen Knoten wie `<e> expanded-QName(…) </e>` konstruieren, darf der Wert nicht typisiert sein. Um dies zu erreichen, müssten Sie den von `expanded-QName()` zurückgegebenen Wert vom Typ xs:QName in xdt:untypedAtomic konvertieren. Dies wird jedoch nicht unterstützt. Eine Lösungsmöglichkeit wird nachfolgend in diesem Thema bereitgestellt.  
  
-   Sie können vorhandene Werte vom Typ QName ändern oder vergleichen. Beispielsweise `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` vergleicht den Wert des Elements <`e`>, mit der QName zurückgegebenes der **expanded-QName()** Funktion.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** in Spalten vom Typ der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. Ersetzen eines Knotenwerts vom Typ QName  
 In diesem Beispiel wird veranschaulicht, wie Sie den Wert eines Elementknotens vom Typ QName ändern können. Das Beispiel führt die folgenden Aktionen aus:  
  
-   Erstellen einer XML-Schemaauflistung, die ein Element vom Typ QName definiert.  
  
-   Erstellt eine Tabelle mit einer **Xml** Typspalte mithilfe der XML-schemaauflistung.  
  
-   Speichern einer XML-Instanz in der Tabelle.  
  
-   Verwendet die **modify()** Methode des XML-Datentyps zum Ändern des Werts eines Elements vom Typ QName in der Instanz. Die **expanded-QName()** Funktion wird verwendet, um den neuen Wert der QName-Typ zu generieren.  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 In der folgenden Abfrage die <`ElemQN`> Wert des Elements wird mithilfe von ersetzt die **modify()** -Methode des Xml-Datentyps und des Replace Value of XML DML, wie dargestellt.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("http://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Dies ist das Ergebnis. Beachten Sie, dass das <`ElemQN`>-Element vom Typ QName jetzt über einen neuen Wert verfügt:  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="http://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 Die folgenden Anweisungen entfernen die in diesem Beispiel verwendeten Objekte.  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. Umgehend mit den Einschränkungen bei Verwendung der erweiterten QName()-Funktion  
 Die **expanded-QName** Funktion kann nicht im XML-Konstruktion verwendet werden. Dies wird anhand des folgenden Beispiels veranschaulicht. Im Beispiel wird zuerst ein Knoten eingefügt, um diese Einschränkung zu umgehen, und dann wird der Knoten geändert.  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="http://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 Im folgenden Versuch wird ein weiteres <`root`>-Element hinzugefügt. Dadurch wird jedoch ein Fehler erzeugt, da die erweiterte QName()-Funktion in der XML-Konstruktion nicht unterstützt wird.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Dies kann vermieden werden, indem zunächst eine Instanz mit einem Wert für das <`root`>-Element eingefügt und anschließend bearbeitet wird. In diesem Beispiel wird zunächst ein Nullwert verwendet, wenn das <`root`>-Element eingefügt wird. Die XML-Schemaauflistung in diesem Beispiel lässt einen Nullwert für das <`root`>-Element zu.  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="http://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Sie können den Wert für QName vergleichen, wie in der folgenden Abfrage gezeigt: Die Abfrage gibt nur den <`root`> Elemente, deren Werte den QName entsprechen, Typwert zurückgegebenes der **expanded-QName()** Funktion.  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Es wird eine Einschränkung: die **expanded-QName()** Funktion die leere Sequenz als zweites Argument akzeptiert und gibt zurück, statt einen Laufzeitfehler auszulösen, wenn das zweite Argument fehlerhaft ist leer.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen, die im Zusammenhang mit QNames &#40; XQuery &#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
