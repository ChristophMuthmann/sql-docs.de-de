---
title: CEILING-Funktion (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c706be1d79119a28f86a389e82e42416b0b3b552
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="numeric-values-functions---ceiling"></a>Numerische Werte Funktionen - ceiling 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die kleinste Anzahl ohne Stellen hinter dem Dezimalpunkt zurück, die nicht geringer ist als der Wert des Funktionsarguments. Wenn das Argument eine leere Sequenz ist, wird die leere Sequenz zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Anzahl, auf die die Funktion angewendet wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Typ des *$arg* ist einer der drei numerischen Basistypen **xs: float**, **xs: double**, oder **xs: decimal**, der Rückgabetyp ist identisch mit die *$arg* Typ.  
  
 Wenn der Typ des *$arg* ist ein Typ, der einen der numerischen Typen abgeleitet ist der Rückgabetyp ist der numerische Basistyp.  
  
 Wenn die Eingabe für die Funktionen Fn: Floor, Fn: CEILING oder Fn: Round ist **xdt: UntypedAtomic**, er wird implizit umgewandelt in **xs: double**.  
  
 Alle anderen Typen führen zum Generieren eines statischen Fehlers.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. Verwenden der XQuery-Funktion ceiling()  
 Für Produktmodell 7 gibt die Abfrage eine Liste der Arbeitsplatzstandorte im Produktionsprozess des Produktmodells zurück. Für jeden einzelnen Arbeitsplatzstandort gibt die Abfrage die Standortkennung, die Arbeitsstunden sowie die Losgröße zurück, sofern diese dokumentiert ist. Die Abfrage verwendet die **Ceiling** -Funktion die Arbeitsstunden als Werte des Typs zurückgibt **decimal**.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Das AWMI-Namespacepräfix steht für Adventure Works Manufacturing Instructions. Dieses Präfix verweist auf denselben Namespace, der im abgefragten Dokument verwendet wird.  
  
-   **Anweisungen** ist ein **Xml** Typspalte. Aus diesem Grund die [Query()-Methode (XML-Datentyp)](../t-sql/xml/query-method-xml-data-type.md) wird zum Angeben der XQuery verwendet. Die XQuery-Anweisung wird als Argument der query-Methode angegeben.  
  
-   **für... zurückgeben** ist eine Schleifenkonstruktion. In der Abfrage die **für** Schleife gibt eine Liste mit \<Speicherort > Elemente. Für jeden einzelnen arbeitsplatzstandort der **zurückgeben** -Anweisung in der **für** Schleife beschreibt die XML generiert werden:  
  
    -   Ein \<Speicherort >-Element mit LocationId- und ein LaborHrs-Attribut. Der entsprechende Ausdruck in den geschweiften Klammern ({ }) ruft die erforderlichen Werte aus dem Dokument ab.  
  
    -   Der {$i/@LotSize } Ausdruck ruft das LotSize-Attribut aus dem Dokument ab, falls vorhanden.  
  
    -   Dies ist das Ergebnis:  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **ceiling()** -Funktion ordnet alle ganzzahligen Werte xs: Decimal.  
  
## <a name="see-also"></a>Siehe auch  
 [Floor-Funktion &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [Round-Funktion &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
