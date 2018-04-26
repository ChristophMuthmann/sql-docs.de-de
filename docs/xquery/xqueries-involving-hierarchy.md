---
title: XQuery-Abfragen im Zusammenhang mit Hierarchie | Microsoft Docs
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
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f485b974ceaac492f8dc611dd2fe0c139426139
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="xqueries-involving-hierarchy"></a>XQuery-Abfragen unter Einbeziehung von Hierarchien
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die meisten **Xml** in Spalten vom Typ der **AdventureWorks** -Datenbank sind halbstrukturierte Dokumente. Deshalb können die in jeder Zeile gespeicherten Dokumente unterschiedlich aussehen. Die in diesem Thema gezeigten Abfragebeispiele veranschaulichen, wie Informationen aus diesen unterschiedlichen Dokumenten extrahiert werden können.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. Abrufen von Arbeitsplatzstandorten mit dem zugehörigen ersten Fertigungsschritt aus Dokumenten mit Produktionsanweisungen  
 Für Produktmodell 7, die Abfrage erstellt XML mit der <`ManuInstr`>-Element mit **ProductModelID** und **ProductModelName** Attribute, und eine oder mehrere <`Location`> untergeordnete Elemente.  
  
 Jedes <`Location`>-Element verfügt über einen eigenen Satz von Attributen sowie ein untergeordnetes <`step`>-Element. Das untergeordnete <`step`>-Element stellt den ersten Fertigungsschritt am Arbeitsplatzstandort dar.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **Namespace** -Schlüsselwort in der [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md) definiert ein Namespacepräfix. Dieses Präfix wirt später im Body-Teil der Abfrage verwendet.  
  
-   Die Tokens zum Kontextwechsel, {) und (}, bewirken das Wechseln der Abfrage von der XML-Konstruktion zur Abfrageauswertung.  
  
-   Die **SQL:Column()** wird verwendet, um einen relationalen Wert in der XML einzuschließen, das erstellt wird.  
  
-   Beim Erstellen des <`Location`>-Elements werden alle Attribute für den Arbeitsplatzstandort von $wc/@* abgerufen.  
  
-   Die **string()** Funktion gibt den String-Wert aus der <`step`> Element.  
  
 Dies ist ein Teilergebnis:  
  
```  
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. Suchen aller Telefonnummern in der AdditionalContactInfo-Spalte  
 Die folgende Abfrage ruft zusätzliche Telefonnummern für einen bestimmten Kundenkontakt ab, indem die gesamte Hierarchie nach dem <`telephoneNumber`>-Element durchsucht wird. Da das <`telephoneNumber`>-Element an einer beliebigen Stelle in der Hierarchie angezeigt werden kann, verwendet die Abfrage den descendant- und den self-Operator (//) in der Suche.  
  
```  
SELECT AdditionalContactInfo.query('  
 declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 Dies ist das Ergebnis:  
  
```  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 Um nur die Telefonnummern der obersten Ebene abzurufen, insbesondere die untergeordneten <`telephoneNumber`>-Elemente von <`AdditionalContactInfo`>, wird der FOR-Ausdruck in der Abfrage wie folgt geändert:  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`installiert haben.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Grundlagen](../xquery/xquery-basics.md)   
 [XML-Konstruktion &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
