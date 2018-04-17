---
title: Sitzungen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 3a980816-675c-4fba-acc9-429297d85bbd
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6f7adea36768f9f46e349bee356d4abd275ce728
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sessions"></a>Sitzungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-anbietersitzung stellt eine einzelne Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erfordert, dass Sitzungen den Transaktionsbereich für eine Datenquelle begrenzen. Alle mit einem bestimmten Sitzungsobjekt erstellten Befehlsobjekte nehmen an der lokalen oder verteilten Transaktion des Sitzungsobjekts teil.  
  
 Das erste für die initialisierte Datenquelle erstellte Sitzungsobjekt empfängt die bei Initialisierung hergestellte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindung. Wenn alle Verweise auf die Schnittstellen des Sitzungsobjekts freigegeben werden, wird die Verbindung zur Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für ein anderes für die Datenquelle erstelltes Sitzungsobjekt verfügbar.  
  
 Ein zusätzliches für die Datenquelle erstelltes Sitzungsobjekt stellt eine eigene Verbindung zur Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, wie von der Datenquelle angegeben. Die Verbindung zur Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird unterbrochen, wenn die Anwendung alle Verweise auf Objekte freigibt, die in dieser Sitzung erstellt wurden.  
  
 Im folgenden Beispiel wird veranschaulicht, wie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter zum Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank:  
  
```  
int main()  
{  
    // Interfaces used in the example.  
    IDBInitialize*      pIDBInitialize      = NULL;  
    IDBCreateSession*   pIDBCreateSession   = NULL;  
    IDBCreateCommand*   pICreateCmd1        = NULL;  
    IDBCreateCommand*   pICreateCmd2        = NULL;  
    IDBCreateCommand*   pICreateCmd3        = NULL;  
  
    // Initialize COM.  
    if (FAILED(CoInitialize(NULL)))  
    {  
        // Display error from CoInitialize.  
        return (-1);  
    }  
  
    // Get the memory allocator for this task.  
    if (FAILED(CoGetMalloc(MEMCTX_TASK, &g_pIMalloc)))  
    {  
        // Display error from CoGetMalloc.  
        goto EXIT;  
    }  
  
    // Create an instance of the data source object.  
    if (FAILED(CoCreateInstance(CLSID_SQLNCLI10, NULL,  
        CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void**)  
        &pIDBInitialize)))  
    {  
        // Display error from CoCreateInstance.  
        goto EXIT;  
    }  
  
    // The InitFromPersistedDS function   
    // performs IDBInitialize->Initialize() establishing  
    // the first application connection to the instance of SQL Server.  
    if (FAILED(InitFromPersistedDS(pIDBInitialize, L"MyDataSource",  
        NULL, NULL)))  
    {  
        goto EXIT;  
    }  
  
    // The IDBCreateSession interface is implemented on the data source  
    // object. Maintaining the reference received maintains the   
    // connection of the data source to the instance of SQL Server.  
    if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession,  
        (void**) &pIDBCreateSession)))  
    {  
        // Display error from pIDBInitialize.  
        goto EXIT;  
    }  
  
    // Releasing this has no effect on the SQL Server connection  
    // of the data source object because of the reference maintained by  
    // pIDBCreateSession.  
    pIDBInitialize->Release();  
    pIDBInitialize = NULL;  
  
    // The session created next receives the SQL Server connection of  
    // the data source object. No new connection is established.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd1)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // A new connection to the instance of SQL Server is established to support the  
    // next session object created. On successful completion, the  
    // application has two active connections on the SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd2)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // pICreateCmd1 has the data source connection. Because the  
    // reference on the IDBCreateSession interface of the data source  
    // has not been released, releasing the reference on the session  
    // object does not terminate a connection to the instance of SQL Server.  
    // However, the connection of the data source object is now   
    // available to another session object. After a successful call to   
    // Release, the application still has two active connections to the   
    // instance of SQL Server.  
    pICreateCmd1->Release();  
    pICreateCmd1 = NULL;  
  
    // The next session created gets the SQL Server connection  
    // of the data source object. The application has two active  
    // connections to the instance of SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd3)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
EXIT:  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd1 has the connection of the data source   
    // object.  
    if (pICreateCmd1 != NULL)  
        pICreateCmd1->Release();  
  
    // Releasing the reference on pICreateCmd2 terminates the SQL  
    // Server connection supporting the session object. The application  
    // now has only a single active connection on the instance of SQL Server.  
    if (pICreateCmd2 != NULL)  
        pICreateCmd2->Release();  
  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd3 has the connection of the   
    // data source object.  
    if (pICreateCmd3 != NULL)  
        pICreateCmd3->Release();  
  
    // On release of the last reference on a data source interface, the  
    // connection of the data source object to the instance of SQL Server is broken.  
    // The example application now has no SQL Server connections active.  
    if (pIDBCreateSession != NULL)  
        pIDBCreateSession->Release();  
  
    // Called only if an error occurred while attempting to get a   
    // reference on the IDBCreateSession interface of the data source.  
    // If so, the call to IDBInitialize::Uninitialize terminates the   
    // connection of the data source object to the instance of SQL Server.  
    if (pIDBInitialize != NULL)  
    {  
        if (FAILED(pIDBInitialize->Uninitialize()))  
        {  
            // Uninitialize is not required, but it fails if an  
            // interface has not been released. Use it for  
            // debugging.  
        }  
        pIDBInitialize->Release();  
    }  
  
    if (g_pIMalloc != NULL)  
        g_pIMalloc->Release();  
  
    CoUninitialize();  
  
    return (0);  
}  
```  
  
 Herstellen einer Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-anbietersitzungsobjekten mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erheblichen Mehraufwand für Anwendungen, die kontinuierlich sitzungsbojekte erstellen und Freigeben von Sitzungsobjekte generieren können. Der Aufwand minimiert werden kann, durch die Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-anbietersitzungsobjekten effizient. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB-anbieteranwendungen können behalten die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verbindung eines Sitzungsobjekts aktiv ist, indem Sie einen Verweis auf mindestens eine Schnittstelle des Objekts zu verwalten.  
  
 Durch Aufrechterhalten eines Pools von Verweisen auf Befehlserstellungsobjekte können aktive Verbindungen für diese Sitzungsobjekte im Pool aktiviert bleiben. Wie Session-Objekte erforderlich sind, übergibt der poolverwaltungscode einen gültigen **IDBCreateCommand** Schnittstellenzeiger auf die Anwendungsmethode die Sitzung erfordert. Wenn die Anwendungsmethode die Sitzung nicht mehr erfordert, gibt die Methode den Schnittstellenzeiger an den Poolverwaltungscode zurück, anstatt den Verweis der Anwendung auf das Befehlserstellungsobjekt freizugeben.  
  
> [!NOTE]  
>  Im vorherigen Beispiel der **IDBCreateCommand** Schnittstelle wird verwendet, da die **ICommand** -Schnittstelle implementiert die **GetDBSession** -Methode, die einzige Methode im Befehls- oder rowsetbereich, die einem Objekt Gelegenheit zu die Sitzung zu ermitteln, auf dem es erstellt wurde. Daher ermöglicht einzig ein Befehlsobjekt einer Anwendung das Abrufen eines Datenquellobjekt-Zeigers, von dem aus weitere Sitzungen erstellt werden können.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellenobjekte & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
