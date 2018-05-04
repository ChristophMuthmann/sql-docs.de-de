---
title: Nur-Lese Status (Excel-Treiber) | Microsoft Docs
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
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0cdfec3129dbe01e5b25f0c8595b8bd4e528ba8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="read-only-status-excel-driver"></a>Nur-Lese Status (Excel-Treiber)
Wenn der Microsoft Excel-Treiber verwendet wird, Daten-Quelltabellen werden standardmäßig als schreibgeschützt geöffnet und können jeweils nur ein einziger Benutzer geöffnet werden. Auch wenn Tabellen schreibgeschützten Status aufweisen, können jedoch Anwendungen einfügungen und Updates für Microsoft Excel-Tabellen ausführen.  
  
 Wenn eine Anwendung einen Befehl Speichern unter für Microsoft Excel-Daten über den Microsoft Excel-Treiber ausführt, sollte die Anwendung eine neue Tabelle erstellen und fügen Sie die Daten in die neue Tabelle gespeichert werden sollen. Fügt ein Anfügen auf die Tabelle resultieren. Für die Tabelle können keine anderen Vorgänge ausgeführt werden, bis er geschlossen und erneut geöffnet wird. Nachdem die Tabelle geschlossen wurde, kann keine nachfolgenden einfügungen ausgeführt werden, da die Tabelle dann schreibgeschützt ist.  
  
 Es ist möglich, Werte zu aktualisieren, wenn der Microsoft Excel-Treiber verwendet, aber eine Zeile kann nicht gelöscht werden, aus einer Tabelle basierend auf einer Microsoft Excel-Arbeitsblatt, damit die Updates nicht berücksichtigt werden offiziell von Microsoft Excel-Treiber unterstützt.
