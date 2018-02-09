---
title: Floor-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
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
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e54241fde9a0c97fe66687c88d82812c7ce0d5eb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="numeric-values-functions---floor"></a>Floor-Funktionen für numerische Werte-
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die größte Zahl ohne Bruchanteil zurück, die nicht größer als der Wert ihres Arguments ist. Wenn das Argument eine leere Sequenz ist, wird die leere Sequenz zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Anzahl, auf die die Funktion angewendet wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Typ des *$arg* ist einer der drei numerischen Basistypen **xs: float**, **xs: double**, oder **xs: decimal**, der Rückgabetyp ist identisch mit der *$arg* Typ. Wenn der Typ des *$arg* ist ein Typ, der einen der numerischen Typen abgeleitet ist der Rückgabetyp ist der numerische Basistyp.  
  
 Wenn die Eingabe für die Funktionen Fn: Floor, Fn: CEILING oder Fn: Round wird **xdt: UntypedAtomic**, nicht typisierte Daten, er wird implizit umgewandelt in **xs: double**. Alle anderen Typen führen zum Generieren eines statischen Fehlers.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Beispieldatenbank.  
  
 Sie können das Arbeitsbeispiel in der [Ceiling-Funktion (XQuery)](../xquery/numeric-values-functions-ceiling.md) für die **floor()** XQuery-Funktion. Alle erfordern wird, ersetzen die **ceiling()** Funktion in der Abfrage durch die **floor()** Funktion.  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **floor()** -Funktion ordnet alle ganzzahligen Werte xs: Decimal.  
  
## <a name="see-also"></a>Siehe auch  
 [CEILING-Funktion &#40; XQuery &#41;](../xquery/numeric-values-functions-ceiling.md)   
 [Round-Funktion &#40; XQuery &#41;](../xquery/numeric-values-functions-round.md)   
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
