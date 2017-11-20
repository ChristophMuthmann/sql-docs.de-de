---
title: "WIE Prädikat Einschränkungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5668f03e785c0d27133965f16af40ce69c2a2567
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="like-predicate-limitations"></a>WIE Prädikat Einschränkungen
Wenn Daten in einer Spalte mehr als 255 Zeichen sind, wird der Vergleich mit LIKE nur auf die ersten 255 Zeichen basieren.  
  
 LIKE verwendet wird, eine Prozedur ist nur bei Konstantenmuster unterstützt. Der Desktop-Datenbanktreiber unterstützt SQL-92 wie Mustervergleich.  
  
 Verwenden einer Escape-Klausel in einer LIKE-Prädikat wird nicht unterstützt.  
  
 Ein Vergleich mit LIKE sollten nicht für eine Spalte mit Daten eines Datentyps Numeric oder "float" ausgeführt werden. Die Ergebnisse möglicherweise nicht vorhersehbar. Weitere Informationen finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.

