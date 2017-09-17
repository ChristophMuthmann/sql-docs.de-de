---
title: Commit- und Rollback-Verhalten | Microsoft Docs
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7bf7e756c77ceef96502fdacc078b4780f01ce86
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="commit-and-rollback-behavior"></a>Commit- und Rollback-Verhalten
Ein gemeinsames Verhalten zwischen Server DBMS werden Cursor geschlossen, und vorbereitete Anweisungen zu verwerfen, wenn eine Anweisung ein Commit oder Rollback ab. Desktopdatenbanken sind eher Cursor geöffnet ist und Beibehalten von vorbereiteten Anweisungen. Weitere Informationen finden Sie unter der SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR Optionen in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung und [Auswirkungen von Transaktionen für Cursor und vorbereitete Anweisungen](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
