---
title: Ausdruckskontext und Ausdrucksauswertung (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa51ff95256dde4ed6d750a2dbfab5c2c44c2d41
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="expression-context-and-query-evaluation-xquery"></a>Ausdruckskontext und Ausdrucksauswertung (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Der Kontext eines Ausdrucks sind die Informationen, die zum Analysieren und Auswerten des Ausdrucks verwendet werden. Die Auswertung von XQuery erfolgt in den folgenden beiden Phasen:  
  
-   **Statischer Kontextname** – Dies ist die Phase der Abfragekompilierung. Auf der Basis der verfügbaren Informationen werden während dieser statischen Analyse der Abfrage manchmal Fehler ausgelöst.  
  
-   **Dynamischer Kontext** – Dies ist die Phase der abfrageausführung. Selbst wenn eine Abfrage keine statischen Fehler wie z. B. Fehler während der Abfragekompilierung aufweist, kann die Abfrage trotzdem während ihrer Ausführung Fehler auslösen.  
  
## <a name="static-context"></a>Statischer Kontext  
 Als Initialisierung des statischen Kontexts wird der Prozess bezeichnet, in dem alle Informationen für die statische Analyse des Ausdrucks zusammengestellt werden. Im Rahmen der Initialisierung des statischen Kontexts werden die folgenden Schritte durchgeführt:  
  
-   Die **grenzleerzeichen** Richtlinie wird festgelegt, um zu entfernen. Aus diesem Grund wird das grenzleerzeichen nicht durch Beibehalten der **jedes Element** und **Attribut** Konstruktoren in der Abfrage. Beispiel:  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     Diese Abfrage gibt das folgende Ergebnis zurück, weil das Grenzleerzeichen beim Analysieren des XQuery-Ausdrucks entfernt wird:  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   Das Präfix und die Namespacebindung werden für folgende Namespaces initialisiert:  
  
    -   Einen Satz von vordefinierten Namespaces.  
  
    -   Alle mithilfe von WITH XMLNAMESPACES definierten Namespaces. Weitere Informationen finden Sie unter [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)).  
  
    -   Alle im Abfrageprolog definierten Namespaces. Beachten Sie, dass die Namespacedeklarationen im Prolog die Namespacedeklaration in WITH XMLNAMESPACES überschreiben können. WITH XMLNAMESPACES deklariert z. B. in der folgenden Abfrage wird ein Präfix (pd), die sie an den Namespace gebunden (`http://someURI`). Diese Bindung wird jedoch in der WHERE-Klausel durch den Abfrageprolog überschrieben.  
  
        ```  
        WITH XMLNAMESPACES ('http://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     Alle diese Namespacebindungen werden bei der Initialisierung des statischen Kontexts aufgelöst.  
  
-   Abfragen einer typisierten **Xml** Spalte oder Variablen, die Bestandteile der Spalte oder Variablen zugeordnete XML-schemaauflistung in statischen Kontext importiert werden. Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
-   Für jeden atomaren Typ in den importierten Schemas wird im statischen Kontext auch eine Umwandlungsfunktion verfügbar gemacht. Dies wird im folgenden Beispiel veranschaulicht. In diesem Beispiel wird eine Abfrage angegeben für eine typisierte **Xml** Variable. Die dieser Variablen zugeordnete XML-Schemaauflistung definiert den atomaren Typ myType. In diesen Typ, eine Umwandlungsfunktion entsprechende **myType()**, während der statischen Analyse zur Verfügung steht. Der Abfrageausdruck (`ns:myType(0)`) gibt einen Wert von myType zurück.  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     Im folgenden Beispiel die Umwandlungsfunktion für die **Int** integrierte XML-Datentyp im Ausdruck angegeben ist.  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 Nachdem der statische Kontext initialisiert wurde, wird der Abfrageausdruck analysiert (kompiliert). Die statische Analyse umfasst die folgenden Schritte:  
  
1.  Analysieren der Abfrage.  
  
2.  Auflösen der im Ausdruck angegebenen Funktions- und Typnamen.  
  
3.  Statisches Typisieren der Abfrage. Damit wird sichergestellt, dass die Abfrage typsicher ist. Beispielsweise gibt die folgende Abfrage einen statischen Fehler zurück, da die **+** Operator erfordert numerischen Grundtyp Argumente:  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     Im folgenden Beispiel die **value()** Operator erfordert einen Singleton. Wie in der XML-Schema angegeben ist, treten möglicherweise mehrere \<Elem >-Elemente. Bei der statischen Analyse des Ausdrucks wird ermittelt, dass der Ausdruck nicht typsicher ist, und es wird ein statischer Fehler zurückgegeben. Um den Fehler aufzulösen, muss der Ausdruck so umgeschrieben werden, dass er explizit einen Singleton-Wert angibt (`data(/x:Elem)[1]`).  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     Weitere Informationen finden Sie unter [XQuery and Static Typing](../xquery/xquery-and-static-typing.md).  
  
### <a name="implementation-restrictions"></a>Einschränkungen für die Implementierung  
 Im Zusammenhang mit dem statischen Kontext gelten die folgenden Einschränkungen:  
  
-   Der XPath-Kompatibilitätsmodus wird nicht unterstützt.  
  
-   Für die XML-Konstruktion wird nur der strip-Konstruktionsmodus unterstützt. Dies ist die Standardeinstellung. Aus diesem Grund ist der Typ des konstruierten Elements vom **Xdt: nicht typisierte** Typ und die Attribute sind von **xdt: UntypedAtomic** Typ.  
  
-   Es wird nur der der ordered-Sortiermodus strip XML unterstützt.  
  
-   Es wird nur die strip-XML-Leerzeichenrichtlinie unterstützt.  
  
-   Die Basis-URI-Funktionalität wird nicht unterstützt.  
  
-   **Fn:doc()** wird nicht unterstützt.  
  
-   **Fn:Collection()** wird nicht unterstützt.  
  
-   Es wird kein statischer Flagger für XQuery bereitgestellt.  
  
-   Die zugeordnete Sortierung der **Xml** -Datentyp verwendet wird. Diese Sortierreihenfolge ist immer auf die Unicode-Codepunktsortierreichenfolge festgelegt.  
  
## <a name="dynamic-context"></a>Dynamischer Kontext  
 Unter dem dynamischen Kontext werden die Informationen verstanden, die zum Zeitpunkt der Ausführung des Ausdrucks verfügbar sein müssen. Zusätzlich zum statischen Kontext werden die folgenden Informationen als Bestandteil des dynamischen Kontexts initialisiert:  
  
-   Der Schwerpunkt des Ausdrucks, z. B. das Kontext-Item, die Kontextposition und die Kontextgröße, werden entsprechend dem folgenden Beispiel initialisiert. Beachten Sie, die alle diese Werte können, indem überschrieben werden die [Nodes()-Methode](../t-sql/xml/nodes-method-xml-data-type.md).  
  
    -   Die **Xml** Datentyp legt das Kontextelement, das gerade verarbeiteten Knoten, auf den Dokumentknoten fest.  
  
    -   Die Kontextposition, also die Position des Kontext-Items im Verhältnis zu den gerade verarbeiteten Knoten, wird auf 1 festgelegt.  
  
    -   Die Kontextgröße, also die Anzahl der Items in der Sequenz, die gerade verarbeitet wird, wird zunächst auf 1 festgelegt, weil es immer einen Dokumentknoten gibt.  
  
### <a name="implementation-restrictions"></a>Einschränkungen für die Implementierung  
 Im Zusammenhang mit dem dynamischen Kontext gelten die folgenden Einschränkungen:  
  
-   Die **aktuelles Datum und Uhrzeit** kontextfunktionen, **Fn:current-Datum**, **Fn:current-Zeit**, und **Fn:current-"DateTime"**, sind nicht unterstützt.  
  
-   Die **implizite Zeitzone** wird auf UTC + 0 festgelegt und kann nicht geändert werden.  
  
-   Die **Fn:doc()** Funktion wird nicht unterstützt. Werden alle Abfragen für ausgeführt **Xml** Spalten oder Variablen vom Typ.  
  
-   Die **Fn:collection()** Funktion wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Grundlagen](../xquery/xquery-basics.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
