---
title: Ablaufverfolgungs-Quelldatei | Microsoft Docs
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
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5c6c58e297e862d0e2241fe216dc7eb82bd4238
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="trace-file"></a>Ablaufverfolgungsdatei
Eine Anwendung gibt der Ablaufverfolgungsdatei durch Festlegen der **TraceFile** Schlüsselwort im Registrierungseintrag Odbc.ini oder durch Aufrufen von **SQLSetConnectAttr** mit SQL_ATTR_TRACEFILE-Verbindungsattribut. Wenn die Datei nicht vorhanden ist, wenn Ablaufverfolgung aktiviert ist, wird der Treiber-Manager die Datei erstellt. Jede Anwendung, müssen einen eigenen dedizierten Ablaufverfolgungsdatei, um Konflikte zu vermeiden. Eine Anwendung kann mehr als eine Ablaufverfolgungsdatei verwenden; Setup-Programm für eine Anwendung kann der Benutzer mithilfe einer Auswahl von Ablaufverfolgungsdateien bereitstellen. Ablaufverfolgung dynamisch aktiviert ist, kann eine Anwendung auch Ablaufverfolgungsergebnisse, anstatt die Protokollierung zu der Ablaufverfolgungsdatei angezeigt.  
  
 Die Ablaufverfolgungsdatei enthält ein Protokoll von jeder ODBC-Funktionsaufruf mit den Datentypen und Werte für alle Argumente. Er protokolliert den Funktionen für alle Eingabe und alle zurückgegebene Funktionen mit Rückgabecodes und Fehlerzustände protokolliert.  
  
 In ODBC 3.*.x*, Parameter, Verbindungsfunktionen werden nicht bereitgestellt, um die Trace-DLL.
