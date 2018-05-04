---
title: 'Schritt 2: Initialisieren Sie die Anwendung | Microsoft Docs'
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
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a577a51395b44d110cde0ae031d76c83df481d46
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="step-2-initialize-the-application"></a>Schritt 2: Initialisieren Sie die Anwendung
Der zweite Schritt ist zum Initialisieren der Anwendung, wie in der folgenden Abbildung dargestellt. Genau wie hier erfolgt, hängt mit der Anwendung.  
  
 ![Initialisieren einer ODBC-Anwendung zeigt](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 An diesem Punkt ist es üblich, dass verwendet **SQLGetInfo** ermitteln Sie die Funktionen des Treibers. Weitere Informationen finden Sie unter [Datenbankfunktionen in Betracht ziehen, zu verwendende](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Alle Anwendungen müssen ein Anweisungshandle mit zuordnen **SQLAllocHandle**, und legen Sie viele Clientanwendungen Anweisungsattribute, z. B. der Cursortyp mit **SQLSetStmtAttr**. Weitere Informationen finden Sie unter [ein Anweisungshandle zuordnen](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) und [Anweisungsattribute](../../../odbc/reference/develop-app/statement-attributes.md).
