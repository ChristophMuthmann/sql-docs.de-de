---
title: Erstellen und Beenden von Threads | Microsoft Docs
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
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a30fbe976ac3de550f8067cca82732631f698ac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-terminating-threads"></a>Erstellen und Beenden von Threads
Multithreadanwendungen, die ODBC verwenden, sollten die Microsoft® Visual C++®-Laufzeitbibliotheksfunktionen aufrufen **_beginthread** und **_endthread** (oder **_beginthreadex** und **_endthreadex**) zum Erstellen und Beenden von Threads, die den ODBC-Treiber-Manager aufrufen. Wenn die Anwendungen die Microsoft Windows NT®-Funktionen aufrufen **CreateThread** und **EndThread** stattdessen prüfen auf Speicherverluste tritt auf, da der Treiber-Manager und einige ODBC-Treiber Aufrufen von C-Laufzeit Arbeitsspeicher-Funktionen, funktioniert nicht in einem Thread erstellt, durch den Aufruf **CreateThread**. Weitere Informationen finden Sie unter der Microsoft Windows®-Dokumentation.

