---
title: Systemanforderungen für OLE DB-Treiber für SQLServer | Microsoft Docs
description: Anforderungen für OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c465001d1e09ac229b0dc8cfd16124df3143e3d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Systemanforderungen für OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Um Datenzugriffsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], wie z. B. MARS, zu verwenden, muss die folgende Software installiert sein:  

-   OLE DB-Treiber für SQL Server auf dem Client.  

-   Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Ihrem Server.   

> [!NOTE]  
>  Melden Sie sich vor der Installation dieser Software mit Administratorberechtigungen an.  

## <a name="operating-system-requirements"></a>Betriebssystemanforderungen  
 Eine Liste der Betriebssysteme, die OLE DB-Treiber für SQL Server zu unterstützen, finden Sie unter [für OLE DB-Treiber für SQL Server-Richtlinien unterstützen](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

## <a name="sql-server-requirements"></a>SQL Server-Anforderungen  
 Verwenden von OLE DB-Treiber für SQL Server für den Datenzugriff in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken benötigen Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] unterstützt Verbindungen von allen Versionen von MDAC, Windows Data Access Components und alle Versionen des OLE DB-Treiber für SQL Server. Wenn eine ältere Clientversion eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellt, werden Serverdatentypen, die dem Client nicht bekannt sind, Typen zugeordnet, die mit der Clientversion kompatibel sind. Weitere Informationen finden Sie unter „Datentypkompatibilität für Clientversionen“ später in diesem Thema.  

## <a name="cross-language-requirements"></a>Anforderungen an die sprachübergreifende Unterstützung  
 Die englischsprachige Version des OLE DB-Treiber für SQL Server wird für alle lokalisierten Versionen unterstützter Betriebssysteme unterstützt. Lokalisierte Versionen des OLE DB-Treiber für SQL Server werden unter lokalisierten Betriebssystemen unterstützt, die der Sprache der lokalisierten OLE DB-Treiber für SQL Server-Version sind. Lokalisierte Versionen des OLE DB-Treiber für SQL Server werden auch auf englischsprachigen Versionen der unterstützten Betriebssysteme unterstützt, solange die entsprechenden spracheinstellungen installiert werden.  

 Für Upgrades:  

-   Englischsprachige Versionen des OLE DB-Treiber für SQL Server können auf jede lokalisierte Version des OLE DB-Treiber für SQL Server aktualisiert werden.  

-   Lokalisierte Versionen des OLE DB-Treiber für SQL Server können auf lokalisierte Versionen des OLE DB-Treiber für SQL Server-Instanz derselben Sprache aktualisiert werden.  

-   Lokalisierte Version des OLE DB-Treiber für SQL Server kann auf die englischsprachige Version des OLE DB-Treiber für SQL Server aktualisiert werden.  

-   Lokalisierte Versionen des OLE DB-Treiber für SQL Server können nicht auf lokalisierte OLE DB-Treiber für SQL Server-Versionen von einer anderen lokalisierten Sprache aktualisiert werden.  

## <a name="data-type-compatibility-for-client-versions"></a>Datentypkompatibilität für Clientversionen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und OLE DB-Treiber für SQL Server Zuordnung neue Datentypen alten Datentypen sind kompatibel mit Downlevelclients, wie in der folgenden Tabelle gezeigt.  

 OLE DB und ADO-Anwendungen können die **DataTypeCompatibility** Schlüsselwort für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server mit älteren Datentypen verwendet werden kann. Wenn **DataTypeCompatibility = 80**, OLE DB-Clients werden eine Verbindung herstellen mit der [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tabular Data stream (TDS)-Version, anstatt die TDS-Version. Dies bedeutet, dass für [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höhere Datentypen früherer Konvertierung erfolgt durch den Server und nicht vom OLE DB-Treiber für SQL Server. Darüber hinaus bedeutet dies, dass die auf der Verbindung verfügbaren Funktionen auf den  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Funktionssatz beschränkt sein werden. Der Versuch, neue Datentypen oder Funktionen zu verwenden, wird auf API-Aufrufen so früh wie möglich entdeckt und zur aufrufenden Anwendung zurückgegeben, anstatt dass ein Versuch unternommen wird, ungültige Anforderungen an den Server zu übergeben.   


 IDBInfo:: GetKeywords gibt stets eine Schlüsselwortliste, die die Serverversion für die Verbindung entspricht und ist nicht betroffen von **DataTypeCompatibility**.  

|Datentyp|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB-Treiber für SQLServer|Windows Data Access Components, MDAC und<br /><br /> OLE DB-Treiber für SQL Server OLE DB-Anwendungen mit DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR-UDT (\<= 8 Kb)|udt|Udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|Text|  
|nvarchar(max)|nvarchar|nvarchar|nvarchar|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|udt|varbinary|varbinary|image|  
|Datum|Datum|varchar|varchar|Varchar|  
|datetime2|datetime2|varchar|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|varchar|Varchar|  
|Uhrzeit|Uhrzeit|varchar|varchar|Varchar|  

## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQLServer](../oledb/oledb-driver-for-sql-server.md)   
 [Installation des OLE DB-Treibers für SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
