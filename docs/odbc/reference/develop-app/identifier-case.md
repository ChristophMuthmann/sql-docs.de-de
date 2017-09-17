---
title: "Die Groß-/Kleinschreibung Bezeichner | Microsoft Docs"
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
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c55118fa47337425e715a8b3d6409525668e383f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="identifier-case"></a>Bezeichner Groß-/Kleinschreibung
In SQL-Anweisungen und Argumente für Katalog-Funktion, Bezeichner und Bezeichner in Anführungszeichen können es sich um Groß-/Kleinschreibung oder nicht, die eine Anwendung durch Aufrufen von ermitteln kann **SQLGetInfo** mit dem SQL_IDENTIFIER_CASE und SQL_QUOTED_ IDENTIFIER_CASE-Optionen.  
  
 Jede dieser Optionen hat vier mögliche Rückgabewerte: eine besagt, dass die Bezeichner oder Bezeichner in Anführungszeichen Groß-/Kleinschreibung beachtet wird, und drei besagt, dass er nicht vertraulich ist. Die drei Werte, die nicht zwischen Groß-und Kleinschreibung erläutern die Groß-/Kleinschreibung, in der Bezeichner im Systemkatalog gespeichert werden. Wie die Bezeichner im Systemkatalog gespeichert werden spielt nur zu Anzeigezwecken, z. B. wenn eine Anwendung die Ergebnisse von eine Katalogfunktion anzeigt; Es ändert sich nicht auf die Unterscheidung von Bezeichnern.
