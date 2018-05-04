---
title: Das Umgebungshandle zuordnen | Microsoft Docs
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
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23851cae822210fd13061b5e4f5de67e0c510e89
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-the-environment-handle"></a>Das Umgebungshandle zuordnen
Die erste Aufgabe für jede ODBC-Anwendung ist der Treiber-Manager zu laden. Diese Vorgehensweise ist abhängig vom Betriebssystem. Z. B. auf einem Computer unter Microsoft® Windows NT® Server-Windows 2000 Server, Windows NT Arbeitsstation/Windows 2000 Professional oder Microsoft Windows® 95-und Windows 98, die Anwendung entweder enthält links zu den Treiber-Manager-Bibliothek oder Aufrufe  **LoadLibrary** zum Laden der DLL-Treiber-Manager.  
  
 Die nächste Aufgabe ausgeführt werden muss, bevor eine Anwendung eine ODBC-Funktion aufrufen kann, ist das Initialisieren der ODBC-Umgebung, und ordnen Sie ein Umgebungshandle wie folgt:  
  
1.  Die Anwendung deklariert eine Variable vom Typ SQLHENV. Er ruft dann **SQLAllocHandle** und übergibt die Adresse dieser Variablen und die Option SQL_HANDLE_ENV auf. Beispiel:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  Der Treiber-Manager weist eine Struktur zum Speichern von Informationen über die Umgebung, und gibt das Umgebungshandle in der Variablen zurück.  
  
 Der Treiber-Manager nicht aufgerufen **SQLAllocHandle** im Treiber auf dieser Zeit, da er nicht, welcher Treiber weiß aufrufen. Erfolgt eine Verzögerung, Aufrufen von **SQLAllocHandle** im Treiber, bis die Anwendung eine Funktion zur Verbindung mit einer Datenquelle aufgerufen. Weitere Informationen finden Sie unter [Treiber-Manager-Rolle in der Verbindungsprozess](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)weiter unten in diesem Abschnitt.  
  
 Wenn die Anwendung mithilfe von ODBC abgeschlossen ist, gibt das Umgebungshandle mit frei **SQLFreeHandle**. Nach der Freigabe der umgebungs, ist es ein anwendungsprogrammierungsfehler Fehler, die Umgebung Handle zu einem Aufruf von einer ODBC-Funktion zu verwenden. Dies hat sich nicht definierte, aber wahrscheinlich schwerwiegende Folgen.  
  
 Wenn **SQLFreeHandle** aufgerufen wird, wird der Treiberversionen, die die Struktur zum Speichern von Informationen über die Umgebung verwendet. Beachten Sie, dass **SQLFreeHandle** kann nicht für ein Umgebungshandle erst aufgerufen werden, nachdem alle Verbindungshandles auf diesem Umgebungshandle freigegeben wurden.  
  
 Weitere Informationen über das Umgebungshandle finden Sie unter [Umgebung behandelt](../../../odbc/reference/develop-app/environment-handles.md).
