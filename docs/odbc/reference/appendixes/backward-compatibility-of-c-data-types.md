---
title: "Abwärtskompatibilität von C-Datentypen | Microsoft Docs"
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
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24d0c05a7410a3db37718ebaa667abbb01072796
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="backward-compatibility-of-c-data-types"></a>Abwärtskompatibilität von C-Datentypen
SQL_C_SHORT, SQL_C_LONG und SQL_C_TINYINT wurden in ODBC durch ersetzt mit und ohne Vorzeichen Typen: SQL_C_SSHORT und SQL_C_USHORT, SQL_C_SLONG und SQL_C_ULONG, und SQL_C_STINYINT und SQL_C_UTINYINT. Eine ODBC 3.*.x* Treiber, die mit ODBC 2. arbeiten sollten. *X* Anwendungen sollten SQL_C_SHORT, SQL_C_LONG und SQL_C_TINYINT, unterstützt, da bei der sie aufgerufen werden, der Treiber-Manager über den Treiber übergibt.

