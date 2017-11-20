---
title: 'Jet: Date, Time und Timestamp-Literale | Microsoft Docs'
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
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c1a98ca0b68198dada19e4ac81f8637798a99b95
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Date, Time und Timestamp-Literale
Für eine optimale Interoperabilität sollte Anwendungen der kanonischen ODBC-Format mit Escape-Klausel Syntax Datumsliterale übergeben:  
  
-   Für Datumsliterale {d '*Wert*"}, wobei *Valu*e hat das Format"Yyyy-mm-Dd"  
  
-   Für Time-Literale {t '*Wert*"}, wobei *Valu*e hat das Format"hh"  
  
 Für Zeitstempel Literale {ts'*Wert*"}, wobei *Valu*e hat das Format" jjjj-mm-tt hh: mm: [. f...] ".

