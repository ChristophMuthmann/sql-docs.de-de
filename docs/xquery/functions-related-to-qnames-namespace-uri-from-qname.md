---
title: Namespace-Uri-aus-QName (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94b19762329355d7e62e13fe7e8614755f3a96ce
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Funktionen im Zusammenhang mit QNames - Namespace-Uri von QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
  
  
