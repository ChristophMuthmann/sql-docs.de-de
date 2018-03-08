---
title: Prozeduraufruf | Microsoft Docs
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
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10af4e60b9fb30e8030d31f80c93681e73375e1e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="procedure-invocation"></a>Prozeduraufruf
Wenn der Microsoft Access-Treiber verwendet wird, können Prozeduren aus dem Treiber aufgerufen werden, mithilfe der **SQLExecDirect** oder **SQLPrepare** -Funktion mit der folgenden Syntax: {Aufrufen *Prozedurnamen*  [(*Parameter*[,*Parameter*]...)]}. Beachten Sie, dass Ausdrücke als Parameter für eine aufgerufene Prozedur nicht unterstützt werden.  
  
 Wenn eine Prozedurnamens einen Bindestrich enthält, muss der Name mit Back Anführungszeichen (') getrennt werden.  
  
 Eine parametrisierte Abfrage kann mit der vorherigen Anweisung aufgerufen werden.
