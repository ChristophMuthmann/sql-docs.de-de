---
title: Andere Nicht-SQL Server-Abonnenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 024860422f6887b335e2e77ba33b3cd0f93c028b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="other-non-sql-server-subscribers"></a>Andere Nicht-SQL Server-Abonnenten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Eine Liste der von[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützten Nicht- [!INCLUDE[msCoName](../../../includes/msconame-md.md)]-Abonnenten finden Sie unter [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Dieses Thema enthält Informationen zu den Anforderungen für ODBC-Treiber und OLE DB-Anbieter.  
  
## <a name="odbc-driver-requirements"></a>Anforderungen für ODBC-Treiber  
 Der ODBC-Treiber muss folgende Voraussetzungen erfüllen:  
  
-   Er muss ODBC Level-1-kompatibel sein.  
  
-   Er muss um eine threadsichere Verteilerumgebung darstellen.  
  
-   Er muss in der Lage sein, Transaktionen zu verarbeiten.  
  
-   Er muss die Datendefinitionssprache (Data Definition Language, DDL) unterstützen.  
  
-   Er darf nicht schreibgeschützt sein.  
  
-   Er muss lange Tabellennamen unterstützen, wie z. B. **MSreplication_subscriptions**.  
  
## <a name="replicating-using-ole-db-interfaces"></a>Replikation mithilfe von OLE DB-Schnittstellen  
 OLE DB-Anbieter müssen folgende Objekte für die Transaktionsreplikation unterstützen.  
  
-   **DataSource** -Objekt  
  
-   **Session** -Objekt  
  
-   **Command** -Objekt  
  
-   **Rowset** -Objekt  
  
-   **Error** -Objekt  
  
### <a name="datasource-object-interfaces"></a>Schnittstellen für DataSource-Objekte  
 Die folgenden Schnittstellen sind erforderlich, um eine Verbindung mit einer Datenquelle herzustellen:  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 Wenn der Anbieter die **IDBInfo** -Schnittstelle unterstützt, verwendet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Schnittstelle zum Abrufen von Informationen, wie z. B. des Bezeichners in Anführungszeichen, der maximalen Länge einer SQL-Anweisung und der maximalen Anzahl von Zeichen in Tabellen- und Spaltennamen.  
  
### <a name="session-object-interfaces"></a>Schnittstellen für Session-Objekte  
 Die folgenden Schnittstellen sind erforderlich:  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### <a name="command-object-interfaces"></a>Schnittstellen für Command-Objekte  
 Die folgenden Schnittstellen sind erforderlich:  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** ist zum Erstellen von Parameterzugriffen erforderlich. Wenn der Anbieter **IColumnRowset**unterstützt, verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Schnittstelle, um zu bestimmen, ob eine Spalte eine Identitätsspalte ist.  
  
### <a name="rowset-object-interfaces"></a>Schnittstellen für Rowset-Objekte  
 Die folgenden Schnittstellen sind erforderlich:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 Eine Anwendung sollte ein Rowset für eine replizierte Tabelle öffnen, das in der Abonnementdatenbank erstellt wird. **IColumnsInfo** und **IAccessor** werden zum Zugreifen auf Daten im Rowset benötigt.  
  
### <a name="error-object-interfaces"></a>Schnittstellen für Error-Objekte  
 Verwenden Sie die folgenden Schnittstellen zur Verwaltung von Fehlern:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Verwenden Sie **ISQLErrorInfo** , wenn diese Schnittstelle vom OLE DB-Anbieter unterstützt wird.  
  
 Weitere Informationen zum OLE DB-Anbieter finden Sie in der Dokumentation zum jeweiligen OLE DB-Anbieter.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  
