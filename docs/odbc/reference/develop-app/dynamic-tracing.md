---
title: Dynamische Tracing | Microsoft Docs
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
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ca4985388ef607becef285b8883f8ab24fbad78
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dynamic-tracing"></a>Dynamische Ablaufverfolgung
Ablaufverfolgung kann aktiviert oder deaktiviert werden, an einem beliebigen Punkt in einer Anwendung ausführen. Dabei kann es sich um eine Anwendung, um eine beliebige Anzahl von Funktionsaufrufen zu verfolgen.  
  
 Die Variable **ODBCSharedTraceFlag** zum Aktivieren der Ablaufverfolgung dynamisch festgelegt ist. Diese Variable wird für alle Kopien des Treiber-Managers freigegeben. Jede Anwendung diese Variable festgelegt, wird die Ablaufverfolgung für alle ODBC-Anwendungen, die derzeit ausgeführt aktiviert. Zum Aktivieren von Ablaufverfolgung deaktivieren, wenn die dynamische Protokollierung aktiviert ist, eine Anwendung ruft **SQLSetConnectAttr** SQL_ATTR_TRACE auf SQL_TRACE_OFF festgelegt. Dieser Aufruf wird die Ablaufverfolgung deaktiviert für diese Anwendung nur vollzogen. Anwendungen, die mit Odbc32.lib verknüpft sind, können mithilfe dieser Variablen ändern. Ablaufverfolgungsdaten können in einem Fenster in Echtzeit anstelle der Ablaufverfolgungsdatei angezeigt werden, die nach der ODBC-Sitzung geöffnet werden müssen. Steuerelemente können zu einer Anwendung Bildschirm aktivieren hinzugefügt werden, wird aktiviert oder deaktiviert die Ablaufverfolgung an.  
  
 Die DLL im Lieferumfang von ODBC 3. Ablaufverfolgung*.x* ist nicht threadsicher. Es ist nicht sichergestellt, dass die Protokolldatei richtig geschrieben wird, wenn die globale Protokollierung aktiviert ist (die Variable **ODBCSharedTraceFlag** festgelegt ist) und mehr als eine Anwendung schreibt in die Ablaufverfolgungsdatei zur gleichen Zeit. Diese Bedingung gibt keinen Fehler zurück.
