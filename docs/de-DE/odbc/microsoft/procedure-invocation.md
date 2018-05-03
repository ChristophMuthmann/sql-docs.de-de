---
title: Prozeduraufruf | Microsoft Docs
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
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d01859ee1b44f29c1109e976cc4a59302306444
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-invocation"></a>Prozeduraufruf
Wenn der Microsoft Access-Treiber verwendet wird, können Prozeduren aus dem Treiber aufgerufen werden, mithilfe der **SQLExecDirect** oder **SQLPrepare** -Funktion mit der folgenden Syntax: {Aufrufen *Prozedurnamen*  [(*Parameter*[,*Parameter*]...)]}. Beachten Sie, dass Ausdrücke als Parameter für eine aufgerufene Prozedur nicht unterstützt werden.  
  
 Wenn eine Prozedurnamens einen Bindestrich enthält, muss der Name mit Back Anführungszeichen (') getrennt werden.  
  
 Eine parametrisierte Abfrage kann mit der vorherigen Anweisung aufgerufen werden.
