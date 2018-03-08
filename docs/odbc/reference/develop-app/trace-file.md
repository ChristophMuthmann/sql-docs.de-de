---
title: Ablaufverfolgungs-Quelldatei | Microsoft Docs
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
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f14ddeafa35a91dc73a9540a63de805a2e16242f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="trace-file"></a>Ablaufverfolgungsdatei
Eine Anwendung gibt der Ablaufverfolgungsdatei durch Festlegen der **TraceFile** Schlüsselwort im Registrierungseintrag Odbc.ini oder durch Aufrufen von **SQLSetConnectAttr** mit SQL_ATTR_TRACEFILE-Verbindungsattribut. Wenn die Datei nicht vorhanden ist, wenn Ablaufverfolgung aktiviert ist, wird der Treiber-Manager die Datei erstellt. Jede Anwendung, müssen einen eigenen dedizierten Ablaufverfolgungsdatei, um Konflikte zu vermeiden. Eine Anwendung kann mehr als eine Ablaufverfolgungsdatei verwenden; Setup-Programm für eine Anwendung kann der Benutzer mithilfe einer Auswahl von Ablaufverfolgungsdateien bereitstellen. Ablaufverfolgung dynamisch aktiviert ist, kann eine Anwendung auch Ablaufverfolgungsergebnisse, anstatt die Protokollierung zu der Ablaufverfolgungsdatei angezeigt.  
  
 Die Ablaufverfolgungsdatei enthält ein Protokoll von jeder ODBC-Funktionsaufruf mit den Datentypen und Werte für alle Argumente. Er protokolliert den Funktionen für alle Eingabe und alle zurückgegebene Funktionen mit Rückgabecodes und Fehlerzustände protokolliert.  
  
 In ODBC 3.*.x*, Parameter, Verbindungsfunktionen werden nicht bereitgestellt, um die Trace-DLL.
