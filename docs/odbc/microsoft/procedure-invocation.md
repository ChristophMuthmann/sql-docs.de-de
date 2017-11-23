---
title: Prozeduraufruf | Microsoft Docs
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
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 793209ab716d720266e834fcbbb846dea56950ed
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="procedure-invocation"></a>Prozeduraufruf
Wenn der Microsoft Access-Treiber verwendet wird, können Prozeduren aus dem Treiber aufgerufen werden, mithilfe der **SQLExecDirect** oder **SQLPrepare** -Funktion mit der folgenden Syntax: {Aufrufen *Prozedurnamen*  [(*Parameter*[,*Parameter*]...)]}. Beachten Sie, dass Ausdrücke als Parameter für eine aufgerufene Prozedur nicht unterstützt werden.  
  
 Wenn eine Prozedurnamens einen Bindestrich enthält, muss der Name mit Back Anführungszeichen (') getrennt werden.  
  
 Eine parametrisierte Abfrage kann mit der vorherigen Anweisung aufgerufen werden.
