---
title: Erstellen und Beenden von Threads | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 62950dba2174baac8e3bc34c60f268e07304fa5a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="creating-and-terminating-threads"></a>Erstellen und Beenden von Threads
Multithreadanwendungen, die ODBC verwenden, sollten die Microsoft® Visual C++®-Laufzeitbibliotheksfunktionen aufrufen **_beginthread** und **_endthread** (oder **_beginthreadex** und **_endthreadex**) zum Erstellen und Beenden von Threads, die den ODBC-Treiber-Manager aufrufen. Wenn die Anwendungen die Microsoft Windows NT®-Funktionen aufrufen **CreateThread** und **EndThread** stattdessen prüfen auf Speicherverluste tritt auf, da der Treiber-Manager und einige ODBC-Treiber Aufrufen von C-Laufzeit Arbeitsspeicher-Funktionen, funktioniert nicht in einem Thread erstellt, durch den Aufruf **CreateThread**. Weitere Informationen finden Sie unter der Microsoft Windows®-Dokumentation.
