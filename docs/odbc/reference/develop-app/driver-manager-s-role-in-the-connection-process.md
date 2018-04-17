---
title: Treiber-Managers&#39;s-Rolle in der Verbindungsprozess | Microsoft Docs
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
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f6b57322f96f469060db134eead3c09071e7dde
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Treiber-Managers&#39;s-Rolle in der Verbindungsprozess
Denken Sie daran, dass Anwendungen keine Treiberfunktionen direkt aufrufen. Stattdessen rufen Sie Treiber-Manager-Funktionen mit dem gleichen Namen und der Treiber-Manager ruft der Treiberfunktionen. In der Regel geschieht dies fast sofort. Beispielsweise ruft die Anwendung **SQLExecute** im Treiber-Manager und nach einigen Fehlern der fehlerprüfung, ruft der Treiber-Manager **SQLExecute** im Treiber.  
  
 Der Verbindungsprozess unterscheidet. Wenn die Anwendung aufruft, **SQLAllocHandle** mit den Optionen SQL_HANDLE_ENV und SQL_HANDLE_DBC auf, ordnet die Funktion behandelt nur in der Treiber-Manager. Diese Funktion im Treiber wird in der Treiber-Manager nicht aufgerufen, da er nicht, welcher Treiber weiß aufrufen. Auf ähnliche Weise, wenn die Anwendung das Handle für eine nicht verbundene Verbindung übergibt **SQLSetConnectAttr** oder **SQLGetConnectAttr**, nur der Treiber-Manager die Funktion führt Folgendes aus. Sie speichert, oder ruft den Wert des Attributs aus der Verbindung zu behandeln und SQLSTATE 08003 (Verbindung nicht geöffnet) beim Abrufen eines Werts für ein Attribut nicht festgelegt wurde und für welche ODBC zurückgegeben keinen Standardwert definiert.  
  
 Wenn die Anwendung aufruft, **SQLConnect**, **SQLDriverConnect**, oder **SQLBrowseConnect**, der Treiber-Manager zunächst ermittelt, welche Treiber verwendet. Es wird dann geprüft, zu bestimmen, ob ein Treiber für die Verbindung ist derzeit geladen:  
  
-   Wenn kein Treiber für die Verbindung geladen wird, überprüft der Treiber-Manager an, ob der angegebene Treiber auf eine andere Verbindung in der gleichen Umgebung geladen wird. Wenn nicht, den Treiber-Manager den Treiber auf die Verbindung und ruft lädt **SQLAllocHandle** im Treiber mit der Option SQL_HANDLE_ENV auf.  
  
     Der Treiber-Manager ruft dann **SQLAllocHandle** im Treiber mit der Option SQL_HANDLE_DBC auf, und zwar unabhängig davon, ob sie nur geladen wurde. Wenn die Anwendung Verbindungsattribute festgelegt wird, ruft der Treiber-Manager **SQLSetConnectAttr** im Treiber; Wenn ein Fehler auftritt, der Treiber-Manager-Verbindungsfunktion gibt SQLSTATE IM006 (des Treibers  **SQLSetConnectAttr** fehlgeschlagen). Zum Schluss ruft der Treiber-Manager die Verbindungsfunktion im Treiber.  
  
-   Wenn der angegebene Treiber für die Verbindung geladen wird, ruft der Treiber-Manager nur die Verbindungsfunktion im Treiber. In diesem Fall muss der Treiber aufbewahren müssen, für die Verbindung alle Verbindungsattribute ihren aktuellen Einstellungen.  
  
-   Wenn ein anderer Treiber für die Verbindung geladen wird, ruft der Treiber-Manager **SQLFreeHandle** im Treiber die Verbindung freizugeben. Wenn es keine anderen Verbindungen, die der Treiber verwendet wird sind, ruft der Treiber-Manager **SQLFreeHandle** im Treiber auf die Umgebung frei und entlädt den Treiber. Der Treiber-Manager führt dann die gleichen Vorgänge wie, wann ein Treiber für die Verbindung nicht geladen wurde.  
  
 Der Treiber-Manager wird das Umgebungshandle gesperrt (*Henv*) vor dem Aufrufen des Treibers **SQLAllocHandle** und **SQLFreeHandle** Wenn *HandleType* festgelegt ist, um **SQL_HANDLE_DBC**.  
  
 Wenn die Anwendung aufruft, **SQLDisconnect**, der Treiber-Manager ruft **SQLDisconnect** im Treiber. Allerdings bleibt den Treiber geladen wird, für den Fall, dass die Anwendung an den Treiber erneut eine Verbindung herstellt. Wenn die Anwendung aufruft, **SQLFreeHandle** mit der Option SQL_HANDLE_DBC auf der Treiber-Manager ruft **SQLFreeHandle** im Treiber. Wenn der Treiber nicht durch alle anderen Verbindungen verwendet wird, ruft der Treiber-Manager dann **SQLFreeHandle** -option in den Treiber mit der SQL_HANDLE_ENV und entlädt den Treiber.
