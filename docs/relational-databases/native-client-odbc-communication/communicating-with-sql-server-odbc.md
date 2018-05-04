---
title: Bei der Kommunikation mit SQLServer (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3cf1b57043fe9333d1b0da73a65aae1e251f00fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="communicating-with-sql-server-odbc"></a>Kommunikation mit SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Für eine ODBC-Anwendung für die Kommunikation mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], müssen sie Umgebung zuordnen und Verbindung handles und Herstellen einer Verbindung mit der Datenquelle. Nach dem Herstellen einer Verbindung kann die Anwendung Abfragen an den Server senden und Resultsets verarbeiten. Wenn die Anwendung die Datenquelle nicht mehr benötigt, wird die Verbindung mit der Datenquelle getrennt und das Verbindungshandle freigegeben. Wenn die Anwendung alle Verbindungshandles freigegeben hat, wird das Umgebungshandle freigegeben.  
  
 Eine Anwendung kann mit beliebig vielen Datenquellen eine Verbindung herstellen. Die Anwendung kann eine Kombination aus Treibern und Datenquellen, denselben Treiber und eine Kombination aus Datenquellen oder auch denselben Treiber und mehrere Verbindungen mit derselben Datenquelle verwenden.  
  
 Sie können herunterladen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Beispiele von der [SQL Server-Downloads](http://go.microsoft.com/fwlink/?LinkId=62796) -Seite auf MSDN.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Zuordnen eines Umgebungshandles](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [Zuordnen eines Verbindungshandles](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC-Datenquellen](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [Herstellen einer Verbindung mit einer Datenquelle &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [Trennen der Verbindung mit einer Datenquelle](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
