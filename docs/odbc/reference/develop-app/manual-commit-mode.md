---
title: Manualcommit-Modus | Microsoft Docs
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
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d0e5a4cc5bbda6c8ee4414854f390694297c94e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="manual-commit-mode"></a>Manualcommit-Modus
*Im Manualcommit-Modus* Anwendungen müssen explizit Transaktionen abschließen, indem Aufrufen **SQLEndTran** sie commit oder Rollback sie. Dies ist der normale Transaktionsmodus für die meisten relationalen Datenbanken.  
  
 Transaktionen in ODBC müssen nicht explizit initiiert werden. Stattdessen beginnt eine Transaktion implizit bei jedem der Anwendung Start, für die Datenbank ausgeführt. Wenn die Datenquelle Start einer expliziten Transaktion erforderlich ist, muss der Treiber bereitstellen, wenn die Anwendung eine Anweisung führt, die eine Transaktion erfordern, und keine aktuelle Transaktion vorhanden ist.
