---
title: Multithreading | Microsoft Docs
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
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 822dcc213a28211a15a07e1bb4586c8a14f7cdd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="multithreading"></a>Multithreading
Bei multithread-Betriebssystemen müssen Treiber threadsicher sein. Also muss es möglich, dass Anwendungen in mehr als einem Thread dasselbe Handle zu verwenden. Treiberspezifische wird dies erreicht wird, und es ist wahrscheinlich, dass Treiber alle Versuche serialisiert, dasselbe Handle in zwei verschiedenen Threads gleichzeitig verwendet werden können.  
  
 Anwendungen verwenden im Allgemeinen mehrere Threads, anstatt die asynchrone Verarbeitung. Die Anwendung erstellt einen separaten Thread, eine ODBC-Funktionsaufrufe darauf und Verarbeitung im Hauptthread fortgesetzt. Anstatt kontinuierlich abrufen, die asynchrone-Funktion, wie der Fall ist, wenn das Anweisungsattribut SQL_ATTR_ASYNC_ENABLE verwendet wird, kann die Anwendung einfach den neu erstellten Thread beenden lassen.  
  
 Funktionen, die ein Anweisungshandle akzeptieren und in einem Thread ausgeführt werden können abgebrochen werden, durch Aufrufen von **SQLCancel** mit der gleichen Anweisung von einem anderen Thread zu behandeln. Obwohl Treiber nicht die Verwendung von serialisieren sollen **SQLCancel** auf diese Weise besteht keine Garantie, dass der Aufruf **SQLCancel** wird tatsächlich abgebrochen. die Funktion, die auf dem anderen Thread ausgeführt wird.
