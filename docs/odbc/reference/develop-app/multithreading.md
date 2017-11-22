---
title: Multithreading | Microsoft Docs
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
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 86ef8e539354dce2d0cd349d75053b05a7ca59ca
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="multithreading"></a>Multithreading
Bei multithread-Betriebssystemen müssen Treiber threadsicher sein. Also muss es möglich, dass Anwendungen in mehr als einem Thread dasselbe Handle zu verwenden. Treiberspezifische wird dies erreicht wird, und es ist wahrscheinlich, dass Treiber alle Versuche serialisiert, dasselbe Handle in zwei verschiedenen Threads gleichzeitig verwendet werden können.  
  
 Anwendungen verwenden im Allgemeinen mehrere Threads, anstatt die asynchrone Verarbeitung. Die Anwendung erstellt einen separaten Thread, eine ODBC-Funktionsaufrufe darauf und Verarbeitung im Hauptthread fortgesetzt. Anstatt kontinuierlich abrufen, die asynchrone-Funktion, wie der Fall ist, wenn das Anweisungsattribut SQL_ATTR_ASYNC_ENABLE verwendet wird, kann die Anwendung einfach den neu erstellten Thread beenden lassen.  
  
 Funktionen, die ein Anweisungshandle akzeptieren und in einem Thread ausgeführt werden können abgebrochen werden, durch Aufrufen von **SQLCancel** mit der gleichen Anweisung von einem anderen Thread zu behandeln. Obwohl Treiber nicht die Verwendung von serialisieren sollen **SQLCancel** auf diese Weise besteht keine Garantie, dass der Aufruf **SQLCancel** wird tatsächlich abgebrochen. die Funktion, die auf dem anderen Thread ausgeführt wird.
