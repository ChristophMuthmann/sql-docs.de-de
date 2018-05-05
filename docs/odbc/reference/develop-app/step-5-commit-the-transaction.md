---
title: 'Schritt 5: Commit die Transaktion | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a311752588742df8f597ce2957c6ba600d8b47c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="step-5-commit-the-transaction"></a>Schritt 5: Commit der Transaktions
Der nächste Schritt ist beim commit der Transaktion, wie in der folgenden Abbildung dargestellt.  
  
 ![Zeigt, wie Commit eine Transaktion](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 Der fünfte Schritt ist das Aufrufen **SQLEndTran** , einen commit oder Rollback der Transaktion. Die Anwendung führt diesen Schritt nur, wenn die Commit-Transaktionsmodus Manualcommit-festlegen; Transaktions-Commit-Modus ist Autocommit-dies die Standardgröße ist die Transaktion automatisch ein Commit ausgeführt, wenn die Anweisung ausgeführt wird. Weitere Informationen finden Sie unter [Transaktionen](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Zum Ausführen einer Anweisung in einer neuen Transaktion gibt die Anwendung mit Schritt 3 fort. Um aus der Datenquelle zu trennen, wird Sie mit Schritt 6 die Anwendung fortgesetzt.
