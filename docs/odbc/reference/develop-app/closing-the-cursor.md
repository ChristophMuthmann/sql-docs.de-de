---
title: Schließen des Cursors | Microsoft Docs
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
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54cc6515ea7b0c60916e9bb1ebd00d0b05af549e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="closing-the-cursor"></a>Schließen des Cursors
Wenn eine Anwendung mithilfe eines Cursors abgeschlossen ist, ruft er **SQLCloseCursor** Schließen des Cursors. Beispiel:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Bis die Anwendung den Cursor geschlossen wurde, kann nicht die Anweisung, die auf der der Cursor geöffnet wird für die meisten anderen Vorgänge, z. B. das Ausführen einer anderen SQL­Anweisung verwendet werden. Eine vollständige Liste der Funktionen, die aufgerufen werden kann, während ein Cursor geöffnet ist, finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Um einen Cursor zu schließen, eine Anwendung aufrufen sollte **SQLCloseCursor**, nicht **SQLCancel**.  
  
 Cursor bleiben geöffnet, bis sie explizit geschlossen werden, außer wenn eine Transaktion ein Commit oder Rollback wird in diesem Fall einige Datenquellen den Cursor zu schließen. Insbesondere erreichen das Ende des Resultsets festgelegt, wenn **SQLFetch** SQL_NO_DATA zurückgibt, wird einen Cursor nicht geschlossen. Auch Cursor bei leeren Resultsets (Resultsets erstellt, wenn eine Anweisung erfolgreich ausgeführt wurde, aber die keine Zeilen zurückgegeben), müssen explizit geschlossen werden.
