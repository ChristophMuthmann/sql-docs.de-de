---
title: Verwenden der Volltextsuche mit XML-Spalten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1599be61411bc98c7862b0c76360caa15818202a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-full-text-search-with-xml-columns"></a>Verwenden der Volltextsuche mit XML-Spalten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Sie können einen Volltextindex für XML-Spalten erstellen, bei dem der Inhalt der XML-Werte indiziert, das XML-Markup jedoch ignoriert wird. Elementtags werden als Tokenbegrenzungen verwendet. Folgende Elemente werden indiziert:  
  
-   Der Inhalt von XML-Elementen.  
  
-   Nur der Inhalt von XML-Attributen des Elements der obersten Ebene, außer wenn diese Werte numerische Werte sind.  
  
 Gegebenenfalls können Sie die Volltextsuche mit dem XML-Index auf folgende Weise kombinieren:  
  
1.  Filtern Sie zuerst die XML-Werte von Interesse mithilfe der SQL-Volltextsuche.  
  
2.  Fragen Sie als Nächstes solche XML-Werte ab, die den XML-Index für die XML-Spalte verwenden.  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>Beispiel: Kombinieren der Volltextsuche mit einer XML-Abfrage  
 Nachdem der Volltextindex für die XML-Spalte erstellt wurde, überprüft die folgende Abfrage, ob ein XML-Wert das Wort "custom" im Titel eines Buchs enthält:  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 Die **contains()** -Methode verwendet den Volltextindex, um die XML-Werte, die das Wort „custom“ irgendwo im Dokument enthalten, zu einer Teilmenge zusammenzufassen. Die **exist()** -Klausel stellt sicher, dass das Wort „custom“ im Titel eines Buchs vorkommt.  
  
 Eine Volltextsuche mit der **contains()** -Klausel und XQuery mithilfe der **contains()** -Klausel weisen unterschiedliche Semantiken auf. Das Letztere ist eine Teilzeichenfolgenübereinstimmung, und das Erstere ist eine Tokenübereinstimmung mithilfe der Wortformgenerierung. Wenn die Suche nach der Zeichenfolge erfolgt, die „run“ im Titel enthält, gilt neben „run“ auch „runs“ und „running“ als Übereinstimmung, weil sowohl die Volltextklausel **contains()** als auch die XQuery-Klausel **contains()** erfüllt ist. Allerdings ergibt die Abfrage keine Übereinstimmung des Worts "customizable" im Titel, weil die Volltextklausel **contains()** nicht erfüllt ist, obwohl die XQuery-Klausel **contains()** erfüllt ist. Im Allgemeinen sollte für eine reine Teilzeichenfolgenübereinstimmung die Volltextklausel **contains()** entfernt werden.  
  
 Außerdem verwendet die Volltextsuche die Wortformgenerierung, während XQuery **contains()** eine Literalübereinstimmung ist. Dieser Unterschied wird im folgenden Beispiel veranschaulicht.  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>Beispiel: Volltextsuche für XML-Werte mit Wortformgenerierung  
 Die XQuery **contains()** -Überprüfung, die im vorherigen Beispiel durchgeführt wurde, kann im Allgemeinen nicht eliminiert werden. Angenommen, die folgende Abfrage wird ausgeführt:  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 Das Wort "ran" im Dokument stimmt wegen der Verwendung der Wortformgenerierung mit der Suchbedingung überein. Außerdem wird der Suchkontext nicht mithilfe von XQuery überprüft.  
  
 Wenn XML in relationale Spalten zerlegt wird, indem volltextindizierte AXSD verwendet wird, führen XPath-Abfragen, die für die XML-Sicht ausgeführt werden, keine Volltextsuche der zugrunde liegenden Tabellen durch.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
