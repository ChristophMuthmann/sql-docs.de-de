---
title: Namespace-Uri-aus-QName (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34a8b738a8c4b38951ff73f4437e3327a3d6a852
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funktionen im Zusammenhang mit QNames - Namespace-Uri von QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeichenfolge, die den Namespace-Uri, der vom angegebenen QName darstellt *$arg*. Das Ergebnis ist die leere Sequenz, wenn *$arg* die leere Sequenz.  
  
## <a name="syntax"></a>Syntax  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Ist der QName, dessen Namespace-URI zurückgegeben wurde.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. Abrufen der Namespace-URI von einem QName  
 Ein funktionierendes Beispiel finden Sie unter [lokale Namen von QName &#40; XQuery &#41; ](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **namespace-uri-from-QName()** -Funktion gibt Instanzen von xs: String, statt xs: anyURI zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen, die im Zusammenhang mit QNames &#40; XQuery &#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
