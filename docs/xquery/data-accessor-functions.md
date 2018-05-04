---
title: Data Accessor-Funktionen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a18880a2419467bdd7abe8ab8830af81faae69f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-accessor-functions"></a>Data Accessor-Funktionen
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die Themen in diesem Abschnitt behandeln die Datenaccessorfunktionen und stellen entsprechenden Beispielcode bereit.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Grundlegendes zu 'fn:data()', 'fn:string()' und text()  
 XQuery verfügt über eine Funktion **Fn:Data()** zum Extrahieren skalarer, extrahierter Werte aus Knoten, ein Knotentest **text()** zum Zurückgeben von Textknoten und die Funktion **Fn:String()** zurückgibt, die die Der Zeichenfolgenwert eines Knotens. Ihre Verwendung kann verwirrend sein. Im Folgenden finden Sie Richtlinien zu ihrer ordnungsgemäßen Verwendung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Die XML-Instanz \<Age > 12 \< /age > dient zur Veranschaulichung.  
  
-   Nicht typisiertes XML: Der Pfadausdruck /age/text() gibt den Textknoten 12 zurück. Die Funktion fn:data(/age) gibt den Zeichenfolgenwert 12 zurück, was auch für fn:string(/age) gilt.  
  
-   Typisiertes XML: Der Ausdruck /age/text() gibt einen statischen Fehler für eine beliebige einfache typisierte \<Age > Element. Dagegen gibt fn:data(/age) die ganze Zahl 12 zurück. fn:string(/age) führt zur Zeichenfolge 12.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [String-Funktion &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Data-Funktion &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Path-Ausdrücken &#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
