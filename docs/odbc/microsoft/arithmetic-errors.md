---
title: Arithmetischen Fehler | Microsoft Docs
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
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d3585f6e1be7a3f9451231004979321202d7852
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="arithmetic-errors"></a>Arithmetischen Fehler
Der ODBC-Treiber ergibt die WHERE-Klausel in einer SELECT-Anweisung, wie jede Zeile abgerufen. Wenn eine Zeile einen Wert enthält, der einen arithmetischen Fehler, z. B. aufgrund einer Division durch null oder numerischen Überlauf bewirkt, dass der Treiber gibt alle Zeilen zurück, gibt jedoch Fehler für Spalten mit arithmetischen Fehlern. Beim Einfügen oder aktualisieren, beendet jedoch der ODBC-Treiber, einfügen oder Aktualisieren von Daten, wenn die erste arithmetische Fehler aufgetreten ist.
