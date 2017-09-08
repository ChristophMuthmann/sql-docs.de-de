---
title: DISTINCT-Values-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94650b355d0431b66103237b019dff01fedbc0e9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-sequences---distinct-values"></a>Funktionen für Sequenzen - distinct-Werte
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt doppelte Werte aus der angegebenen Sequenz *$arg*. Wenn *$arg* ist eine leere Sequenz, die leere Sequenz zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Sequenz der atomaren Werte.  
  
## <a name="remarks"></a>Hinweise  
 Alle Typen der atomaren Werte, die übergeben werden **distinct-values()** müssen Untertypen des gleichen Basistyps sein. Basistypen, die akzeptiert werden, sind Typen, die die **Eq** Vorgang. Diese Typen sind z. B. die drei integrierten numerischen Basistypen, die date/time-Basistypen, xs:string, xs:boolean und xdt:untypedAtomic. Werte des Typs xdt:untypedAtomic werden in xs:string umgewandelt. Wenn eine Mischung dieser Typen vorliegt oder andere Werte anderer Typen übergeben werden, wird ein statischer Fehler ausgelöst.  
  
 Das Ergebnis des **distinct-values()** erhält den Basistyp der übergebenen Typen, z. B. xs: String im Fall von xdt: UntypedAtomic, mit der ursprünglichen Kardinalität. Wenn die Eingabe statisch leer ist, wird dies angegeben und ein statischer Fehler ausgelöst wird.  
  
 Werte vom Typ xs:string werden mit der Unicode-Codepunkt-Standardsortierung von XQuery verglichen.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Verwenden der distinct-values()-Funktion zum Entfernen doppelter Werte aus der Sequenz  
 In diesem Beispiel wird eine XML-Instanz, die Rufnummern enthält zugewiesen ist ein **Xml** Typvariablen. Die XQuery, die auf diese Variable wird verwendet, die mit der **distinct-values()** Funktion, um eine Liste von Rufnummern zu kompilieren, die keine Duplikate enthalten.  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 Dies ist das Ergebnis:  
  
```  
111-111-1111 222-222-2222    
```  
  
 In der folgenden Abfrage wird übergeben eine Sequenz von Zahlen (1, 1, 2) in der **distinct-values()** Funktion. Die Funktion entfernt anschließend die doppelten Werte in der Sequenz und gibt die beiden verbleibenden Werte zurück.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 Die Abfrage gibt 1 2 zurück.  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **distinct-values()** -Funktion ordnet ganzzahligen Werte xs: Decimal.  
  
-   Die **distinct-values()** Funktion nur die oben erwähnten Typen unterstützt und die Mischung der Basistypen nicht unterstützt.  
  
-   Die **distinct-values()** Funktion auf xs: Duration-Werten wird nicht unterstützt.  
  
-   Die Option syntactic, die eine Sortierung bereitstellt, wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
