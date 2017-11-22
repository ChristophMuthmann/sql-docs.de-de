---
title: Erstellen und Beenden von Threads | Microsoft Docs
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
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1035c59acfaa8c28582751b7c4d97b1d02cce920
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="creating-and-terminating-threads"></a>Erstellen und Beenden von Threads
Multithreadanwendungen, die ODBC verwenden, sollten die Microsoft® Visual C++®-Laufzeitbibliotheksfunktionen aufrufen **_beginthread** und **_endthread** (oder **_beginthreadex** und **_endthreadex**) zum Erstellen und Beenden von Threads, die den ODBC-Treiber-Manager aufrufen. Wenn die Anwendungen die Microsoft Windows NT®-Funktionen aufrufen **CreateThread** und **EndThread** stattdessen prüfen auf Speicherverluste tritt auf, da der Treiber-Manager und einige ODBC-Treiber Aufrufen von C-Laufzeit Arbeitsspeicher-Funktionen, funktioniert nicht in einem Thread erstellt, durch den Aufruf **CreateThread**. Weitere Informationen finden Sie unter der Microsoft Windows®-Dokumentation.
