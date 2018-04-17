---
title: 'Schritt 4 b: die Anzahl der Zeilen abrufen | Microsoft Docs'
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
ms.topic: article
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 231608e65d186c23ffd2baff50e6b8d5d94a3eb3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="step-4b-fetch-the-row-count"></a>Schritt 4 b: die Anzahl der Zeilen abrufen
Der nächste Schritt ist beim Abrufen der Zeilenanzahl liegt, wie in der folgenden Abbildung dargestellt.  
  
 ![Zeigt das Abrufen der Zeilenanzahl](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 Wenn die Anweisung in Schritt 3 ausgeführt wurde ein **UPDATE**, **löschen**, oder **einfügen** -Anweisung, die Anwendung ruft die Anzahl der betroffenen Zeilen mit  **SQLRowCount**. Weitere Informationen finden Sie unter [bestimmen die Anzahl der betroffenen Zeilen](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
 Die Anwendung jetzt gibt, Schritt 3, um zu einer anderen Anweisung in derselben Transaktion ausgeführt oder mit Schritt 5, um einen commit oder Rollback der Transaktions fortgesetzt wird.
