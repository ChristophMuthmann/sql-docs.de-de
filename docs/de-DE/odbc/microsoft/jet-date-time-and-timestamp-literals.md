---
title: 'Jet: Date, Time und Timestamp-Literale | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: cc36c46885a358e1ca453901fd72362ed1dbb32b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Date, Time und Timestamp-Literale
Für eine optimale Interoperabilität sollte Anwendungen der kanonischen ODBC-Format mit Escape-Klausel Syntax Datumsliterale übergeben:  
  
-   Für Datumsliterale {d '*Wert*"}, wobei *Valu*e hat das Format"Yyyy-mm-Dd"  
  
-   Für Time-Literale {t '*Wert*"}, wobei *Valu*e hat das Format"hh"  
  
 Für Zeitstempel Literale {ts'*Wert*"}, wobei *Valu*e hat das Format" jjjj-mm-tt hh: mm: [. f...] ".
