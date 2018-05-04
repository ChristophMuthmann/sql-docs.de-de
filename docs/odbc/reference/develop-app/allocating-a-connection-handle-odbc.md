---
title: Zuordnen eines Verbindungshandles ODBC | Microsoft Docs
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
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a27daadecb685a64d7c5a05e01cda05ec30dd185
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-a-connection-handle-odbc"></a>Zuordnen eines Verbindungshandles ODBC
Bevor die Anwendung auf eine Datenquelle oder Treiber zugreifen kann, müssen sie ein Verbindungshandle wie folgt zuordnen:  
  
1.  Die Anwendung deklariert eine Variable vom Typ SQLHDBC. Er ruft dann **SQLAllocHandle** und übergibt die Adresse dieser Variablen wird das Handle für die Umgebung aus, die die Verbindung und die Option SQL_HANDLE_DBC zuordnen. Beispiel:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  Der Treiber-Manager weist eine Struktur zum Speichern von Informationen über die Anweisung und gibt das Verbindungshandle in der Variablen zurück.  
  
 Der Treiber-Manager nicht aufgerufen **SQLAllocHandle** im Treiber auf dieser Zeit, da er nicht, welcher Treiber weiß aufrufen. Erfolgt eine Verzögerung, Aufrufen von **SQLAllocHandle** im Treiber, bis die Anwendung eine Funktion zur Verbindung mit einer Datenquelle aufgerufen. Weitere Informationen finden Sie unter [Treiber-Manager-Rolle in der Verbindungsprozess](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)weiter unten in diesem Abschnitt.  
  
 Es ist wichtig zu beachten, dass das Zuordnen eines Verbindungshandles nicht um einen Treiber zu laden identisch ist. Der Treiber wurde nicht geladen werden, bis eine Verbindungsfunktion aufgerufen wird. Daher nach dem Zuordnen eines Verbindungshandles und vor dem Herstellen einer Verbindung mit der Treiber oder die Datenquelle, die nur Funktionen, die die Anwendung mit dem Verbindungshandle aufrufen kann stimmen **SQLSetConnectAttr**, **SQLGetConnectAttr**, oder **SQLGetInfo** mit der Option SQL_ODBC_VER. Aufruf anderer Funktionen mit dem Verbindungshandle, z. B. **SQLEndTran**, gibt SQLSTATE 08003 (Verbindung nicht geöffnet). Ausführliche Informationen finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Weitere Informationen zu Verbindungshandles, finden Sie unter [Verbindungshandles](../../../odbc/reference/develop-app/connection-handles.md).
