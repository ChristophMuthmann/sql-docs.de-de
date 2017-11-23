---
title: Der ODBC-Cursorbibliothek | Microsoft Docs
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
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96b3b09306c9e91b883fbb32b1fcc26afc53e315
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="the-odbc-cursor-library"></a>Der ODBC-Cursorbibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Blocks und bildlauffähigen Cursorn sind sehr nützlich Ergänzungen viele Anwendungen. Allerdings unterstützt nicht alle Treiber Blocks und bildlauffähigen Cursorn. Dasselbe gilt auch für positionierte Update und delete-Anweisungen und **SQLSetPos**, werden die im Aktualisieren von Daten erläutert. Deshalb enthält die ODBC-Komponente des Windows SDK, früher im Microsoft Data Access Components (MDAC) SDK, enthalten eine Cursorbibliothek. Die Cursorbibliothek implementiert Block, statische Cursor, positionierte Update- und Delete-Anweisungen und **SQLSetPos** für alle Treiber, der den Standard Open Group-CLI-Konformitätsgrad erfüllt. Die Cursorbibliothek kann mit ODBC-Anwendungen verteilt werden. finden Sie unter den Lizenzvertrag im SDK für Weitere Informationen.  
  
 Für die Verwendung die Cursorbibliothek setzt eine Anwendung das SQL_ATTR_ODBC_CURSORS-Verbindungsattribut auf, bevor sie mit der Datenquelle eine Verbindung hergestellt. Weitere Informationen über die Cursorbibliothek finden Sie unter [Anhang F: ODBC-Cursorbibliothek](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
