---
title: Ort des Caches | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78e4378e5895e68e8eeb461560faa88ef9cef837
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="location-of-cache"></a>Ort des Caches
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Die Cursorbibliothek werden Daten im Arbeitsspeicher und in temporären Dateien Windows® zwischengespeichert. Dies schränkt die Größe des Resultsets, die die Cursorbibliothek nur nach verfügbarem Speicherplatz verarbeiten kann. Eine temporäre Datei wird verwendet, wenn die Daten zwischengespeichert werden die Segment-Grenze Verzierung, wenn am Ende des Cursors Bibliothek Cache eingefügt. Stattdessen werden die Daten zwischengespeichert werden anstelle der zuletzt gespeicherten Block von Daten im Cache hinzugefügt. Der zuletzt gespeicherten Datenblock wird in einer temporären Datei gespeichert. Wenn die Cursorbibliothek fehlerbedingt beendet wird, z. B. wenn die Leistungsfähigkeit ein Fehler auftritt, können sie Windows temporäre Dateien auf dem Datenträger lassen. Diese heißen ~ CTT*Nnnn*TMP und sind im aktuellen Verzeichnis erstellt.  
  
> [!NOTE]  
>  Wenn die Cursorbibliothek in Microsoft® WindowsNT®/Windows2000 versucht zum Zwischenspeichern von Daten in einer temporären Datei für das aktuelle Verzeichnis während der Ausführung der Anwendung aus einer schreibgeschützten Freigabe oder einem Compact Disk-(z. B. ein Microsoft Foundation Class Library-Beispiel), SQLSTATE HY000 (Allgemein Error-Unable, erstellen Sie einen Dateipuffer) wird zurückgegeben.
