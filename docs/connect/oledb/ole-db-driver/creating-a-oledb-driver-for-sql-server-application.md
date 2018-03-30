---
title: Erstellen einen OLE DB-Treiber für SQL Server-Anwendung | Microsoft Docs
description: Erstellen einen OLE DB-Treiber für SQL Server-Anwendung
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e54bdee09a64cd1393a41109207d42a598cb31fa
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>Erstellen einen OLE DB-Treiber für SQL Server-Anwendung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Erstellen einen OLE DB-Treiber für SQL Server-Anwendung umfasst folgende Schritte aus:  
  
1.  Eine Verbindung mit einer Datenquelle herzustellen.  
  
2.  Ausführen eines Befehls an.  
  
3.  Verarbeiten der Ergebnisse  
  
> [!NOTE]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn die Windows-Authentifizierung nicht verfügbar ist, fordern Sie die Benutzer auf, ihre Anmeldeinformationen zur Laufzeit einzugeben. Die Anmeldeinformationen sollten nicht in einer Datei gespeichert werden. Wenn Sie die Anmeldeinformationen persistent speichern müssen, sollten Sie sie mit der [Win32 Crypto-API](http://go.microsoft.com/fwlink/?LinkId=9504)verschlüsseln.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Herstellen einer Verbindung mit einer Datenquelle](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [Ausführen eines Befehls](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [Verarbeiten von Ergebnissen](../../oledb/ole-db-driver/processing-results.md)  
  
-   [Informationen zu OLE DB-Eigenschaften](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [Mithilfe der OUTPUT-Klausel mit OLE DB in OLE DB-Treiber für SQLServer](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQLServer &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
