---
title: Handhabung von Namespaces in XQuery | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 285277ec57e10d23e1c5dc4c322dbba57a5d793e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="handling-namespaces-in-xquery"></a>Handhabung von Namespaces in XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dieses Thema bietet Beispiele für die Handhabung von Namespaces in Abfragen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-declaring-a-namespace"></a>A. Deklarieren eines Namespaces  
 Die folgende Abfrage ruft die Produktionsschritte eines bestimmten Produktmodells ab.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
…  
```  
  
 Beachten Sie, dass die **Namespace** Schlüsselwort wird verwendet, um ein neues Namespacepräfix zu definieren "AWMI:". Dieses Präfix muss dann in der Abfrage für alle Elemente verwendet werden, die in diesem Namespace liegen.  
  
### <a name="b-declaring-a-default-namespace"></a>B. Deklarieren eines Standardnamespaces  
 In der vorherigen Abfrage wurde ein neues Namespacepräfix definiert. Dieses Präfix musste dann in der Abfrage verwendet werden, um die gesuchten XML-Strukturen auszuwählen. Alternativ können Sie einen Namespace als Standardnamespace deklarieren, was die folgende geänderte Abfrage zeigt:  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
<step xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
…  
```  
  
 Beachten Sie in diesem Beispiel, dass der definierte Namespace – `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"` – angelegt wurde, um den Standardnamespace oder einen leeren Namespace zu überschreiben. Aus diesem Grund befindet sich in dem für die Abfrage verwendeten Pfadausdruck kein Namespacepräfix mehr. Auch in den in den Ergebnissen enthaltenen Elementnamen befinden sich keine Namespacepräfixe mehr. Darüber hinaus wird der Standardnamespace auf alle Element angewendet, aber nicht auf deren Attribute.  
  
### <a name="c-using-namespaces-in-xml-construction"></a>C. Verwenden von Namespaces in XML-Konstruktion  
 Wenn Sie neue Namespaces definieren, gelten diese nicht nur für die Abfrage, sondern auch für die Konstruktion. Bei der XML-Konstruktion können Sie z. B. mit der "`declare namespace ...`"-Deklaration einen neuen Namespace definieren und diesen Namespace dann mit allen Elementen und Attributen verwenden, die Sie als Abfrageergebnisse erstellen.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace myNS="uri:SomeNamespace";<myNS:Result>  
          { /ProductDescription/Summary }  
       </myNS:Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Dies ist das Ergebnis:  
  
```  
  
      <myNS:Result xmlns:myNS="uri:SomeNamespace">  
  <Summary xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
     Our top-of-the-line competition mountain bike. Performance-enhancing   
     options include the innovative HL Frame, super-smooth front   
     suspension, and traction for all terrain.</p1:p>  
  </Summary>  
</myNS:Result>  
```  
  
 Alternativ können Sie den Namespace auch explizit an jedem Punkt definieren, an dem er als Teil der XML-Konstruktion verwendet wird. Das folgende Beispiel verdeutlicht dies:  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>D. Konstruktion mit Standardnamespaces  
 Für die Verwendung im konstruierten XML können Sie auch einen Standardnamespace definieren. Z. B. die folgende Abfrage zeigt, wie Sie einen Standardnamespace "SomeNamespace" angeben können\\, um als Standard für lokal benannte Elemente, die z. B. erstellt werden, verwenden die `<Result>` Element.  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      declare default element namespace "uri:SomeNamespace";<Result>  
          { /PD:ProductDescription/PD:Summary }  
       </Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Dies ist das Ergebnis:  
  
```  
  
      <Result xmlns="uri:SomeNamespace">  
  <PD:Summary xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 Beachten Sie, dass durch das Überschreiben des Standardelementnamespace oder leerer Namespaces alle in dem konstruierten XML enthaltenen, lokal benannten Elemente anschließend an den überschreibenden Standardnamespace gebunden werden. Wenn Sie Flexibilität bei der XML-Konstruktion benötigen und die Vorteile leerer Namespaces nutzen wollen, sollten Sie aus diesem Grund den Standardelementnamespace nicht überschreiben.  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
