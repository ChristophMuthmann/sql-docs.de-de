---
title: Threadsicherheit Hinweise auf API-Funktionen (ODBC-Treiber für Oracle) | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a99ddfed60ebb9d7d8dcfd4215b7c0a8d57314fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Threadsicherheit Hinweise auf API-Funktionen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Der Microsoft ODBC-Treiber für Oracle ist threadsicher. Oracle lässt jedoch nicht mehrere gleichzeitige Anweisungen über eine einzelne Verbindung. Der Treiber erzwingt diese Einschränkung. In anderen Worten: Obwohl einen beliebigen Thread zu einem beliebigen Zeitpunkt in der ODBC-Treiber für Oracle aufrufen kann blockiert, in Multithreadanwendungen verwendet werden können, der Treiber ein anderen Threads aus dem Treiber auf die gleiche Verbindung bis der ursprüngliche Thread bewirkt, den Treiber dass.  
  
 Wenn zwei Anweisungen für zwei unterschiedliche Verbindungen blockiert der Treiber nicht. Ist eine einzelne Verbindung mit zwei Anweisungen, ist es jedoch zum Blockieren von potenziellen.
