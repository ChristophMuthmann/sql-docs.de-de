---
title: Arithmetischen Fehler | Microsoft Docs
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
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e52d0edb1704df3e4085e417493fd68b7a7af977
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="arithmetic-errors"></a>Arithmetischen Fehler
Der ODBC-Treiber ergibt die WHERE-Klausel in einer SELECT-Anweisung, wie jede Zeile abgerufen. Wenn eine Zeile einen Wert enthält, der einen arithmetischen Fehler, z. B. aufgrund einer Division durch null oder numerischen Überlauf bewirkt, dass der Treiber gibt alle Zeilen zurück, gibt jedoch Fehler für Spalten mit arithmetischen Fehlern. Beim Einfügen oder aktualisieren, beendet jedoch der ODBC-Treiber, einfügen oder Aktualisieren von Daten, wenn die erste arithmetische Fehler aufgetreten ist.
