---
title: Position-Funktion (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0c2bcb078026fc66fc3d783543a1a81edb9fb458
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="context-functions---position-xquery"></a>Kontextfunktionen - Position (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt einen ganzzahligen Wert zurück, der die Position des Kontextelements in der Sequenz der Elemente angibt, die derzeit verarbeitet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **Fn:Position()** kann nur im Kontext eines kontextabhängigen Prädikats verwendet werden. Die Funktion kann insbesondere nur innerhalb von eckigen Klammern ([ ]) verwendet werden. Das Vergleichen mit dieser Funktion verringert nicht die Kardinalität während des statischen Typrückschlusses.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** in Spalten vom Typ der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank.  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. Abrufen der ersten beiden Produktfunktionen mit der XQuery-Funktion position()  
 Die folgende Abfrage ruft die beiden ersten Funktionen, die ersten beiden untergeordneten Elemente des <`Features`>-Elements, aus der Produktmodell-Katalogbeschreibung ab. Wenn mehr Funktionen vorhanden sind, wird dem Ergebnis ein <`there-is-more/`>-Element hinzugefügt.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **Namespace** -Schlüsselwort in der [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md) definiert ein Namespacepräfix, das verwendet wird, im Hauptteil Abfrage.  
  
-   Der abfragehauptteil konstruiert XML, in dem ein \<Product >-Element mit **ProductModelID** und **ProductModelName** Attribute und dessen Produktfunktionen als untergeordnete Elemente zurückgegeben.  
  
-   Die **position()** Funktion wird im Prädikat verwendet, um zu bestimmen, der die Position des der \<Features > untergeordnetes Element im Kontext. Wenn es sich dabei um die erste oder zweite Funktion handelt, wird diese zurückgegeben.  
  
-   Die IF-Anweisung fügt eine \<dort-is-More / >-Element auf das Ergebnis, wenn mehr als zwei Funktionen im Produktkatalog vorhanden sind.  
  
-   Da nicht für alle Produktmodelle Katalogbeschreibungen in der Tabelle gespeichert sind, wird die WHERE-Klausel zum Verwerfen von Zeilen verwendet, in denen CatalogDescriptions den Wert NULL besitzt.  
  
 Dies ist ein Teilergebnis:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
…  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
