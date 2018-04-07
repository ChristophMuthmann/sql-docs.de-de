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
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5f009cf311c1eb395915e017bf202abea5ae5290
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL oder OLE DB-Treiber für SQL Server ist ein Begriff, der synonym verwendet wird, um auf OLE DB-Treiber für SQL Server zu verweisen.

## <a name="different-generations-of-ole-db-drivers"></a>Verschiedene Generationen von OLE DB-Treiber

Es gibt drei verschiedene Generationen von Microsoft OLE DB-Anbieter für SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Microsoft OLE DB-Anbieter für SQLServer (SQLOLEDB)
Die [Microsoft OLE DB-Anbieter für SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) noch geliefert wird, im Rahmen des [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). Sie wird nicht mehr verwaltet, und es wird nicht empfohlen, diesen Treiber für neue Entwicklungen verwenden. 


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) enthält eine OLE DB-Provider-Schnittstelle (SQLNCLI) und ist der OLE DB-Anbieter, die im Lieferumfang [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] über [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Es wurde [angekündigt, sobald in 2011 veraltet](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) und es wird nicht empfohlen, diesen Treiber für neue Entwicklungen verwenden. Weitere Informationen zu den SNAC-Lebenszyklus und die verfügbaren Downloads, finden Sie unter [SNAC-Lebenszyklus erklärt](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB-Treiber für SQLServer (MSOLEDBSQL)
Wurde von OLE DB- [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) in 2018 veröffentlicht und kann heruntergeladen werden [hier](https://go.microsoft.com/fwlink/?linkid=871294).

Die neue OLE DB-Anbieter wird der Microsoft OLE DB-Treiber für SQL Server (MSOLEDBSQL) aufgerufen. Der neue Anbieter wird mit den neuesten Server-Funktionen, die zukünftig aktualisiert werden.

> [!NOTE]
> Um die neue Microsoft OLE DB-Treiber für SQL Server in vorhandene Anwendungen zu verwenden, sollten Sie planen, die Verbindungszeichenfolgen von SQLOLEDB oder SQLNCLI, in MSOLEDBSQL zu konvertieren.   

Informationen zu den OLE DB-Treiber für SQL Server-Funktionen:

-   [OLE DB-Treiber für SQL Server-Unterstützung für LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [Metadatenermittlung](../oledb/features/metadata-discovery.md)  

-   [UTF-16-Unterstützung im OLE DB-Treiber für SQL Server (OLE DB)](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [OLE DB-Treiber für SQL Server-Unterstützung für Hochverfügbarkeit, Notfallwiederherstellung](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [Zugreifen auf Diagnoseinformationen im Protokoll der erweiterten Ereignisse](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>Siehe auch  
[Installieren des OLE DB-Treiber für SQLServer](../oledb/applications/installing-oledb-driver-for-sql-server.md)     
[OLE DB-Treiber für SQL Server-Features](../oledb/features/oledb-driver-for-sql-server-features.md )     
