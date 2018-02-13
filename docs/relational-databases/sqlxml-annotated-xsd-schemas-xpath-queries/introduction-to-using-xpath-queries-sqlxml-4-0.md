---
title: "Einführung in die Verwendung von XPath-Abfragen (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], about XPath queries
- W3C XPath specification
- XPath queries [SQLXML], functionality
ms.assetid: 01050a8e-0ccc-4a02-a4eb-b48be5c3f4f3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b08c314d50376e55d9825658aabc75385bbbe0be
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="introduction-to-using-xpath-queries-sqlxml-40"></a>Einführung in die Verwendung von XPath-Abfragen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XPath (XML Path Language)-Abfragen können als Teil einer URL oder in einer Vorlage angegeben werden. Das Zuordnungsschema bestimmt die Struktur des resultierenden Fragments, und die Werte werden aus der Datenbank abgerufen. Dieser Vorgang ähnelt prinzipiell dem Erstellen von Sichten mit der CREATE VIEW-Anweisung und dem Schreiben von SQL-Abfragen für diese Sichten.  
  
> [!NOTE]  
>  Um XPath-Abfragen in SQLXML 4.0 verstehen zu können, müssen Sie XML-Sichten und verwandte Konzepte wie Vorlagen und Zuordnungsschemas kennen. Weitere Informationen finden Sie unter [Einführung in XSD-Schemas mit Anmerkungen versehen &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md), und die vom World Wide Web Consortium (W3C) definierten Standard.  
  
 Ein XML-Dokument besteht aus Knoten, z. B. Elementknoten, Attributknoten, Textknoten usw. Betrachten Sie z. B. folgendes XML-Dokument:  
  
```  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was  
          very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
```  
  
 In diesem Dokument  **\<Kunden >** ist ein Elementknoten **Cid** wird ein Attributknoten und **"Important"** ein Textknoten.  
  
 XPath ist eine Diagrammnavigationssprache, die verwendet wird, um eine Gruppe von Knoten aus einem XML-Dokument auszuwählen. Jeder XPath-Operator wählt eine Knotengruppe aus, die auf einer von einem vorherigen XPath-Operator ausgewählten Knotengruppe basiert. Angenommen, eine Reihe von  **\<Kunden >** XPath-Knoten können auswählen, alle  **\<Reihenfolge >** Knoten mit der **Datum** -Attributwert **"7/14/1999"**. Die resultierende Knotengruppe enthält alle Bestellungen mit dem Bestelldatum 14.7.1999.  
  
 Die XPath-Sprache wurde vom World Wide Web Consortium (W3C) als Standardnavigationssprache definiert. SQLXML 4.0 implementiert eine Teilmenge der XPath-Spezifikation des W3C, die Sie unter der Adresse http://www.w3.org/TR/1999/PR-xpath-19991008.html finden.  
  
 Nachfolgend werden die Hauptunterschiede zwischen der XPath-Implementierung des W3C und der SQLXML 4.0-Implementierung beschrieben.  
  
-   **Abfragen des Stammelements**  
  
     In SQLXML 4.0 werden Abfragen des Stammelements (/) nicht unterstützt. Jede XPath-Abfrage muss auf einem der obersten Ebene beginnen  **\<ElementType >** im Schema.  
  
-   **Erstellen von Fehlerberichten**  
  
     Die XPath-Spezifikation des W3C definiert keine Fehlerbedingungen. XPath-Abfragen, die keine Knoten auswählen, geben eine leere Knotengruppe zurück. In SQLXML 4.0 kann eine Abfrage viele Arten von Fehlermeldungen zurückgeben.  
  
-   **Dokumentreihenfolge**  
  
     In SQLXML 4.0 ist die Dokumentreihenfolge nicht immer bestimmt. Aus diesem Grund, sich die numerische Prädikate und die Achsen, die Dokumentreihenfolge verwenden (z. B. **folgenden**) werden nicht implementiert.  
  
     Das Fehlen einer Dokumentreihenfolge bedeutet auch, dass der Zeichenfolgenwert eines Knotens nur dann ausgewertet werden kann, wenn der betreffende Knoten nur einer Spalte in nur einer Zeile zugeordnet werden kann. Ein Element mit untergeordneten Elementen oder einem IDREFS-Knoten oder NMTOKENS-Knoten kann nicht in eine Zeichenfolge konvertiert werden.  
  
    > [!NOTE]  
    >  In einigen Fällen die **Key-Felder** -Anmerkung oder Schlüssel aus der **Beziehung** Anmerkung kann in einer deterministischen Dokumentreihenfolge führen. Dies ist nicht der primäre Verwendungszweck dieser Anmerkungen Informationen jedoch finden Sie unter [Identifizieren von Schlüsselspalten mithilfe von SQL: Key-Felder &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md) und [angeben von Beziehungen mithilfe von SQL: Relationship &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md).  
  
