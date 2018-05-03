---
title: Datenquellenobjekte (OLE DB) | Microsoft Docs
description: Datenquellenobjekte (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 05e9653ad107d31042ff75416e85754129709fff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-objects-ole-db"></a>Datenquellenobjekte (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB-Treiber für SQL Server verwendet den Begriff-Datenquelle für den Satz von OLE DB-Schnittstellen verwendet, um einen Link zu einem Datenspeicher, z. B. herzustellen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Erstellen einer Instanz von das Datenquellenobjekt des Anbieters ist die erste Aufgabe von einer OLE DB-Treiber für SQL Server-Consumer.  
  
 Jeder OLE DB-Anbieter deklariert einen Klassenbezeichner (CLSID) für sich. Die CLSID für den OLE DB-Treiber für SQL Server ist die C/C++-GUID-CLSID_MSOLEDBSQL (das Symbol MSOLEDBSQL_CLSID, um den richtigen aufgelöst wird progid in der msoledbsql.h-Datei, die Sie referenzieren). Mit der CLSID verwendet der Consumer die OLE **CoCreateInstance** Funktion zur Herstellung einer Instanz des Datenquellenobjekts.  
  
 OLE DB-Treiber für SQL Server ist ein in-Process-Server. Instanzen von OLE DB-Treiber für SQL Server-Objekte werden erstellt, mithilfe des CLSCTX_INPROC_SERVER-Makros zu den ausführbaren Kontext anzugeben.  
  
 Der OLE DB-Treiber für SQL Server-Datenquellenobjekt macht die OLE DB-Initialisierungsschnittstellen bereit, mit denen den Consumer für die Verbindung zu vorhandenen können [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbanken.  
  
 Jede Verbindung, die über den OLE DB-Treiber für SQL Server legt diese Optionen automatisch fest:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Dieses Beispiel verwendet das klassenbezeichnermakro zum Erstellen von OLE DB-Treiber für SQL Server-Daten Datenquellenobjekts und zum Abrufen eines Verweises auf die **IDBInitialize** Schnittstelle.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 Mit der erfolgreichen Erstellung einer Instanz von einer OLE DB-Treiber für SQL Server-Datenquellenobjekt kann die Consumeranwendung fortfahren, indem die Datenquelle initialisiert und Sitzungen erstellt. OLE DB-Sitzungen präsentieren die Schnittstellen, die Datenzugriff und -bearbeitung ermöglichen.  
  
 Der OLE DB-Treiber für SQL Server stellt die erste Verbindung zu einer angegebenen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als Teil einer erfolgreichen datenquelleninitialisierung. Die Verbindung wird beibehalten, solange ein Verweis auf eine beliebige Datenquellen-Initialisierungsschnittstelle oder bis beibehalten wird die **IDBInitialize:: UnInitialize** -Methode aufgerufen wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Datenquelleneigenschaften & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Eigenschaften für Datenquelleninformationen](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Initialisierungs- und Autorisierungseigenschaften](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sitzungen](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [Sitzungseigenschaften: OLE DB-Treiber für SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [Persistente Datenquellenobjekte](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Programmierung](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
