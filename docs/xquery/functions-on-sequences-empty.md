---
title: leer-Funktion (XQuery) | Microsoft Docs
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
- empty function
- fn:empty function
ms.assetid: 46da89a8-0cd9-4913-8521-4087589a04ba
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ca580d89bf60046aaf2d02315f18b12772e0bea
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-sequences---empty"></a>Funktionen für Sequenzen - leer
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt "true" zurück, wenn der Wert der *$arg* ist eine leere Sequenz. Andernfalls gibt die Funktion False zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:empty($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Eine Sequenz aus Elementen. Falls die Sequenz leer ist, gibt die Funktion True zurück. Andernfalls gibt die Funktion False zurück.  
  
## <a name="remarks"></a>Hinweise  
 Die **Fn:Exists()** Funktion wird nicht unterstützt. Alternativ können die **"NOT()" "** -Funktion kann verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-empty-xquery-function-to-determine-if-an-attribute-is-present"></a>A. Verwenden der empty() XQuery-Funktion zum Bestimmen, ob ein Attribut vorhanden ist  
 Im Herstellungsvorgang für Produktmodell 7, gibt diese Abfrage alle arbeitsplatzstandorte, auf denen keine **MachineHours** Attribut.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in /AWMI:root/AWMI:Location[empty(@MachineHours)]  
     return  
       <Location  
            LocationID="{ ($i/@LocationID) }"  
            LaborHrs="{ ($i/@LaborHours) }" >  
            {   
              $i/@MachineHours  
            }    
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID      Result          
-------------- ------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
 Die folgende, leicht geänderte Abfrage gibt "NotFound" zurück, wenn die **MachineHour** -Attribut nicht vorhanden ist:  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace p14="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in /p14:root/p14:Location  
     return  
       <Location  
            LocationID="{ ($i/@LocationID) }"  
            LaborHrs="{ ($i/@LaborHours) }" >  
            {   
                 if (empty($i/@MachineHours)) then  
                    attribute MachineHours { "NotFound" }  
                 else  
                    attribute MachineHours { data($i/@MachineHours) }  
            }    
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID Result                         
-------------- -----------------------------------  
7                
  <Location LocationID="10" LaborHrs="2.5" MachineHours="3"/>  
  <Location LocationID="20" LaborHrs="1.75" MachineHours="2"/>  
  <Location LocationID="30" LaborHrs="1" MachineHours="NotFound"/>  
  <Location LocationID="45" LaborHrs="0.5" MachineHours="0.65"/>  
  <Location LocationID="50" LaborHrs="3" MachineHours="NotFound"/>  
  <Location LocationID="60" LaborHrs="4" MachineHours="NotFound"/>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Funktionen für den Xml-Datentyp](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [vorhanden &#40; &#41; -Methode &#40; Xml-Datentyp &#41;](../t-sql/xml/exist-method-xml-data-type.md)  
  
  

