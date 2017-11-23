---
title: Data Accessor-Funktionen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords: data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c77c0a1a9b6d61465956d8e1e81eb58e86f8b086
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="data-accessor-functions"></a>Data Accessor-Funktionen
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die Themen in diesem Abschnitt behandeln die Datenaccessorfunktionen und stellen entsprechenden Beispielcode bereit.  
  
## <a name="understanding-fndata-fnstring-and-text"></a>Grundlegendes zu 'fn:data()', 'fn:string()' und text()  
 XQuery verfügt über eine Funktion **Fn:Data()** zum Extrahieren skalarer, extrahierter Werte aus Knoten, ein Knotentest **text()** zum Zurückgeben von Textknoten und die Funktion **Fn:String()** zurückgibt, die die Der Zeichenfolgenwert eines Knotens. Ihre Verwendung kann verwirrend sein. Im Folgenden finden Sie Richtlinien zu ihrer ordnungsgemäßen Verwendung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Die XML-Instanz \<Age > 12 \< /age > dient zur Veranschaulichung.  
  
-   Nicht typisiertes XML: Der Pfadausdruck /age/text() gibt den Textknoten 12 zurück. Die Funktion fn:data(/age) gibt den Zeichenfolgenwert 12 zurück, was auch für fn:string(/age) gilt.  
  
-   Typisiertes XML: Der Ausdruck /age/text() gibt einen statischen Fehler für eine beliebige einfache typisierte \<Age > Element. Dagegen gibt fn:data(/age) die ganze Zahl 12 zurück. fn:string(/age) führt zur Zeichenfolge 12.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [eine Zeichenfolge Function &#40; XQuery &#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [Data-Funktion &#40; XQuery &#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Path-Ausdrücken &#40; XQuery &#41;](../xquery/path-expressions-xquery.md)  
  
  
