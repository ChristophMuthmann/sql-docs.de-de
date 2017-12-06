---
title: Konstruktorfunktionen (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords: constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7592e3880cf0248efef68f7c49133ca869bce3c8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="constructor-functions-xquery"></a>Konstruktorfunktionen (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die Konstruktorfunktionen erstellen Instanzen beliebiger integrierter oder benutzerdefinierter atomarer XSD-Typen aus den angegebenen Eingaben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>Argumente  
 *$strval*  
 Zu konvertierende Zeichenfolge.  
  
 *KONFIGURATIONSELEMENTTYP*  
 Ein beliebiger integrierter XSD-Typ.  
  
## <a name="remarks"></a>Hinweise  
 Konstruktoren werden von atomaren XSD-Basistypen sowie abgeleiteten Typen unterstützt. Allerdings die Untertypen von **xs: Duration**, darunter **xdt: yearmonthduration und xdt: dayTimeDuration**, und **xs: QName**, **xs: NMTOKEN**, und **xs** werden nicht unterstützt. Die benutzerdefinierten atomaren Typen, die in den damit verbundenen Schemaauflistungen verfügbar sind, stehen auch hier zur Verfügung, unter der Voraussetzung, dass sie direkt oder indirekt aus den folgenden Typen abgeleitet sind.  
  
#### <a name="supported-base-types"></a>Unterstützte Basistypen  
 Es folgen die unterstützten Basistypen:  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>Unterstützte abgeleitete Typen  
 Es folgen die unterstützten abgeleiteten Typen:  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 SQL Server unterstützt außerdem die Reduktion konstanter Ausdrücke beim Aufrufen von Konstruktorfunktionen unter folgenden Bedingungen:  
  
-   Wenn das Argument ein Zeichenfolgenliteral ist, wird der Ausdruck zur Kompilierzeit ausgewertet. Wenn der Wert die Typeinschränkungen nicht erfüllt, wird ein statischer Fehler ausgelöst.  
  
-   Wenn das Argument ein Literal eines anderen Typs ist, wird der Ausdruck zur Kompilierzeit ausgewertet. Wenn der Wert die Typeinschränkungen nicht erfüllt, wird die leere Sequenz zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. Abrufen älterer Produktbeschreibungen mit der dateTime()-Funktion von XQuery  
 In diesem Beispiel wird ein XML-Beispieldokument zunächst auf zugewiesen ein **Xml** Typvariablen. Dieses Dokument enthält drei <`ProductDescription`>-Beispielelemente, die jeweils ein untergeordnetes <`DateCreated`>-Element enthalten.  
  
 Die Variable wird dann abgefragt, um nur diejenigen Produktbeschreibungen abzurufen, die vor einem bestimmten Datum erstellt worden sind. Für Vergleichszwecke verwendet die Abfrage die **xs:DateTime()** Konstruktorfunktion, um die Datumsangaben eingeben.  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die FOR ... WHERE-Schleifenstruktur zum Abrufen der \<ProductDescription >-Element in der WHERE-Klausel angegebene Bedingung erfüllt.  
  
-   Die **dateTime()** Konstruktorfunktion wird verwendet, um erstellen **"DateTime"** Geben Sie Werte aus, damit diese ordnungsgemäß verglichen werden können.  
  
-   Anschließend konstruiert die Abfrage die resultierende XML-Ausgabe: Nachdem dabei eine Reihe von Attributen konstruiert wird, werden in der XML-Konstruktion Kommas und Klammern verwendet.  
  
 Dies ist das Ergebnis:  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Konstruktion &#40; XQuery &#41;](../xquery/xml-construction-xquery.md)   
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
