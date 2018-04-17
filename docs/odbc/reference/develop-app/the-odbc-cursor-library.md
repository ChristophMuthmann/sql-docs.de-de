---
title: Der ODBC-Cursorbibliothek | Microsoft Docs
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
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e1d6f7c6e532622d8bd0ee8fb637754f5df19429
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="the-odbc-cursor-library"></a>Der ODBC-Cursorbibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Blocks und bildlauffähigen Cursorn sind sehr nützlich Ergänzungen viele Anwendungen. Allerdings unterstützt nicht alle Treiber Blocks und bildlauffähigen Cursorn. Dasselbe gilt auch für positionierte Update und delete-Anweisungen und **SQLSetPos**, werden die im Aktualisieren von Daten erläutert. Deshalb enthält die ODBC-Komponente des Windows SDK, früher im Microsoft Data Access Components (MDAC) SDK, enthalten eine Cursorbibliothek. Die Cursorbibliothek implementiert Block, statische Cursor, positionierte Update- und Delete-Anweisungen und **SQLSetPos** für alle Treiber, der den Standard Open Group-CLI-Konformitätsgrad erfüllt. Die Cursorbibliothek kann mit ODBC-Anwendungen verteilt werden. finden Sie unter den Lizenzvertrag im SDK für Weitere Informationen.  
  
 Für die Verwendung die Cursorbibliothek setzt eine Anwendung das SQL_ATTR_ODBC_CURSORS-Verbindungsattribut auf, bevor sie mit der Datenquelle eine Verbindung hergestellt. Weitere Informationen über die Cursorbibliothek finden Sie unter [Anhang F: ODBC-Cursorbibliothek](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
