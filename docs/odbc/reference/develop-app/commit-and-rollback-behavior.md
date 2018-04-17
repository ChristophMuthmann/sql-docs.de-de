---
title: Commit- und Rollback-Verhalten | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 326ce5cdeb29fbc402a980e99429d1b3dd36b1d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="commit-and-rollback-behavior"></a>Commit- und Rollback-Verhalten
Ein gemeinsames Verhalten zwischen Server DBMS werden Cursor geschlossen, und vorbereitete Anweisungen zu verwerfen, wenn eine Anweisung ein Commit oder Rollback ab. Desktopdatenbanken sind eher Cursor geöffnet ist und Beibehalten von vorbereiteten Anweisungen. Weitere Informationen finden Sie unter der SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR Optionen in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung und [Auswirkungen von Transaktionen für Cursor und vorbereitete Anweisungen](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
