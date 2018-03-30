---
title: OLE DB-Treiber für SQLServer | Microsoft Docs
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
description: ''
ms.custom: ''
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 89e66fe2c61ae17a43e2a58071ba04374f33ea04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL oder OLE DB-Treiber für SQL Server ist ein Begriff, der synonym verwendet wurde, um auf OLE DB-Treiber für SQL Server zu verweisen.

## <a name="different-incarnations-of-ole-db-drivers"></a>Andere Variationen der OLE DB-Treiber

Es gibt drei verschiedene Variationen der Microsoft OLE DB-Anbieter für SQL Server.


### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Microsoft OLE DB-Anbieter für SQLServer (SQLOLEDB)

Die [Microsoft OLE DB-Anbieter für SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) noch geliefert wird, im Rahmen des [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). Es wird nicht empfohlen, diese Treiber für neue Entwicklungen verwenden.


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)

Ab SQL Server 2005, die [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) enthält eine OLE DB-Provider-Schnittstelle (SQLNCLI), und die OLE DB-Anbieter, die mit SQL Server 2005 über SQL Server-2017 ausgeliefert wird.

Es wurde [angekündigt, sobald in 2011 veraltet](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) und es wird nicht empfohlen, diesen Treiber für neue Entwicklungen verwenden.


### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB-Treiber für SQLServer (MSOLEDBSQL)

Wurde von OLE DB- [als undeprecated in 2017 angekündigt](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/). Eine neue Version des geplanten wurde für 2018 angekündigt.

Die neue OLE DB-Anbieter wird der Microsoft OLE DB-Treiber für SQL Server (MSOLEDBSQL) aufgerufen. Der neue Anbieter wird mit den neuesten Server-Funktionen, die zukünftig aktualisiert werden.

Informationen zu den OLE DB-Treiber für SQL Server-Funktionen:

-   [OLE DB-Treiber für SQL Server-Unterstützung für LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [Metadatenermittlung](../oledb/features/metadata-discovery.md)  

-   [UTF-16-Unterstützung in OLE DB-Treiber für SQLServer](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [Zugreifen auf Diagnoseinformationen im Protokoll der erweiterten Ereignisse](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>Siehe auch  
[Installieren des OLE DB-Treiber für SQLServer](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
 [OLE DB-Treiber für SQL Server-Funktionen](../oledb/features/oledb-driver-for-sql-server-features.md )  
