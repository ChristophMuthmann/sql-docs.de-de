---
title: 'Schritt 5: Commit die Transaktion | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 680901e7be6f3fa556b18ed1381d49c2f09f09be
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="step-5-commit-the-transaction"></a>Schritt 5: Commit der Transaktions
Der nächste Schritt ist beim commit der Transaktion, wie in der folgenden Abbildung dargestellt.  
  
 ![Zeigt, wie Commit eine Transaktion](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 Der fünfte Schritt ist das Aufrufen **SQLEndTran** , einen commit oder Rollback der Transaktion. Die Anwendung führt diesen Schritt nur, wenn die Commit-Transaktionsmodus Manualcommit-festlegen; Transaktions-Commit-Modus ist Autocommit-dies die Standardgröße ist die Transaktion automatisch ein Commit ausgeführt, wenn die Anweisung ausgeführt wird. Weitere Informationen finden Sie unter [Transaktionen](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Zum Ausführen einer Anweisung in einer neuen Transaktion gibt die Anwendung mit Schritt 3 fort. Um aus der Datenquelle zu trennen, wird Sie mit Schritt 6 die Anwendung fortgesetzt.
