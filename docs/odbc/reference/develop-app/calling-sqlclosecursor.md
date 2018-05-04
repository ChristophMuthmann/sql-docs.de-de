---
title: SQLCloseCursor aufrufen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 5d574729d7fa49a65b26e067c54a0af459a36094
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor aufrufen
Da **SQLCloseCursor** ist nahezu identisch mit **SQLFreeStmt** mit SQL_CLOSE, führt der Treiber-Manager diese Funktion nicht zuordnen. Ersatzfunktionen werden zugeordnet, sodass vorhandene ODBC 2.*.x* Anwendungen können problemlos verschieben, um ODBC 3. *X* mit den neuen Funktionen. Eine solche Verschiebung erleichtert das für solche Anwendungen mit neuen ODBC 3. beginnen. *x* -Funktionen in bedingten Code modulare Weise. **SQLCloseCursor** stellt keinen keine neuen Funktionen dar. Eine Anwendung ist keine Vorteile erzielen, indem Sie die zu **SQLCloseCursor** aus **SQLFreeStmt** mit SQL_CLOSE.