-   **Datentypen**  
  
     SQLXML 4.0 weist Einschränkungen hinsichtlich der Implementierung der XPath- **Zeichenfolge**, **Anzahl**, und **booleschen** -Datentypen. Weitere Informationen finden Sie unter [XPath-Datentypen &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md).  
  
-   **Produktübergreifende Abfragen**  
  
     SQLXML 4.0 unterstützt keine produktübergreifende XPath-Abfragen wie `Customers[Order/@OrderDate=Order/@ShipDate]`. Mit dieser Abfrage werden alle Order-Datensätze aus der Datenbank Customers ausgewählt, bei denen der OrderDate-Wert dem ShipDate-Wert entspricht.  
  
     Allerdings unterstützt SQLXML 4.0 keine Abfragen wie `Customer[Order[@OrderDate=@ShippedDate]]`, mit der alle Customer-Datensätze ausgewählt werden, für die Order-Datensätze vorhanden sind, bei denen der OrderDate-Wert dem ShipDate-Wert entspricht.  
  
-   **Fehlerbehandlung und Sicherheit**  
  
     Je nachdem, welches Schema und welcher XPath-Abfrageausdruck verwendet werden, können [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler unter bestimmten Bedingungen für die Benutzer verfügbar gemacht werden.  
  
 Die Tabellen in den folgenden Abschnitten enthalten nähere Angaben dazu, in welcher Hinsicht sich die Implementierung von XPath-Abfragen in SQLXML 4.0 von der betreffenden W3C-Spezifikation unterscheidet.  
  
## <a name="supported-functionality"></a>Unterstützte Funktionalität  
 In der folgenden Tabelle werden die Funktionen der XPath-Sprache aufgeführt, die in SQLXML 4.0 implementiert sind.  
  
|Funktion|Element|Link zu Beispielabfragen|  
|-------------|----------|----------------------------|  
|Achsen|**Attribut**, **untergeordneten**, **übergeordneten**, und **self** Achsen|[Angeben von Achsen in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-axes-in-xpath-queries-sqlxml-4-0.md)|  
|Prädikate mit booleschen Werten einschließlich aufeinander folgender und geschachtelter Prädikate||[Angeben von arithmetischen Operatoren in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Alle relationalen Operatoren|=, !=, <, \<=, >, >=|[Angeben von relationalen Operatoren in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-relational-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Arithmetische Operatoren|+, -, *, div|[Angeben von arithmetischen Operatoren in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-arithmetic-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Explizite Konvertierungsfunktionen|**number()**, **string()**, **Boolean()**|[Angeben von expliziten Konvertierungsfunktionen in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-4-0.md)|  
|Boolesche Operatoren|AND, OR|[Angeben von booleschen Operatoren in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-operators-in-xpath-queries-sqlxml-4-0.md)|  
|Boolesche Funktionen|**true()**, **false()**, **not()**|[Angeben von booleschen Funktionen in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-boolean-functions-in-xpath-queries-sqlxml-4-0.md)|  
|XPath-Variablen||[Angeben von XPath-Variablen in XPath-Abfragen &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/specifying-xpath-variables-in-xpath-queries-sqlxml-4-0.md)|  
  
## <a name="unsupported-functionality"></a>Nicht unterstützte Funktionalität  
 In der folgenden Tabelle werden die Funktionen der XPath-Sprache aufgeführt, die in SQLXML 4.0 nicht implementiert sind.  
  
|Funktion|Element|  
|-------------|----------|  
|Achsen|**ancestor**, **ancestor-or-self**, **descendant**, **descendant-or-self (//)**, **following**, **following-sibling**, **namespace**, **preceding**, **preceding-sibling**|  
|Prädikate mit numerischen Werten||  
|Arithmetische Operatoren|mod|  
|Knotenfunktionen|**ancestor**, **ancestor-or-self**, **descendant**, **descendant-or-self (//)**, **following**, **following-sibling**, **namespace**, **preceding**, **preceding-sibling**|  
|Zeichenfolgenfunktionen|**string()**, **concat()**, **starts-with()**, **contains()**, **substring-before()**, **substring-after()**, **substring()**, **string-length()**, **normalize()**, **translate()**|  
|Boolesche Funktionen|**lang()**|  
|Numerische Funktionen|**sum()**, **floor()**, **ceiling()**, **round()**|  
|Union-operator|&#124;|  
  
 Bei der Angabe von XPath-Abfragen in einer Vorlage ist Folgendes zu beachten:  
  
-   XPath kann Zeichen wie < oder & enthalten, die in XML (und eine Vorlage ist ein XML-Dokument) eine spezielle Bedeutung haben. Sie müssen diese Zeichen mittels XML &-Codierung mit Escapezeichen versehen oder XPath in der URL angeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von XPath-Abfragen in SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
  
  
