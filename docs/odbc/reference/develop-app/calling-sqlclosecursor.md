---
title: SQLCloseCursor aufrufen | Microsoft Docs
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
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f0d8c7ccb49840ae9477fac5a002b94b79c98302
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor aufrufen
Da **SQLCloseCursor** ist nahezu identisch mit **SQLFreeStmt** mit SQL_CLOSE, führt der Treiber-Manager diese Funktion nicht zuordnen. Ersatzfunktionen werden zugeordnet, sodass vorhandene ODBC 2.*.x* Anwendungen können problemlos verschieben, um ODBC 3..* X* mit den neuen Funktionen. Eine solche Verschiebung erleichtert das für solche Anwendungen mit neuen ODBC 3. beginnen. *x* -Funktionen in bedingten Code modulare Weise. **SQLCloseCursor** stellt keinen keine neuen Funktionen dar. Eine Anwendung ist keine Vorteile erzielen, indem Sie die zu **SQLCloseCursor** aus **SQLFreeStmt** mit SQL_CLOSE.
