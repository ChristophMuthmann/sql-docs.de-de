---
title: "VARCHAR Spaltengröße (ODBC-Treiber für Oracle) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fdd09067b2a938a285264955ad0ff05c6455c00a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR Spaltengröße (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 In 8 hat die maximale Größe einer Spalte VARCHAR von 2000 auf 4.000 Byte erhöht. Die Oracle-Clientsoftware 7.3.x hat keine Möglichkeit zum Binden eines Parameterwert, der größer als 2000 Bytes. Daher bei der Erstellung einer Tabellenstatus mit einer VARCHAR-Spalte von mehr als 2000 Bytes werden Sie zum Ausführen von parametrisierten einfügungen, Updates, löscht und Abfragen dafür mit Daten, die das 2000-Byte-Grenze der Clientsoftware überschreitet. Da sowohl die ODBC-Treiber für Oracle der OLE DB-Anbieter für Oracle verwenden parametrisierte Einfügevorgänge, Updates, löschungen und Abfragen, werden sie in diesem Fall ORA-01026 Fehler gemeldet. Daten, die innerhalb der Beschränkungen, die von der Oracle-Clientsoftware funktioniert. Um diese 2000-Byte-Grenze zu vermeiden, müssen Sie die Clientsoftware auf 8 aktualisieren (8.0.4.1.1c oder höher).
