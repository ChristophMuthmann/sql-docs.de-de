---
title: Thread-Unterstützung (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e93bfc712c7f06ce239a7425a12ba3498291e385
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Thread-Unterstützung (Visual FoxPro-ODBC-Treiber)
Der Visual FoxPro-ODBC-Treiber ist threadsicher. Zugriff auf Umgebungshandles (*enn*), Verbindungshandles (*Hdbc*), und Anweisungshandles (*Befehls beschäftigt*) wird in der entsprechenden Semaphoren, um zu verhindern, dass andere Prozesse eingebunden auf zugreifen und möglicherweise ändern internen Datenstrukturen des Treibers.  
  
 In einer Multithreadanwendung können Sie eine Funktion, die synchron mit läuft Abbrechen einer *Befehls beschäftigt* durch Aufrufen von [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) in einem separaten Thread.  
  
 Der Treiber verwendet einen separaten Thread zum Abrufen von Daten bei Verwendung von progressiven abrufen. Um progressive Abrufen von Zeilen für eine Datenquelle zu verwenden, wählen Sie die **Abrufen von Daten im Hintergrund** Kontrollkästchen auf der [ODBC Visual FoxPro einrichten (Dialogfeld)](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) , oder verwenden Sie das Schlüsselwort der BackgroundFetch-Attribut in der Verbindungszeichenfolge Zeichenfolge. Verwenden Sie abrufen im Hintergrund beim Aufrufen des Treibers von Multithreadanwendungen verwendet werden können. Informationen über Schlüsselwörter für Verbindungszeichenfolgen-Attribut finden Sie unter [Verbindungszeichenfolgen verwenden](../../odbc/microsoft/using-connection-strings.md).  
  
 Weitere Informationen zu Threads und **SQLCancel**, finden Sie unter [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) in der *ODBC Programmer's Reference*.
