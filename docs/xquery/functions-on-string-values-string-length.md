---
title: String-Length-Funktion (XQuery) | Microsoft Docs
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
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a01221907acd777eaaf41ca77d73bf561724c96c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-string-values---string-length"></a>Funktionen für Zeichenfolgenwerte - String-length-Funktion
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Länge der Zeichenfolge in Zeichen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Quellzeichenfolge, deren Länge berechnet werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert der *$arg* ist eine leere Sequenz ein **xs: Integer** wird der Wert 0 zurückgegeben.  
  
 Das Verhalten von Ersatzpaaren in XQuery-Funktionen hängt vom Kompatibilitätsgrad der Datenbank ab. Beim Kompatibilitätsgrad 110 oder höher wird jedes Ersatzpaar als einzelnes Zeichen gezählt. Bei niedrigeren Kompatibilitätsgraden werden Ersatzpaare als zwei Zeichen betrachtet. Weitere Informationen finden Sie unter [ALTER DATABASE Kompatibilitätsgrad &#40; Transact-SQL &#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) und [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
 Wenn der Wert ein 4-Byte-Unicode-Zeichen enthält, das durch zwei Ersatzzeichen dargestellt wird, zählt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Ersatzzeichen einzeln.  
  
 Die **string-length()** ohne ein Parameter nur in einem Prädikat verwendet werden kann. Beispielsweise gibt die folgende Abfrage das <`ROOT`>-Element zurück:  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Das Verhalten von Ersatzzeichenpaaren in XQuery-Funktionen hängt vom Kompatibilitätsgrad der Datenbank ab und in einigen Fällen vom Standardnamespace-URI für Funktionen. Weitere Informationen finden Sie im Abschnitt "XQuery-Funktionen sind Ersatzzeichenabhängig" im Thema [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Siehe auch [ALTER DATABASE Kompatibilitätsgrad &#40; Transact-SQL &#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) und [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen in verschiedenen gespeicherten **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. Verwenden der string-length()-Funktion von XQuery zum Abrufen von Produkten mit langen Zusammenfassungsbeschreibungen  
 Für Produkte, deren Zusammenfassungsbeschreibung größer als 50 Zeichen ist, ruft die folgende Abfrage die Produkt-ID, die Länge der Zusammenfassungsbeschreibung sowie die Zusammenfassung selbst (das <`Summary`>-Element) ab.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die Bedingung in der WHERE-Klausel ruft nur die Zeilen ab, für die die im XML-Dokument gespeicherte Zusammenfassung länger als 200 Zeichen ist. Er verwendet die [Value()-Methode (XML-Datentyp)](../t-sql/xml/value-method-xml-data-type.md).  
  
-   Die SELECT-Klausel erstellt nur das von Ihnen gewünschte XML. Er verwendet die [Query()-Methode (XML-Datentyp)](../t-sql/xml/query-method-xml-data-type.md) zum Erstellen des XMLS, und geben Sie die erforderlichen XQuery-Ausdrucks zum Abrufen von Daten aus dem XML-Dokument.  
  
 Dies ist ein Teilergebnis:  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>B. Verwenden der string-length()-Funktion von XQuery zum Abrufen von Produkten, deren Garantiebeschreibungen kurz sind  
 Für Produkte, deren Garantiebeschreibung weniger als 20 Zeichen lang ist, ruft die folgende Abfrage XML ab, das die Produkt-ID, die Länge, die Garantiebeschreibung und das <`Warranty`>-Element selbst enthält.  
  
 Die Garantie ist eine der Produktfunktionen. Ein optionales untergeordnetes <`Warranty`>-Element folgt nach dem <`Features`>-Element.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   **pD** und **Wm** die Namespacepräfixe in dieser Abfrage verwendet werden. Sie geben den gleichen Namespace an, der in dem Dokument verwendet wird, das abgefragt wird.  
  
-   Die XQuery gibt eine geschachtelte FOR-Schleife an. Die äußere FOR-Schleife ist erforderlich, da Sie abrufen möchten die **ProductModelID** Attribute von der <`ProductDescription`> Element. Die innere FOR-Schleife ist erforderlich, weil Sie nur die Produkte abrufen möchten, die Garantiefunktionsbeschreibungen besitzen, die kürzer als 20 Zeichen sind.  
  
 Dies ist das Teilergebnis:  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
