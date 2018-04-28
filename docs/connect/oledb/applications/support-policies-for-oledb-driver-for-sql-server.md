---
title: Unterstützung von Richtlinien für OLE DB-Treiber für SQLServer | Microsoft Docs
description: Unterstützung von Richtlinien für die OLE DB-Treiber für SQL Server
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dfac5b5acd86c71787e3ee5052927d7d59969f8b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Richtlinien zur Unterstützung für OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Dieser Artikel beschreibt die Verwendung verschiedener Datenzugriffskomponenten mit OLE DB-Treiber für SQL Server verwendet werden können.  

## <a name="server-support"></a>Serverunterstützung  
 OLE DB-Treiber für SQL Server unterstützt Verbindungen mit [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)],[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], und [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Unterstützte Betriebssystemversionen  
 Die folgende Tabelle enthält die Betriebssysteme Unterstützung OLE DB-Treiber für SQL Server.  

|Unterstützte Betriebssysteme|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Richtlinien zur ADO-Unterstützung  
 ADO-Anwendungen können den zum Lieferumfang von Windows gehörenden SQLOLEDB OLE DB-Anbieter verwenden, sofern sie keine Funktionen von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher benötigen.  

 ADO-Anwendungen können den OLE DB-Treiber für SQL Server verwenden, aber wenn sie zu diesem Zweck müssen sie angeben `DataTypeCompatibility=80` in den Verbindungszeichenfolgen. Wenn `DataTypeCompatibility=80` in den Verbindungszeichenfolgen angegeben wird, sind nur die Funktionen von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] verfügbar.  

## <a name="ole-db-support-policies"></a>Richtlinien zur OLE DB-Unterstützung  
Anwendungen können den OLE DB-Anbieter (SQLOLEDB) mit dem Windows-Betriebssystem enthalten. Allerdings, die in den Wartungsmodus versetzt wird und nicht mehr aktualisiert. Sie sollten den OLE DB-Treiber für SQL Server (MSOLEDBSQL) verwenden.

## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
