---
title: AVG-Funktion (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f3c3acc233552cae8f3237e38ef3b4328b4eee5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="aggregate-functions---avg"></a>Aggregatfunktionen - durchschn.
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Mittelwert einer Sequenz von Zahlen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Die Sequenz der atomaren Werte, deren Mittelwert berechnet wird.  
  
## <a name="remarks"></a>Hinweise  
 Alle Typen der atomaren Werte, die übergeben werden **avg()** ein Untertyp genau eines der drei integrierten numerischen Basistypen oder xdt: UntypedAtomic sein. Es darf keine Mischung vorliegen. Werte des Typs xdt:untypedAtomic werden wie xs:double behandelt. Das Ergebnis des **avg()** erhält den Basistyp der übergebenen Typen, z. B. xs: Double im Fall von xdt: UntypedAtomic.  
  
 Wenn die Eingabe statisch leer ist, wird dies angegeben und ein statischer Fehler ausgegeben.  
  
 Die **avg()** Funktion gibt den Mittelwert der berechneten Zahlen zurück. Beispiel:  
  
 **SUM (** *$arg* **) Div-Anzahl (** *$arg* **)**  
  
 Wenn *$arg* ist eine leere Sequenz ist, wird die leere Sequenz zurückgegeben.  
  
 Wenn ein xdt: UntypedAtomic-Wert in xs: Double umgewandelt werden kann, wird der Wert in der Eingabesequenz ignoriert *$arg*.  
  
 In allen anderen Fällen gibt die Funktion einen statischen Fehler zurück.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. Verwenden der XQuery-Funktion avg() zum Suchen nach Arbeitsplatzstandorten im Fertigungsprozess, an denen die Anzahl der Arbeitsstunden größer als der Mittelwert für alle Arbeitsplatzstandorte ist.  
 Sie können die Abfrage im bereitgestellten umschreiben [min-Funktion (XQuery)](../xquery/aggregate-functions-min.md) verwenden die **avg()** Funktion.  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **avg()** -Funktion ordnet alle ganzzahligen Werte xs: Decimal.  
  
-   Die **avg()** -Funktion für Werte des Typs xs: Duration nicht unterstützt.  
  
-   Sequenzen, die Typen über Basistypbegrenzungen hinweg mischen, werden nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
