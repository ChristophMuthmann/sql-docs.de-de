---
title: SQLGetDiagField aufrufen | Microsoft Docs
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
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 323aea923a4f7763d849367493b481262cd3b59d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlgetdiagfield"></a>SQLGetDiagField aufrufen
Wenn eine ODBC-3. *x* Anwendung ruft **SQLGetDiagField** in einer ODBC 2.*.x* Treiber, der Treiber gibt SQL_SUCCESS zurück, und die entsprechenden Informationen im zurück  *\*DiagInfoPtr* Wenn die *DiagIdentifier* Argument ist SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_ Anzahl, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME oder SQL_DIAG_SQLSTATE. Alle anderen Diagnosefelder gibt SQL_ERROR zurück.
