---
title: SUM-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ae0eacebba36dd75537a36cfaf0ce46ba43f332
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions---sum"></a>Aggregatfunktionen – Summe
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Summe einer Sequenz von Zahlen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Sequenz aus atomaren Werten, deren Summe berechnet werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Alle Typen der atomaren Werte, die übergeben werden **sum()** müssen Untertypen des gleichen Basistyps sein. Zu den akzeptierten Basistypen zählen die drei integrierten numerischen Basistypen oder xdt:untypedAtomic. Werte des Typs xdt:untypedAtomic werden in xs:double umgewandelt. Wenn eine Mischung dieser Typen ist, oder wenn andere Werte anderer Typen übergeben werden, wird ein statischer Fehler ausgelöst.  
  
 Das Ergebnis des **sum()** erhält den Basistyp der übergebenen Typen, z. B. xs: Double im Fall von xdt: UntypedAtomic, selbst wenn die Eingabe optional die leere Sequenz ist. Wenn die Eingabe statisch leer ist, ist das Ergebnis 0 mit dem statischen und dynamischen Typ xs:integer.  
  
 Die **sum()** Funktion gibt die Summe der numerischen Werte zurück. Wenn ein xdt: UntypedAtomic-Wert in xs: Double umgewandelt werden kann, wird der Wert in der Eingabesequenz ignoriert *$arg*. Wenn die Eingabe eine dynamisch berechnete leere Sequenz ist, wird der Wert 0 des verwendeten Basistyps zurückgegeben.  
  
 Die Funktion gibt einen Laufzeitfehler zurück, wenn ein Ausnahmefehler wegen Überlauf oder Verstoß gegen den Gültigkeitsbereich auftritt.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** in Spalten vom Typ der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank.  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>A. Ermitteln der kombinierten Gesamtanzahl der Arbeitsstunden für alle Arbeitsplatzstandorte im Produktionsprozess mit der XQuery-Funktion sum()  
 Die folgende Abfrage sucht nach der Gesamtanzahl der Arbeitsstunden für alle Arbeitsplatzstandorte im Produktionsprozess aller Produktmodelle, für die Produktionsanweisungen gespeichert sind.  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 Dies ist das Teilergebnis.  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 Die Abfrage kann auch so geschrieben werden, dass das Resultset nicht als XML-Code zurückgegeben wird, sondern dass relationale Ergebnisse generiert werden, wie das in der folgenden Abfrage gezeigt wird:  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 Dies ist ein Teilergebnis:  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Nur die einzelargumentversion von **sum()** wird unterstützt.  
  
-   Wenn die Eingabe eine dynamisch berechnete leere Sequenz ist, wird statt des Typs xs:integer der Wert 0 des verwendeten Basistyps zurückgegeben.  
  
-   Die **sum()** -Funktion ordnet alle ganzzahligen Werte xs: Decimal.  
  
-   Die **sum()** -Funktion für Werte des Typs xs: Duration nicht unterstützt.  
  
-   Sequenzen, die Typen über Basistypbegrenzungen hinweg mischen, werden nicht unterstützt.  
  
-   Der Code sum((xs:double(“INF”), xs:double(“-INF”))) löst einen Domänenfehler aus.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

