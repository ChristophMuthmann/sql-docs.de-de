---
title: Wählen Sie für die UPDATE-Anweisungen verarbeiten | Microsoft Docs
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
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ede999422f6b52112356aa7c9c4b7715eafb96c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="processing-select-for-update-statements"></a>Wählen Sie für die UPDATE-Anweisungen verarbeiten
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Für eine optimale Interoperabilität sollte Anwendungen generieren Resultsets, die durch das Ausführen mit einer positioniertes Update-Anweisung aktualisiert werden, eine **für aktualisieren wählen** Anweisung. Obwohl die Cursorbibliothek dies nicht erforderlich ist, ist es die meisten Datenquellen erforderlich, die positionierte Update-Anweisungen unterstützen.  
  
 Die Cursorbibliothek ignoriert die Spalten in der **FOR UPDATE** -Klausel einer **SELECT FOR UPDATE** -Anweisung vor der Anweisung an den Treiber übergeben diese Klausel wird entfernt. In der Cursorbibliothek SQL_ATTR_CONCURRENCY-Anweisungsattribut, zusammen mit den Einschränkungen, die im vorherigen Abschnitt erwähnten können Steuerelemente, ob die Spalten in einem Resultset aktualisiert werden.
