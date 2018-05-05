---
title: Aktualisieren, löschen oder Abrufen von Lesezeichen | Microsoft Docs
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
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9b919d30d604410a30ae4c844471c1557b6a2a9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Aktualisieren, löschen oder Abrufen von Lesezeichen
Lesezeichen können verwendet werden, um Daten im Resultset, das Ergebnis festgelegt oder abgerufen werden, aus dem Resultset in die Rowset-Puffer gelöscht aktualisiert werden zu identifizieren. Diese Vorgänge werden ausgeführt, durch den Aufruf von **SQLBulkOperations** mit einem *Option* Argument SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK oder SQL_FETCH_BY_BOOKMARK. Die Lesezeichen, die bei diesen Vorgängen verwendet werden in der Spalte 0 der Rowset-Puffer gespeichert. Bei der Aktualisierung von Lesezeichen werden die Daten, die Spalten ergeben aktualisiert, wird von den Puffern Rowset abgerufen. Weitere Informationen finden Sie unter [Aktualisieren von Daten mit SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
