---
title: NOT-Funktion (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
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
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 339e25e304b85fef9dc1401d750dfe2b41cb0287
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-boolean-values---not-function"></a>Funktionen für boolesche Werte - not-Funktion 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt "true" zurück, wenn der effektive boolesche Wert der *$arg* lautet "false" und "false" zurückgegeben, wenn der effektive boolesche Wert der *$arg* ist "true".  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Eine Elementsequenz, für die es einen effektiven booleschen Wert gibt.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. Verwenden der NOT()-XQuery-Funktion zum Suchen von Produktmodellen, deren katalogbeschreibungen enthalten nicht die \<Spezifikationen > Element.  
 Die folgende Abfrage erstellt XML mit den IDs von Produktmodellen, deren Katalogbeschreibung das <`Specifications`>-Element nicht enthält.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Da das Dokument Namespaces verwendet, wird in diesem Beispiel die WITH NAMESPACES-Anweisung verwendet. Eine andere Möglichkeit ist die Verwendung der **Namespace deklarieren** -Schlüsselwort in der [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md) um das Präfix zu definieren.  
  
-   Anschließend konstruiert die Abfrage der XML mit der <`Product`>-Element und dessen **ProductModelID** Attribut.  
  
-   Die WHERE-Klausel verwendet die [EXIST()-Methode (XML-Datentyp)](../t-sql/xml/exist-method-xml-data-type.md) zum Filtern der Zeilen. Die **exist()** -Methode gibt True zurück, wenn es sind \<ProductDescription >-Elemente, die keine \<Spezifikation > untergeordnete Elemente. Beachten Sie die Verwendung der **"NOT()" "** Funktion.  
  
 Dieses Resultset ist leer, da jedes Produktmodell-katalogbeschreibung enthält die \<Spezifikationen > Element.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. Abrufen von Arbeitsplatzstandorten ohne MachineHours-Attribut mit der XQuery-Funktion not()  
 Die folgende Abfrage wird beispielsweise für die Instructions-Spalte angegeben. Diese Spalte speichert Anweisungen zur Fertigung der Produktmodelle.  
  
 Die Abfrage ruft Arbeitsplatzstandorte, für die kein MachineHours-Attribut angegeben ist, für ein bestimmtes Produktmodell ab. D. h. das Attribut **MachineHours** ist nicht angegeben, für die \<Speicherort > Element.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 Beachten Sie in der vorherigen Abfrage Folgendes:  
  
-   Die **Declarenamespace** in [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md) definiert das Namespacepräfix der fertigungsanweisungen in Adventure Works. Dieser Namespace ist mit dem in dem Fertigungsanweisungsdokument verwendeten identisch.  
  
-   In der Abfrage die **nicht (@MachineHours)** -Prädikat True zurück, wenn es ist keine **MachineHours** Attribut.  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **"NOT()" "** Funktion unterstützt nur Argumente vom Typ xs: Boolean, node() *, oder die leere Sequenz.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
