---
title: Herstellen einer Verbindung | Microsoft Docs
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
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 43e7ab9f883df271f47b0ad55a931ce1a2d2c220
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="establishing-a-connection"></a>Herstellen einer Verbindung
Nach dem Zuweisen der umgebungs- und Verbindungshandles und Festlegen der Verbindungsattribute, ist die Anwendung für die Datenquelle oder der Treiber die Verbindung bereit. Es gibt drei verschiedene Funktionen, die die Anwendung zu diesem Zweck verwenden kann: **SQLConnect** (Core-Schnittstelle Konformitätsgrad), **SQLDriverConnect** (Core), und **SQLBrowseConnect**(Stufe 1). Jeder der drei wird in ein anderes Szenario verwendet werden sollen. Bevor Sie eine Verbindung herstellen, kann die Anwendung bestimmen, welche dieser Funktionen mit unterstützt wird die **ConnectFunctions** Schlüsselwort zurückgegebenes **SQLDrivers**.  
  
> [!NOTE]  
>  Einige Treiber zu begrenzen die Anzahl der aktiven Verbindungen, die sie unterstützen. Ruft die Anwendung **SQLGetInfo** mit der Option SQL_MAX_DRIVER_CONNECTIONS, um zu bestimmen, wie viele aktive Verbindungen ein bestimmter Treiber unterstützt.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Standard-Datenquelle](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Herstellen einer Verbindung mit SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Verbindungszeichenfolgen](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Herstellen einer Verbindung mit SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Herstellen einer Verbindung mit SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
