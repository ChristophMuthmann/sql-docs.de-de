---
title: Erstellen und Beenden von Threads | Microsoft Docs
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
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92f69906811791a56134094fb4b05859763d1624
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="creating-and-terminating-threads"></a>Erstellen und Beenden von Threads
Multithreadanwendungen, die ODBC verwenden, sollten die Microsoft® Visual C++®-Laufzeitbibliotheksfunktionen aufrufen **_beginthread** und **_endthread** (oder **_beginthreadex** und **_endthreadex**) zum Erstellen und Beenden von Threads, die den ODBC-Treiber-Manager aufrufen. Wenn die Anwendungen die Microsoft Windows NT®-Funktionen aufrufen **CreateThread** und **EndThread** stattdessen prüfen auf Speicherverluste tritt auf, da der Treiber-Manager und einige ODBC-Treiber Aufrufen von C-Laufzeit Arbeitsspeicher-Funktionen, funktioniert nicht in einem Thread erstellt, durch den Aufruf **CreateThread**. Weitere Informationen finden Sie unter der Microsoft Windows®-Dokumentation.
