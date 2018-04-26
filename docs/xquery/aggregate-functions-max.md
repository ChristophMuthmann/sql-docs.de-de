---
title: Max-Funktion (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b04741b79c65e2fd698d211129d22f5463261c79
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="aggregate-functions---max"></a>Aggregatfunktionen - max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt aus einer Sequenz aus atomaren Werten *$arg*, die ein Element, dessen Wert größer als alle anderen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Sequenz der atomaren Werte, aus denen der Maximalwert zurückgegeben wird.  
  
## <a name="remarks"></a>Hinweise  
 Alle Typen der atomaren Werte, die übergeben werden **max()** müssen Untertypen des gleichen Basistyps sein. Basistypen, die akzeptiert werden, sind Typen, die die **Gt** Vorgang. Diese Typen sind z. B. die drei integrierten numerischen Basistypen, die date/time-Basistypen, xs:string, xs:boolean und xdt:untypedAtomic. Werte des Typs xdt:untypedAtomic werden in xs:double umgewandelt. Wenn eine Mischung dieser Typen ist, oder wenn andere Werte anderer Typen übergeben werden, wird ein statischer Fehler ausgelöst.  
  
 Das Ergebnis des **max()** erhält den Basistyp der übergebenen Typen, z. B. xs: Double im Fall von xdt: UntypedAtomic. Wenn die Eingabe statisch leer ist, wird dies angegeben und ein statischer Fehler ausgelöst wird.  
  
 Die **max()** Funktion gibt einen Wert zurück, in der Sequenz, die größer als alle anderen Werte in der Eingabesequenz ist. Für xs:string-Werte wird die Unicode-Codepunkt-Standardsortierung verwendet. Wenn ein xdt: UntypedAtomic-Wert in xs: Double umgewandelt werden kann, wird der Wert in der Eingabesequenz ignoriert *$arg*. Wenn die Eingabe eine dynamisch berechnete leere Sequenz ist, wird die leere Sequenz zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** in Spalten vom Typ der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank.  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. Ermitteln der Arbeitsplatzstandorte im Herstellungsprozess mit den meisten Arbeitsstunden unter Verwendung der () XQuery-Funktion  
 Die Abfrage im bereitgestellten [min-Funktion (XQuery)](../xquery/aggregate-functions-min.md) kann so umgeschrieben werden, dass mithilfe der **max()** Funktion.  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **max (**)-Funktion ordnet alle ganzzahligen Werte xs: Decimal.  
  
-   Die **max()** -Funktion für Werte des Typs xs: Duration nicht unterstützt.  
  
-   Sequenzen, die Typen über Basistypbegrenzungen hinweg mischen, werden nicht unterstützt.  
  
-   Die Option syntactic, die eine Sortierung bereitstellt, wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
