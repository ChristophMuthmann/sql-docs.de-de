---
title: Verfolgen Sie die DLL | Microsoft Docs
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
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7eb679c8d7182dd0edd3a96caafa824a8722962
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="trace-dll"></a>Trace-DLL
Die DLL, die von der Ablaufverfolgung ist der ODBC-Kernkomponenten. Die Ablaufverfolgung, die DLL wird derzeit als eine DLL-Beispiel in der ODBC-Komponente des Windows SDK bereitgestellt und wurde, enthalten früher Microsoft Data Access Components (MDAC) SDK. Daher sind der Registrierungseintrag, Schnittstelle und Beispielcode für die Ablaufverfolgung DLL verfügbar. Diese DLL kann von einer Ablaufverfolgung durch einen ODBC-Benutzer oder einem Drittanbieter erstellte DLL ersetzt werden. Eine benutzerdefinierte Ablaufverfolgung DLL Unternehmensservern benötigen einen anderen Namen als die ursprüngliche Beispiel Ablaufverfolgung DLL. Trace-DLLs im Verzeichnis "System" installiert werden müssen, oder sie können nicht geladen werden. Verbindungszeichenfolgen für die Verbindung werden nicht in die Ablaufverfolgung DLL vom Treiber-Manager übergeben.  
  
 Die DLL-Ablaufverfolgung verfolgt Eingabeargumente, Ausgabeargumente verzögerte Argumente, Rückgabecodes und SQLSTATEs. Wenn Ablaufverfolgung aktiviert ist, ruft der Treiber-Manager die Trace-DLL an zwei Punkten: einmal Funktionseinstieg (vor der Argument-Prüfung) und wieder nur vor der Rückkehr der Funktion.  
  
 Wenn eine Anwendung eine Funktion aufruft, ruft der Treiber-Manager eine Trace-Funktion in der Ablaufverfolgung DLL vor dem Aufrufen der Funktion im Treiber oder den Aufruf selbst verarbeiten. Jede ODBC-Funktion verfügt über eine entsprechende Trace-Funktion (mit dem Präfix *Ablaufverfolgung*), die an die ODBC-Funktion, mit Ausnahme von den Namen identisch ist. Wenn die Trace-Funktion aufgerufen wird, wird die Ablaufverfolgung DLL erfasst die Eingabeargumente und einen Rückgabecode gibt. Da die Ablaufverfolgung DLL aufgerufen wird, bevor der Treiber-Manager Argumente überprüft, werden ungültige Funktionsaufrufe nachverfolgt, damit Zustand Übergang Fehler und ungültige Argumente protokolliert werden.  
  
 Nach dem Aufrufen der Funktion Trace in der Ablaufverfolgung DLL, ruft der Treiber-Manager die ODBC-Funktion im Treiber. Er ruft dann **TraceReturn** in der Ablaufverfolgung DLL. Diese Funktion akzeptiert zwei Argumente: den Rückgabewert von der DLL-Ablaufverfolgung für die Funktion Trace und den Rückgabecode, der vom Treiber zurückgegebene, um den Treiber-Manager für die ODBC-Funktion (oder der Wert, der vom Treiber-Manager selbst zurückgegeben, wenn er die Funktion verarbeitet). Die Funktion verwendet den Rückgabewert für die Ablaufverfolgungsfunktion erfassten Eingabeargument Werte bearbeiten. Er schreibt den Code für die ODBC-Funktion zurückgegeben wird, in der Protokolldatei gespeichert (oder wird dynamisch angezeigt, wenn aktiviert ist). Die Ausgabe argumentzeiger dereferenziert, und die ausgabeargumentwerte protokolliert.
