---
title: "Andere Nicht-SQL Server-Abonnenten | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Nicht-SQL Server-Abonnenten, andere Typen"
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Andere Nicht-SQL Server-Abonnenten
  Eine Liste der nicht -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] von Abonnenten unterstützt [!INCLUDE[msCoName](../../../includes/msconame-md.md)], finden Sie unter [nicht-SQL Server-Abonnenten](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Dieses Thema enthält Informationen zu den Anforderungen für ODBC-Treiber und OLE DB-Anbieter.  
  
## Anforderungen für ODBC-Treiber  
 Der ODBC-Treiber muss folgende Voraussetzungen erfüllen:  
  
-   Er muss ODBC Level-1-kompatibel sein.  
  
-   Er muss um eine threadsichere Verteilerumgebung darstellen.  
  
-   Er muss in der Lage sein, Transaktionen zu verarbeiten.  
  
-   Er muss die Datendefinitionssprache (Data Definition Language, DDL) unterstützen.  
  
-   Er darf nicht schreibgeschützt sein.  
  
-   Muss z. B. lange Tabellennamen unterstützen **MSreplication_subscriptions**.  
  
## Replikation mithilfe von OLE DB-Schnittstellen  
 OLE DB-Anbieter müssen folgende Objekte für die Transaktionsreplikation unterstützen.  
  
-   **DataSource** -Objekt  
  
-   **Session** -Objekt  
  
-   **Command** -Objekt  
  
-   **Rowset** -Objekt  
  
-   **Error** -Objekt  
  
### Schnittstellen für DataSource-Objekte  
 Die folgenden Schnittstellen sind erforderlich, um eine Verbindung mit einer Datenquelle herzustellen:  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 Wenn der Anbieter die **IDBInfo** -Schnittstelle unterstützt, verwendet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Schnittstelle zum Abrufen von Informationen, wie z. B. des Bezeichners in Anführungszeichen, der maximalen Länge einer SQL-Anweisung und der maximalen Anzahl von Zeichen in Tabellen- und Spaltennamen.  
  
### Schnittstellen für Session-Objekte  
 Die folgenden Schnittstellen sind erforderlich:  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### Schnittstellen für Command-Objekte  
 Die folgenden Schnittstellen sind erforderlich:  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** ist zum Erstellen von Parameterzugriffen erforderlich. Wenn der Anbieter **IColumnRowset**unterstützt, verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Schnittstelle, um zu bestimmen, ob eine Spalte eine Identitätsspalte ist.  
  
### Schnittstellen für Rowset-Objekte  
 Die folgenden Schnittstellen sind erforderlich:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 Eine Anwendung sollte ein Rowset für eine replizierte Tabelle öffnen, das in der Abonnementdatenbank erstellt wird. **IColumnsInfo** und **IAccessor** werden zum Zugreifen auf Daten im Rowset benötigt.  
  
### Schnittstellen für Error-Objekte  
 Verwenden Sie die folgenden Schnittstellen zur Verwaltung von Fehlern:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Verwenden Sie **ISQLErrorInfo** , wenn diese Schnittstelle vom OLE DB-Anbieter unterstützt wird.  
  
 Weitere Informationen zum OLE DB-Anbieter finden Sie in der Dokumentation zum jeweiligen OLE DB-Anbieter.  
  
## Siehe auch  
 [Nicht-SQL Server-Abonnenten](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  