---
title: Round-Funktion (XQuery) | Microsoft Docs
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
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5626f5e882d7ca9f300b0ec5c2dae50d2f426ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-values-functions---round"></a>Numerische Werte Funktionen - round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Zahl (ohne Stellen hinter dem Dezimalpunkt) zurück, die dem Argument am nächsten kommt. Wenn es mehr als eine solche Zahl gibt, wird diejenige zurückgegeben, die am nächsten an der positiv unendlichen Zahl liegt. Beispiel:  
  
 Wenn das Argument 2.5 ist **round()** gibt 3 zurück.  
  
 Wenn das Argument 2.4999, **round()** gibt 2 zurück.  
  
 Wenn das Argument-2.5 ist **round()** -2 zurück.  
  
 Wenn das Argument eine leere Sequenz ist **round()** die leere Sequenz zurückgibt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Anzahl, auf die die Funktion angewendet wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Typ des *$arg* ist einer der drei numerischen Basistypen **xs: float**, **xs: double**, oder **xs: decimal**, der Rückgabetyp ist identisch mit der *$arg* Typ. Wenn der Typ des *$arg* ist ein Typ, der einen der numerischen Typen abgeleitet ist der Rückgabetyp ist der numerische Basistyp.  
  
 Wenn die Eingabe in die **Fn: Floor**, **Fn: CEILING**, oder **Fn: Round** Funktionen **xdt: UntypedAtomic**, nicht typisierte Daten, er wird implizit umgewandelt in **xs: double**.  
  
 Alle anderen Typen führen zum Generieren eines statischen Fehlers.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen in verschiedenen gespeicherten **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
 Sie können das Arbeitsbeispiel in der [Ceiling-Funktion (XQuery)](../xquery/numeric-values-functions-ceiling.md) für die **round()** XQuery-Funktion. Alle erfordern wird, ersetzen die **ceiling()** Funktion in der Abfrage durch die **round()** Funktion.  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **round()** -Funktion ordnet ganzzahligen Werte xs: Decimal.  
  
-   Die **round()** -Funktion von xs: Double und xs: float-Werten zwischen - 0.5e0 und -0e0 werden 0e0 zugeordnet statt - 0e0 zugeordnet.  
  
## <a name="see-also"></a>Siehe auch  
 [Floor-Funktion &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [CEILING-Funktion &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
