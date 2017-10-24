---
title: Sequenz und QNames (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79e43de914a80fd8f39ebab0b93c55c1e1fc2670
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sequence-and-qnames-xquery"></a>Sequenz und QNames (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden die folgenden grundlegenden Konzepte von XQuery beschrieben:  
  
-   Sequenz  
  
-   QNames und vordefinierte Namespaces  
  
## <a name="sequence"></a>Sequenz  
 In XQuery ist das Ergebnis eines Ausdrucks eine Sequenz, die aus einer Liste von XML-Knoten und aus Instanzen von atomaren XSD-Typen besteht. Ein einzelner Eintrag in einer Sequenz wird als ein Item bezeichnet. Ein Item in einer Sequenz kann einem der folgenden Typen entsprechen:  
  
-   Ein Knoten, wie z. B. ein Element, Attribut, Text, eine Verarbeitungsanweisung, ein Kommentar oder Dokument  
  
-   Ein atomarer Wert, z. B. eine Instanz eines einfachen XSD-Typs  
  
 Die folgende Abfrage konstruiert z. B. eine Sequenz aus zwei Elementknotenelementen:  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 Dies ist das Ergebnis:  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 In der vorigen Abfrage ist das Komma (`,`) am Ende der `<step1>`-Konstruktion der erforderliche Sequenzkonstruktor. Die Leerzeichen in den Ergebnissen wurden nur zur Veranschaulichung hinzugefügt und sind in allen Beispielergebnissen in dieser Dokumentation enthalten.  
  
 Es folgen einige Zusatzinformationen zum Konzept der Sequenzen:  
  
-   Wenn eine Abfrage zu einer Sequenz führt, die eine andere Sequenz enthält, so wird die enthaltene Sequenz in der Containersequenz vereinfacht. So wird die Sequenz ((1,2, (3,4,5)),6) z. B. im Datenmodell zu (1, 2, 3, 4, 5, 6) vereinfacht.  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   Eine leere Sequenz ist eine Sequenz, die kein Item enthält. Das wird als "()" dargestellt.  
  
-   Eine Sequenz mit nur einem Item kann als ein atomarer Wert behandelt werden und umgekehrt. Das heißt: (1) = 1.  
  
 In dieser Implementierung muss die Sequenz homogen sein. Das heißt, dass eine Sequenz entweder ganz aus atomaren Werten oder aus Knoten bestehen kann. So sind z. B. die folgenden Sequenzen gültig:  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 Die folgende Abfrage gibt einen Fehler zurück, weil heterogene Sequenzen nicht unterstützt werden.  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 Jeder Bezeichner in einer XQuery-Abfrage ist ein QName. Ein QName besteht aus einem Namespacepräfix und einem lokalen Namen. In dieser Implementierung sind die XQuery-Variablennamen QNames, und sie können keine Präfixe besitzen.  
  
 Betrachten Sie das folgende Beispiel, in denen eine Abfrage angegeben wird, für eine nicht typisierte **Xml** Variablen:  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 Im Ausdruck (`/Root/a`) sind `Root` und `a` QNames.  
  
 Im folgenden Beispiel wird eine Abfrage angegeben für eine typisierte **Xml** Spalte. Die Abfrage führt eine Iteration durch alle \<Schritt >-Elemente am ersten arbeitsplatzstandort.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Beachten Sie im Abfrageausdruck Folgendes:  
  
-   `AWMI root`, `AWMI:Location`, `AWMI:step` und `$Step` sind jeweils QNames. `AWMI` ist ein Präfix, und `root`, `Location` und `Step` sind lokale Namen.  
  
-   Die `$step`-Variable ist ein QName und besitzt kein Präfix.  
  
 Die folgenden Namespaces sind zum Verwenden für die XQuery-Unterstützung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vordefiniert.  
  
|Präfix|URI|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(kein Präfix)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|http://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`http://www.w3.org/XML/1998/namespace`|  
|(kein Präfix)|`http://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 Jede Datenbank, die Sie erstellen, besitzt die **Sys** XML-schemaauflistung. Sie reserviert diese Schemas, sodass auf sie von jeder benutzererstellten XML-Schemaauflistung zugegriffen werden kann.  
  
> [!NOTE]  
>  Diese Implementierung unterstützt nicht das `local`-Präfix, das in der XQuery-Spezifikation unter http://www.w3.org/2004/07/xquery-local-functions beschrieben wird.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Basics (XQuery-Grundlagen)](../xquery/xquery-basics.md)  
  
  

