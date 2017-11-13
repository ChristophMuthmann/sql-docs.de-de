---
title: SQLGetDiagField aufrufen | Microsoft Docs
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
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2d19805c12075a9d8961e161070b8c95ae08be89
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlgetdiagfield"></a>SQLGetDiagField aufrufen
Wenn eine ODBC-3. *x* Anwendung ruft **SQLGetDiagField** in einer ODBC 2.*.x* Treiber, der Treiber gibt SQL_SUCCESS zurück, und die entsprechenden Informationen im zurück  *\*DiagInfoPtr* Wenn die *DiagIdentifier* Argument ist SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_ Anzahl, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME oder SQL_DIAG_SQLSTATE. Alle anderen Diagnosefelder gibt SQL_ERROR zurück.

