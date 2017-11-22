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
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 780b8ade4417aac4ee4b5a6472d0b3e14776cd10
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Date, Time und Timestamp-Literale
Für eine optimale Interoperabilität sollte Anwendungen der kanonischen ODBC-Format mit Escape-Klausel Syntax Datumsliterale übergeben:  
  
-   Für Datumsliterale {d '*Wert*"}, wobei *Valu*e hat das Format"Yyyy-mm-Dd"  
  
-   Für Time-Literale {t '*Wert*"}, wobei *Valu*e hat das Format"hh"  
  
 Für Zeitstempel Literale {ts'*Wert*"}, wobei *Valu*e hat das Format" jjjj-mm-tt hh: mm: [. f...] ".
