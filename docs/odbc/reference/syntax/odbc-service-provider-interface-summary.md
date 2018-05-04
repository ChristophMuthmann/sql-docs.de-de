---
title: ODBC-Service-Schnittstelle Anbieterzusammenfassung | Microsoft Docs
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
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29a19d20e6a69adf459ee1690e018bb7d237caf3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC-Dienstzusammenfassung Provider-Schnittstelle
Die folgende Tabelle beschreibt die Funktionen der ODBC-Dienstanbieter-Schnittstelle. Weitere Informationen zur Syntax und Semantik für die einzelnen Funktionen finden Sie unter [ODBC Service Provider Interface (SPI) Verweis](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Funktionsname|Zweck|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Identisch mit [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), aber es wird das Attribut auf die Informationen Verbindungstoken statt auf dem Verbindungshandle.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Legt die Verbindungszeichenfolge in das Verbindungstoken für die Informationen für einer Anwendungsverzeichnis [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) aufrufen.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Legt die Datenquelle, Benutzer-ID und Kennwort in das Verbindungstoken für die Informationen für einer Anwendungsverzeichnis [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) aufrufen.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Ruft die Pool-ID ab|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Bestimmt, ob ein Treiber eine vorhandene Verbindung im Verbindungspool wiederverwendet werden kann.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Erstellen Sie eine neue Verbindung, wenn keine Verbindung im Pool wiederverwendet werden kann.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Teilt einen Treiber, den Timeout eine Anwendungspool-ID an.|
