---
title: Implementieren von SQLGetDiagRec und SQLGetDiagField | Microsoft Docs
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
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d757e4addf483690e491a71d2f7094aa3d9ad116
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementieren von SQLGetDiagRec und SQLGetDiagField
**SQLGetDiagRec** und **SQLGetDiagField** werden von der Treiber-Manager und jeden Treiber implementiert. Der Treiber-Manager jeden Treiber DiagnoseDatensätze für jede Umgebung, die Verbindung, die-Anweisung und die Deskriptorhandles verwalten und diese Datensätze freigeben, nur, wenn Sie mit einer anderen Funktion aufgerufen wird, dass Handle oder das Handle freigegeben wird.  
  
 Obwohl der Treiber-Manager und jeden Treiber entsprechend die Rangfolgen in den ersten Status-Datensatz festlegen müssen [Sequenz Statusdatensätze](../../../odbc/reference/develop-app/sequence-of-status-records.md), der Treiber-Manager bestimmt die endgültige Reihenfolge der Datensätze.  
  
 **SQLGetDiagRec** und **SQLGetDiagField** Diagnosedatensätzen über sich selbst nicht gesendet.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Regeln der Diagnosebehandlung](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Rolle des Treiber-Managers](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Rolle des Treibers](../../../odbc/reference/develop-app/role-of-the-driver.md)
