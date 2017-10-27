---
title: "VARCHAR Spaltengröße (ODBC-Treiber für Oracle) | Microsoft Docs"
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
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57dcc53769c9b5ba80f5c949436f0b3eb2ce08b1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR Spaltengröße (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 In 8 hat die maximale Größe einer Spalte VARCHAR von 2000 auf 4.000 Byte erhöht. Die Oracle-Clientsoftware 7.3.x hat keine Möglichkeit zum Binden eines Parameterwert, der größer als 2000 Bytes. Daher bei der Erstellung einer Tabellenstatus mit einer VARCHAR-Spalte von mehr als 2000 Bytes werden Sie zum Ausführen von parametrisierten einfügungen, Updates, löscht und Abfragen dafür mit Daten, die das 2000-Byte-Grenze der Clientsoftware überschreitet. Da sowohl die ODBC-Treiber für Oracle der OLE DB-Anbieter für Oracle verwenden parametrisierte Einfügevorgänge, Updates, löschungen und Abfragen, werden sie in diesem Fall ORA-01026 Fehler gemeldet. Daten, die innerhalb der Beschränkungen, die von der Oracle-Clientsoftware funktioniert. Um diese 2000-Byte-Grenze zu vermeiden, müssen Sie die Clientsoftware auf 8 aktualisieren (8.0.4.1.1c oder höher).

