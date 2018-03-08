---
title: 'Schritt 2: Initialisieren Sie die Anwendung | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64ef3dea2a8403af43cc03a3deeee47ff16dd2b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="step-2-initialize-the-application"></a>Schritt 2: Initialisieren Sie die Anwendung
Der zweite Schritt ist zum Initialisieren der Anwendung, wie in der folgenden Abbildung dargestellt. Genau wie hier erfolgt, hängt mit der Anwendung.  
  
 ![Initialisieren einer ODBC-Anwendung zeigt](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 An diesem Punkt ist es üblich, dass verwendet **SQLGetInfo** ermitteln Sie die Funktionen des Treibers. Weitere Informationen finden Sie unter [Datenbankfunktionen in Betracht ziehen, zu verwendende](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Alle Anwendungen müssen ein Anweisungshandle mit zuordnen **SQLAllocHandle**, und legen Sie viele Clientanwendungen Anweisungsattribute, z. B. der Cursortyp mit **SQLSetStmtAttr**. Weitere Informationen finden Sie unter [ein Anweisungshandle zuordnen](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) und [Anweisungsattribute](../../../odbc/reference/develop-app/statement-attributes.md).
