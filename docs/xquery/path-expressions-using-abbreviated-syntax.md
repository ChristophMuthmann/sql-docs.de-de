---
title: Mithilfe von Syntax in einem Pfadausdruck abgekürzt | Microsoft Docs
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
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9751d48c38ae96f85d0cc97992f5dd5acfef9b2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="path-expressions---using-abbreviated-syntax"></a>Path-Ausdrücken - verwenden abgekürzter Syntax
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In allen Beispielen in [Understanding the Path Expressions in XQuery](../xquery/path-expressions-xquery.md) verwenden abgekürzte Syntax für Path-Ausdrücken. Die ungekürzte Syntax für einen Achsenschritt in einem Pfadausdruck umfasst den Achsennamen und den Knotentest, getrennt durch einen Doppelpunkt und gefolgt von null oder mehr Schrittqualifizierern.  
  
 Beispiel:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery unterstützt die folgenden Abkürzungen für die Verwendung in path-Ausdrücken:  
  
-   Die **untergeordneten** -Achse ist die Standardachse. Aus diesem Grund die **untergeordneten::** Achse kann in einem Schritt in einem Ausdruck ausgelassen werden. So kann z. B. `/child::ProductDescription/child::Summary` als `/ProductDescription/Summary` geschrieben werden.  
  
-   Ein **Attribut** -Achse kann abgekürzt werden @. So kann z. B. `/child::ProductDescription[attribute::ProductModelID=10]` als `/ProudctDescription[@ProductModelID=10]` geschrieben werden.  
  
-   Ein **/descendant-or-self::node()/** kann abgekürzt werden / /. So kann z. B. `/descendant-or-self::node()/child::act:telephoneNumber` als `//act:telephoneNumber` geschrieben werden.  
  
     Die vorherige Abfrage ruft alle Rufnummern ab, die in der AdditionalContactInfo-Spalte in der Contact-Tabelle gespeichert sind. Das Schema für AdditionalContactInfo wird so definiert, die eine \<"telephoneNumber" >-Element an beliebiger Stelle im Dokument auftreten kann. Aus diesem Grund müssen Sie zum Abrufen aller Rufnummern jeden Knoten im Dokument durchsuchen. Die Suche beginnt im Stamm des Dokuments und wird dann über alle nachfolgenden Knoten fortgesetzt.  
  
     Die folgende Abfrage ruft alle Rufnummern für einen bestimmten Kundenkontakt ab:  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="http://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     Wenn Sie den Pfadausdruck durch die abgekürzte Syntax `//act:telephoneNumber` ersetzen, können Sie die gleichen Ergebnisse erzielen.  
  
-   Die **Self::node()** in einem Schritt kann zu einem einzelnen Punkt (.) abgekürzt werden. Der Punkt ist jedoch nicht äquivalent oder austauschbar mit der **Self::node()**.  
  
     In der folgenden Abfrage stellt die Verwendung eines Punkts z. B. einen Wert und keinen Knoten dar:  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   Die **Parent::node()** in einem Schritt kann zu einem zwei Punkten (..) abgekürzt werden.  
  
  
