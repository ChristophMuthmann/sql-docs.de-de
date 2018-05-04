---
title: Count-Funktion (XQuery) | Microsoft Docs
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
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a4736bae163e427d98c4c7e21f13cc957d91187f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="aggregate-functions---count"></a>Aggregatfunktionen - Anzahl
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl der enthaltenen Elemente in der angegebenen Sequenz *$arg*.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Zu zählende Elemente.  
  
## <a name="remarks"></a>Hinweise  
 Gibt 0 zurück, wenn *$arg* ist eine leere Sequenz.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. Verwenden der count()-Funktion von XQuery zum Zählen der Arbeitsplatzstandorte im Fertigungsprozess eines Produktmodells  
 Die folgende Abfrage zählt die Anzahl der Arbeitsplatzstandorte im Fertigungsprozess eines Produktmodells (ProductModelID=7).  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **Namespace** -Schlüsselwort in [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md) definiert ein Namespacepräfix. Dieses Präfix wird anschließend im Hauptteil der XQuery verwendet.  
  
-   Die Abfrage erstellt XML mit dem <`NoOfWorkStations`>-Element.  
  
-   Die **count()** -Funktion im Hauptteil der XQuery zählt die Anzahl der <`Location`> Elemente.  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 Sie können den XML-Code auch so konstruieren, dass er die ID und den Namen des Produktmodells enthält, wie in der folgenden Abfrage gezeigt:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 Dies ist das Ergebnis:  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 Anstelle von XML können Sie die Werte auch so zurückgeben, dass sie nicht vom Typ XML sind, wie in der folgenden Abfrage gezeigt. Die Abfrage verwendet die [Value()-Methode (Xml-Datentyp)](../t-sql/xml/value-method-xml-data-type.md) die Anzahl der Arbeitsaufgaben Center Speicherort abgerufen.  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
