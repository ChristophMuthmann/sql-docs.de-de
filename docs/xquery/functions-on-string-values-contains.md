---
title: Contains-Funktion (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
caps.latest.revision: 42
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e7c23a4c4eb886ea0cd9434d970410376991f35b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-string-values---contains"></a>Funktionen für Zeichenfolgenwerte - enthält
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt einen Wert des Typs xs: Boolean, der angibt, ob der Wert der *$arg1* enthält einen Zeichenfolgenwert, der gemäß *$arg2*.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg1*  
 Zu testender Zeichenfolgenwert.  
  
 *$arg2*  
 Abzurufende Unterzeichenfolge.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert der *$arg2* ist eine Zeichenfolge der Länge 0 (null), gibt die Funktion **"true"**. Wenn der Wert der *$arg1* ist eine Zeichenfolge der Länge 0 (null) und der Wert der *$arg2* ist eine Zeichenfolge der Länge 0 (null), gibt die Funktion **"false"**.  
  
 Wenn der Wert der *$arg1* oder *$arg2* ist die leere Sequenz ist, wird das Argument als die Zeichenfolge der Länge 0 (null) behandelt.  
  
 Die contains()-Funktion verwendet die Unicode-Codepunkt-Standardsortierung von XQuery für den Zeichenfolgenvergleich.  
  
 Für die angegebene Unterzeichenfolgenwert *$arg2* muss kleiner oder gleich 4000 Zeichen sein. Wenn der angegebene Wert größer als 4000 Zeichen ist, tritt eine dynamische fehlerbedingung auf, und die Contains()-Funktion gibt eine leere Sequenz statt eines booleschen Werts von **"true"** oder **"false"**. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] löst keine dynamischen Fehler bei XQuery-Ausdrücken aus.  
  
 Um die Groß-/Kleinschreibung Vergleiche, die [Großbuchstaben](../xquery/functions-on-string-values-upper-case.md) oder lower-case-Funktionen verwendet werden können.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Das Verhalten von Ersatzzeichenpaaren in XQuery-Funktionen hängt vom Kompatibilitätsgrad der Datenbank ab und in einigen Fällen vom Standardnamespace-URI für Funktionen. Weitere Informationen finden Sie im Abschnitt "XQuery-Funktionen sind Ersatzzeichenabhängig" im Thema [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Siehe auch [ALTER DATABASE Kompatibilitätsgrad &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) und [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen in verschiedenen Xml-Datentyp-Spalten in der AdventureWorks-Datenbank gespeichert.  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>A. Verwenden der contains()-Funktion von XQuery zum Suchen nach einer bestimmten Zeichenfolge  
 Die folgende Abfrage sucht nach Produkten, die das Wort Aerodynamic in den Zusammenfassungsbeschreibungen enthalten. Die Abfrage gibt ProductID und das <`Summary`>-Element für derartige Produkte zurück.  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
   /pd:ProductDescription/pd:Summary//text()  
    [contains(., "Aerodynamic")]') = 1  
```  
  
 Ergebnisse  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `28     <Prod ProductModelID="28">`  
  
 `<pd:Summary xmlns:pd=`  
  
 `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
