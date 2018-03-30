---
title: Herstellen einer Verbindung mit einer Datenquelle | Microsoft Docs
description: Herstellen einer Verbindung mit einer Datenquelle mithilfe von OLE DB-Treiber für SQL Server
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
- data sources [OLE DB Driver for SQL Server]
- connections [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, data source connections
- CoCreateInstance method
- OLE DB data sources [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10e80f6f9669059f749d4d96b72c7cc69743f6b4
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="establishing-a-connection-to-a-data-source"></a>Herstellen einer Verbindung zu einer Datenquelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Für den Zugriff auf den OLE DB-Treiber für SQL Server der Consumer muss zuerst erstellen Sie eine Instanz von einem Datenquellenobjekt durch Aufrufen der **CoCreateInstance** Methode. Ein eindeutiger Klassenbezeichner (CLSID) identifiziert jeden OLE DB-Anbieter. Für den OLE DB-Treiber für SQL Server ist der Klassenbezeichner CLSID_MSOLEDBSQL. Sie können auch das Symbol MSOLEDBSQL_CLSID verwenden, die in der OLE DB-Treiber für SQL Server aufgelöst wird, die in der msoledbsql.h verwendet wird, die Sie verweisen.  
  
 Die Datenquelle macht die **IDBProperties** -Schnittstelle, die der Consumer verwendet, um grundlegende Authentifizierungsinformationen wie Servername, Datenbankname, Benutzer-ID und Kennwort bereitzustellen. Die **IDBProperties:: SetProperties** Methode wird aufgerufen, um diese Eigenschaften festzulegen.  
  
 Wenn mehrere Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf dem Computer ausgeführt werden, wird der Servername als ServerName\InstanceName angegeben.  
  
 Auch das Datenquellenobjekt macht die **IDBInitialize** Schnittstelle. Nach dem Festlegen der Eigenschaften wird die Verbindung mit der Datenquelle hergestellt, durch Aufrufen der **IDBInitialize:: Initialize** Methode. Beispiel:  
  
```  
CoCreateInstance(CLSID_MSOLEDBSQL,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```  
  
 Dieser Aufruf **CoCreateInstance** erstellt ein einzelnes Objekt der Klasse CLSID_MSOLEDBSQL (CSLID zugeordnet, die Daten und den Code, der zum Erstellen des Objekts verwendet wird) zugeordnet. IID_IDBInitialize ist ein Verweis auf den Bezeichner der Schnittstelle (**IDBInitialize**) für die Kommunikation mit dem Objekt verwendet werden.  
  
 Die folgende Funktion ist eine Beispielfunktion, die eine Verbindung zur Datenquelle initiiert und herstellt.  
  
```  
void InitializeAndEstablishConnection() {  
   // Initialize the COM library.  
   CoInitialize(NULL);  
  
   // Obtain access to the OLE DB Driver for SQL Server.  
   hr = CoCreateInstance(CLSID_MSOLEDBSQL,   
                         NULL,   
                         CLSCTX_INPROC_SERVER,  
                         IID_IDBInitialize,   
                         (void **) &pIDBInitialize);  
   // Initialize property values needed to establish connection.  
   for (i = 0 ; i < 4 ; i++)   
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   // See DBPROP structure for more information on InitProperties  
   InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt    = VT_BSTR;  
   InitProperties[0].vValue.bstrVal=   
                     SysAllocString(L"Server");  
   InitProperties[0].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid       = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt    = VT_BSTR;  
   InitProperties[1].vValue.bstrVal= SysAllocString(L"database");  
   InitProperties[1].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid       = DB_NULLID;  
  
   // Username (login).  
   InitProperties[2].dwPropertyID  = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt    = VT_BSTR;  
   InitProperties[2].vValue.bstrVal= SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid       = DB_NULLID;  
   InitProperties[3].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[3].colid       = DB_NULLID;  
  
   // Construct the DBPROPSET structure(rgInitPropSet). The   
   // DBPROPSET structure is used to pass an array of DBPROP   
   // structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties   = 4;  
   rgInitPropSet[0].rgProperties   = InitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                           (void **)&pIDBProperties);  
   hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   pIDBInitialize->Initialize();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einen OLE DB-Treiber für SQL Server-Anwendung](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
