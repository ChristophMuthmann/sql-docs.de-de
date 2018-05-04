---
title: XQuery-Abfragen, die die Reihenfolge | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sequence [XQuery]
- XQuery, sequence
- ordered expressions [XQuery]
ms.assetid: 4f1266c5-93d7-402d-94ed-43f69494c04b
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 517bdd257f5631f55422d685418db2d10284d9e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xqueries-involving-order"></a>XQuery-Abfragen, die die Reihenfolge berücksichtigen
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In relationalen Datenbanken spielt die Reihenfolge keine Rolle. Sie können z. B. keine Anforderung wie etwa "Ersten Kunden aus der Datenbank abrufen" erstellen. Sie können jedoch ein XML-Dokument Abfragen und Abrufen der ersten \<Customer > Element. In diesem Fall wird immer der gleiche Kunde abgerufen.  
  
 Dieses Thema stellt Abfragen vor, die auf der Reihenfolge basieren, in der Knoten im Dokument vorhanden sind.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-retrieve-manufacturing-steps-at-the-second-work-center-location-for-a-product"></a>A. Abrufen von Herstellungsschritten am zweiten Arbeitsplatzstandort für ein Produkt  
 Die folgende Abfrage ruft die Fertigungsschritte für ein bestimmtes Produktmodell an einem zweiten Arbeitsplatzstandort in einer Abfolge von Arbeitsplatzstandorten im Fertigungsprozess ab.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    <ManuStep ProdModelID = "{sql:column("Production.ProductModel.ProductModelID")}"  
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
     <Location>  
       { (//AWMI:root/AWMI:Location)[2]/@* }  
       <Steps>  
         { for $s in (//AWMI:root/AWMI:Location)[2]//AWMI:step  
           return  
              <Step>  
               { string($s) }  
              </Step>  
         }  
        </Steps>  
      </Location>  
     </ManuStep>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die Ausdrücke in den geschweiften Klammern werden durch das Ergebnis der Auswertung ersetzt. Weitere Informationen finden Sie unter [XML-Konstruktion &#40;XQuery&#41;](../xquery/xml-construction-xquery.md).  
  
-   **@\*** Ruft alle Attribute des zweiten arbeitsplatzstandort ab.  
  
-   Die FLWOR-Iteration (FOR ... EINGABETASTE) ruft alle untergeordneten <`step`>-Elemente am zweiten Arbeitsplatzstandort ab.  
  
-   Die [SQL:Column()-Funktion (XQuery)](../xquery/xquery-extension-functions-sql-column.md) enthält den relationalen Wert in der XML, das erstellt wird.  
  
 Dies ist das Ergebnis:  
  
```  
<ManuStep ProdModelID="7" ProductModelName="HL Touring Frame">  
  <Location LocationID="20" SetupHours="0.15"   
              MachineHours="2"  LaborHours="1.75" LotSize="1">  
  <Steps>  
   <Step>Assemble all frame components following blueprint 1299.</Step>  
     …  
  </Steps>  
 </Location>  
</ManuStep>    
```  
  
 Die vorherige Abfrage ruft nur die Textknoten ab. Wenn Sie möchten, dass die gesamte <`step`> Entfernen Sie das Element stattdessen zurückgegeben der **string()** Funktion aus der Abfrage:  
  
### <a name="b-find-all-the-material-and-tools-used-at-the-second-work-center-location-in-the-manufacturing-of-a-product"></a>B. Suchen aller Materialen und Werkzeuge, die am zweiten Arbeitsplatzstandort zur Fertigung eines Produkts verwendet werden  
 Die folgende Abfrage ruft die Materialien und Werkzeuge für ein bestimmtes Produktmodell an einem zweiten Arbeitsplatzstandort in der Abfolge von Arbeitsplatzstandorten im Fertigungsprozess ab.  
  
```  
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <Location>  
      { (//AWMI:root/AWMI:Location)[1]/@* }  
       <Tools>  
         { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:tool  
           return  
              <Tool>  
                { string($s) }  
              </Tool>  
          }  
        </Tools>  
        <Materials>  
            { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:material  
              return  
                 <Material>  
                    { string($s) }  
                 </Material>  
             }  
         </Materials>  
  </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die Abfrage erstellt das <Loca`tion`>-Element und ruft seine Attributwerte aus der Datenbank ab.  
  
-   Sie verwendet zwei FLWOR (for...return)-Iterationen: eine Iteration zum Abrufen der Werkzeuge und eine zweite Iteration zum Abrufen der verwendeten Materialien.  
  
 Dies ist das Ergebnis:  
  
```  
<Location LocationID="10" SetupHours=".5"   
          MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
    <Tool>router with a carbide tip 15</Tool>  
    <Tool>Forming Tool FT-15</Tool>  
  </Tools>  
  <Materials>  
    <Material>aluminum sheet MS-2341</Material>  
  </Materials>  
</Location>  
```  
  
### <a name="c-retrieve-the-first-two-product-feature-descriptions-from-the-product-catalog"></a>C. Abrufen der ersten beiden Produktfunktionsbeschreibungen aus dem Produktkatalog  
 Die Abfrage ruft die ersten beiden Funktionsbeschreibungen für ein bestimmtes Produktmodell aus dem <`Features`>-Element im Produktmodellkatalog ab.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <ProductModel ProductModelID= "{ data( (/p1:ProductDescription/@ProductModelID)[1] ) }"  
                   ProductModelName = "{ data( (/p1:ProductDescription/@ProductModelName)[1] ) }" >  
       {  
         for $F in /p1:ProductDescription/p1:Features  
         return   
           $F/*[position() <= 2]   
       }  
     </ProductModel>  
      ') as x  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
 Der Abfragetext erstellt XML mit dem <`ProductModel`>-Element, das das ProductModelID-Attribut und das ProductModelName-Attribut enthält.  
  
-   Die Abfrage verwendet eine FOR ... RETURN-Schleife zum Abrufen der Produktmodell-Funktionsbeschreibungen. Die **position()** Funktion wird verwendet, um die ersten beiden Funktionen abzurufen.  
  
 Dies ist das Ergebnis:  
  
```  
<ProductModel ProductModelID="19" ProductModelName="Mountain 100">  
 <p1:Warranty   
  xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
  <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
 <p2:Maintenance   
  xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p2:NoOfYears>10</p2:NoOfYears>  
  <p2:Description>maintenance contact available through your dealer   
            or any AdventureWorks retail store.  
  </p2:Description>  
 </p2:Maintenance>  
</ProductModel>   
```  
  
### <a name="d-find-the-first-two-tools-used-at-the-first-work-center-location-in-the-manufacturing-process-of-the-product"></a>D. Suchen der ersten beiden Werkzeuge, die am ersten Arbeitsplatzstandort zur Herstellung des Produkts verwendet werden  
 Die folgende Abfrage gibt die ersten beiden Werkzeuge für ein Produktmodell zurück, die am ersten Arbeitsplatzstandort in der Abfolge von Arbeitsplatzstandorten im Fertigungsprozess verwendet werden. Die Abfrage wird angegeben, für die produktionsanweisungen, gespeichert der **Anweisungen** Spalte die **Production.ProductModel** Tabelle.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   for $Inst in (//AWMI:root/AWMI:Location)[1]  
   return   
     <Location>  
       { $Inst/@* }  
       <Tools>  
         { for $s in ($Inst//AWMI:step//AWMI:tool)[position() <= 2]  
           return  
             <Tool>  
               { string($s) }  
             </Tool>  
         }  
       </Tools>  
     </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Location LocationID="10" SetupHours=".5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
  </Tools>  
</Location>   
```  
  
### <a name="e-find-the-last-two-manufacturing-steps-at-the-first-work-center-location-in-the-manufacturing-of-a-specific-product"></a>E. Suchen der letzten zwei Herstellungsschritte am ersten Arbeitsplatzstandort zur Fertigung eines bestimmten Produkts  
 Die Abfrage verwendet die **last()** Funktion zum Abrufen der letzten beiden Fertigungsschritte.  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
<LastTwoManuSteps>  
   <Last-1Step>When finished, inspect the forms for defects per   
               Inspection Specification .</Last-1Step>  
   <LastStep>Remove the frames from the tool and place them in the   
             Completed or Rejected bin as appropriate.</LastStep>  
</LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML-Konstruktion &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
