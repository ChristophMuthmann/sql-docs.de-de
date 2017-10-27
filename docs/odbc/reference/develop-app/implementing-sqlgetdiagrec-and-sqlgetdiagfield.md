---
title: Implementieren von SQLGetDiagRec und SQLGetDiagField | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 463ddfe552c94a9e90ceb2a24f8061674955979d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementieren von SQLGetDiagRec und SQLGetDiagField
**SQLGetDiagRec** und **SQLGetDiagField** werden von der Treiber-Manager und jeden Treiber implementiert. Der Treiber-Manager jeden Treiber DiagnoseDatensätze für jede Umgebung, die Verbindung, die-Anweisung und die Deskriptorhandles verwalten und diese Datensätze freigeben, nur, wenn Sie mit einer anderen Funktion aufgerufen wird, dass Handle oder das Handle freigegeben wird.  
  
 Obwohl der Treiber-Manager und jeden Treiber entsprechend die Rangfolgen in den ersten Status-Datensatz festlegen müssen [Sequenz Statusdatensätze](../../../odbc/reference/develop-app/sequence-of-status-records.md), der Treiber-Manager bestimmt die endgültige Reihenfolge der Datensätze.  
  
 **SQLGetDiagRec** und **SQLGetDiagField** Diagnosedatensätzen über sich selbst nicht gesendet.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Diagnose Behandlung Regeln](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Rolle des Treiber-Managers](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Rolle des Treibers ""](../../../odbc/reference/develop-app/role-of-the-driver.md)

