---
title: ODBC-Dienstverweis Provider-Schnittstelle (SPI) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a4521d90f3e7eda4167062bd8bc1299921b0e31d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC-Dienstverweis Provider-Schnittstelle (SPI)
ODBC definiert bisher eine Anwendungsprogrammierschnittstelle (API). Die API-Funktionen von Anwendungen aufgerufen werden können und sollten sie in der Treiber-Manager und der Treiber implementiert werden.  
  
 Durch das Hinzufügen von treiberfähiges Verbindungspoolfunktion ist führt ODBC die Service Provider Interface (SPI). Die Funktionen in der SPI sind für die Kommunikation zwischen der Treiber-Manager und Treiber verwendet. SPI-Funktionen werden vom Treiber implementiert. der Treiber-Manager wird kein SPI-Funktionen für Anwendungen bereitgestellt. Anwendungen sollten diese Funktionen nicht direkt aufrufen.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
 Dieser Abschnitt enthält die folgenden Themen  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Entwickeln von Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Treibermanager-Verbindungspooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
