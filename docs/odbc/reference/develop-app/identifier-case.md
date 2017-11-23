---
title: "Die Groß-/Kleinschreibung Bezeichner | Microsoft Docs"
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
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17c1d7658b313860fdc3abfe0c756a38046dbfc4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="identifier-case"></a>Bezeichner Groß-/Kleinschreibung
In SQL-Anweisungen und Argumente für Katalog-Funktion, Bezeichner und Bezeichner in Anführungszeichen können es sich um Groß-/Kleinschreibung oder nicht, die eine Anwendung durch Aufrufen von ermitteln kann **SQLGetInfo** mit dem SQL_IDENTIFIER_CASE und SQL_QUOTED_ IDENTIFIER_CASE-Optionen.  
  
 Jede dieser Optionen hat vier mögliche Rückgabewerte: eine besagt, dass die Bezeichner oder Bezeichner in Anführungszeichen Groß-/Kleinschreibung beachtet wird, und drei besagt, dass er nicht vertraulich ist. Die drei Werte, die nicht zwischen Groß-und Kleinschreibung erläutern die Groß-/Kleinschreibung, in der Bezeichner im Systemkatalog gespeichert werden. Wie die Bezeichner im Systemkatalog gespeichert werden spielt nur zu Anzeigezwecken, z. B. wenn eine Anwendung die Ergebnisse von eine Katalogfunktion anzeigt; Es ändert sich nicht auf die Unterscheidung von Bezeichnern.
