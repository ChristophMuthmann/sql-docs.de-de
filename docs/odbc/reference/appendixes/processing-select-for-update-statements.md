---
title: "Wählen Sie für die UPDATE-Anweisungen verarbeiten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c065a3194e492d7f05bae4b857eda293aa523cd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="processing-select-for-update-statements"></a>Wählen Sie für die UPDATE-Anweisungen verarbeiten
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Für eine optimale Interoperabilität sollte Anwendungen generieren Resultsets, die durch das Ausführen mit einer positioniertes Update-Anweisung aktualisiert werden, eine **für aktualisieren wählen** Anweisung. Obwohl die Cursorbibliothek dies nicht erforderlich ist, ist es die meisten Datenquellen erforderlich, die positionierte Update-Anweisungen unterstützen.  
  
 Die Cursorbibliothek ignoriert die Spalten in der **FOR UPDATE** -Klausel einer **SELECT FOR UPDATE** -Anweisung vor der Anweisung an den Treiber übergeben diese Klausel wird entfernt. In der Cursorbibliothek SQL_ATTR_CONCURRENCY-Anweisungsattribut, zusammen mit den Einschränkungen, die im vorherigen Abschnitt erwähnten können Steuerelemente, ob die Spalten in einem Resultset aktualisiert werden.
