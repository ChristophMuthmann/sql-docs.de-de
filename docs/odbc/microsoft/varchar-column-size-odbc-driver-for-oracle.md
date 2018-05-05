---
title: VARCHAR Spaltengröße (ODBC-Treiber für Oracle) | Microsoft Docs
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
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02e02b9faf3bd19665536e141884bd663ad64266
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR Spaltengröße (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 In 8 hat die maximale Größe einer Spalte VARCHAR von 2000 auf 4.000 Byte erhöht. Die Oracle-Clientsoftware 7.3.x hat keine Möglichkeit zum Binden eines Parameterwert, der größer als 2000 Bytes. Daher bei der Erstellung einer Tabellenstatus mit einer VARCHAR-Spalte von mehr als 2000 Bytes werden Sie zum Ausführen von parametrisierten einfügungen, Updates, löscht und Abfragen dafür mit Daten, die das 2000-Byte-Grenze der Clientsoftware überschreitet. Da sowohl die ODBC-Treiber für Oracle der OLE DB-Anbieter für Oracle verwenden parametrisierte Einfügevorgänge, Updates, löschungen und Abfragen, werden sie in diesem Fall ORA-01026 Fehler gemeldet. Daten, die innerhalb der Beschränkungen, die von der Oracle-Clientsoftware funktioniert. Um diese 2000-Byte-Grenze zu vermeiden, müssen Sie die Clientsoftware auf 8 aktualisieren (8.0.4.1.1c oder höher).
