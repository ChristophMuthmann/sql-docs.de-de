---
title: CREATE DATABASE (Azure SQL-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SERVICE_OBJECTIVE
- SERVICE_OBJECTIVE_TSQL
- ELASTIC_POOL
- ELASTIC_POOL_TSQL
- EDITION
- EDITION_TSQL
- MAXSIZE
- MAXSIZE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVICE_OBJECTIVE
- ELASTIC_POOL
- EDITION SQL Database
- MAXSIZE SQL Database
ms.assetid: 22b167f7-ae86-490b-adb3-ec02ca1c1508
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de82cfb595559b738ca8db7d72acd620101d3995
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Erstellt eine neue Datenbank.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

## <a name="syntax"></a>Syntax  
  
``` 
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
{  
   (<edition_options> [, ...n])   
}  

[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }  ]
  
<edition_options> ::=   
{  

      MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }    
    | ( EDITION = {  'basic' | 'standard' | 'premium' }   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>Argumente  
 Das Syntaxdiagramm veranschaulicht die in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] unterstützten Argumente.  
  
 *database_name*  
 Der Name der neuen Datenbank. Dieser Name muss auf dem SQL-Server eindeutig sein, der [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]- und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]-Datenbanken hosten kann, und muss den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Regeln für Bezeichner entsprechen. Weitere Informationen finden Sie unter [Bezeichner](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
 *Collation_name*  
 Gibt die Standardsortierung für die Datenbank an. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Wenn keine Angabe erfolgt, wird der Datenbank die Standardsortierung, SQL_Latin1_General_CP1_CI_AS, zugewiesen.  
  
 Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
 *CATALOG_COLLATION*  
Gibt die Standardsortierung für den Metadatenkatalog an. *DATABASE_DEFAULT* gibt an, dass der Metadatenkatalog sortiert werden muss, der für Systemansichten und Systemtabellen verwendet wird, um der Standardsortierung der Datenbank zu entsprechen.  SQL Server weist dieses Verhalten auf. 

*SQL_Latin1_General_CP1_CI_AS* gibt an, dass der Metadatenkatalog, der für Systemansichten und -tabellen verwendet wird, für die feste Sortierung „SQL_Latin1_General_CP1_CI_AS“ sortiert werden muss.  Sofern nichts anderes angegeben ist, entspricht dies der Standardeinstellung für Azure SQL-Datenbank.

 *EDITION*  
 Gibt die Dienstebene der Datenbank an. Die verfügbaren Werte sind „basic“, „standard“ und „premium“. Der Support für „premiumrs“ wurde entfernt. Wenn Sie Fragen haben, wenden Sie sich an den E-Mail-Alias premium-rs@microsoft.com.
  
 Wenn EDITION angegeben ist, MAXSIZE jedoch nicht, wird MAXSIZE auf die restriktivste, von der Edition unterstützte Größe festgelegt.  
  
 *MAXSIZE*  
 Gibt die maximale Größe der Datenbank an. MAXSIZE muss für die angegebene EDITION (Dienstebene) gültig sein. Im Folgenden sind die unterstützten MAXSIZE-Werte und die Standardwerte (S) für die Dienstebenen aufgeführt.  
  
|**MAXSIZE**|**Grundlegend**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** 
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (S)|√|√|√|√|  
|5 GB|–|√|√|√|√|  
|10 GB|–|√|√|√|√|  
|20 GB|–|√|√|√|√|  
|30 GB|–|√|√|√|√|  
|40 GB|–|√|√|√|√|  
|50 GB|–|√|√|√|√|  
|100 GB|–|√|√|√|√|  
|150 GB|–|√|√|√|√|  
|200 GB|–|√|√|√|√|  
|250 GB|–|√ (S)|√ (S)|√|√|  
|300 GB|–|–|√|√|√|  
|400 GB|–|–|√|√|√|
|500 GB|–|–|√|√ (S)|√|
|750 GB|–|–|√|√|√|
|1024 GB|–|–|√|√|√ (S)|
|Von 1024 GB bis 4096 GB in Inkrementen von 256 GB* |–|–|–|–|√|√|  
  
 \* P11 und P15 ermöglichen, dass die Größe von MAXSIZE bis zu 4 TB beträgt, wobei 1024 GB die Standardgröße darstellt.  P11 und P15 können bis zu 4 TB des enthaltenen Speichers ohne Aufpreis verwenden. Im Premium-Tarif ist MAXSIZE von mehr als 1 TB derzeit in folgenden Regionen verfügbar: USA, Osten 2; USA, Westen; USA Gov Virginia; Europa, Westen; Deutschland, Mitte; Asien, Südosten; Australien, Osten; Kanada, Mitte; Kanada, Osten. Weitere Informationen zu derzeitigen Einschränkungen finden Sie unter [Single databases (Einzelne Datenbanken)](https://docs.microsoft.com/azure/sql-database-single-database-resources).  
<!---Loc Comment: Link [Single databases] is not working---> 
  
 Die folgenden Regeln gelten für das MAXSIZE-Argument und das EDITION-Argument:  
  
-   Falls angegeben, muss der MAXSIZE-Wert einem gültigen, in der Tabelle oben aufgeführten Wert entsprechen.  
  
-   Wenn EDITION angegeben ist, MAXSIZE jedoch nicht, wird der Standardwert für die Edition verwendet. Wenn EDITION beispielsweise auf „Standard“ festgelegt und MAXSIZE nicht angegeben ist, wird MAXSIZE automatisch auf 250 MB festgelegt.  
  
-   Wenn weder MAXSIZE noch EDITION angegeben sind, wird EDITION auf „Standard“ (S0) und MAXSIZE auf 250 GB festgelegt.  
  
 SERVICE_OBJECTIVE  
 Gibt die Leistungsebene an. Dienstzielbeschreibungen und weitere Informationen zu Größe, Editionen und Dienstzielkombinationen finden Sie unter [Azure SQL Database Service Tiers and Performance Levels (Dienstebenen und Leistungsstufen von Azure SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) und [SQL Database resource limits (Ressourcenlimits von SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits). Wenn der angegebene SERVICE_OBJECTIVE von der EDITION nicht unterstützt wird, erhalten Sie eine Fehlermeldung.  
  
 ELASTIC_POOL (name = \<elastic_pool_name>) Legen Sie zum Erstellen einer neuen Datenbank in einem Pool für elastische Datenbanken das Schlüsselwort SERVICE_OBJECTIVE der Datenbank auf ELASTIC_POOL fest, und stellen Sie den Namen des Pools bereit. Weitere Informationen finden Sie unter [Create and manage a SQL Database elastic database pool (preview) (Erstellen und Verwalten eines Pool für elastische Datenbanken von SQL-Datenbank (Vorschau))](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/).  
  
 *AS COPY OF [source_server_name.]source_database_name*  
 Zum Kopieren einer Datenbank auf demselben oder einem anderen [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server.  
  
 *source_server_name*  
 Der Name des [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Servers, auf dem sich die Quelldatenbank befindet. Dieser Parameter ist optional, wenn sich die Quell- und die Zieldatenbank auf demselben [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server befinden sollen.  
  
 Hinweis: Das `AS COPY OF`-Argument unterstützt nicht die vollqualifizierten eindeutigen Domänennamen. Das heißt, wenn der vollqualifizierte Domänenname des Servers `serverName.database.windows.net` ist, verwenden Sie `serverName` nur während des Datenbankkopiervorgangs.  
  
 *source_database_name*  
 Der Name der zu kopierenden Datenbank.  
  
 Folgende Argumente und Optionen werden nicht von [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] unterstützt, wenn die `CREATE DATABASE`-Anweisung verwendet wird:  
  
-   Parameter im Zusammenhang mit der physischen Platzierung der Datei, z.B. \<filespec> und \<filegroup>  
  
-   Externe Zugriffsoptionen wie DB_CHAINING und TRUSTWORTHY  
  
-   Anfügen einer Datenbank  
  
-   Service Broker-Optionen, wie ENABLE_BROKER, NEW_BROKER und ERROR_BROKER_CONVERSATIONS  
  
-   Datenbankmomentaufnahme  
  
 Weitere Informationen zu den Argumenten und der `CREATE DATABASE`-Anweisung finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Datenbanken in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] weisen einige Standardeinstellungen auf, die beim Erstellen der Datenbank festgelegt werden. Weitere Informationen zu diesen Standardeinstellungen finden Sie in der Liste der Werte unter [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE bietet die Möglichkeit, die Größe der Datenbank zu beschränken. Wenn die Größe der Datenbank den Wert von MAXSIZE erreicht, erhalten Sie den Fehlercode 40544. In diesem Fall können Sie keine Daten einfügen oder aktualisieren oder neue Objekte (wie Tabellen, gespeicherte Prozeduren. Sichten und Funktionen) erstellen. Sie können jedoch weiterhin Daten lesen und löschen, Tabellen abschneiden, Tabellen und Indizes löschen sowie Indizes neu erstellen. Anschließend können Sie MAXSIZE auf einen Wert aktualisieren, der größer als die aktuelle Datenbankgröße ist, oder Sie löschen einige Daten, um Speicherplatz freizugeben. Eine Verzögerung von bis zu fünfzehn Minuten ist möglich, bevor Sie neue Daten einfügen können.  
  
> [!IMPORTANT]  
>  Die `CREATE DATABASE`-Anweisung muss die einzige Anweisung in einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch sein. 
  
 Verwenden Sie [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md), um die Größe, Edition oder die Dienstzielwerte im Nachhinein zu ändern.  

Das Argument CATALOG_COLLATION ist nur während der Erstellung der Datenbank verfügbar. 
  
## <a name="database-copies"></a>Datenbankkopien  
 Beim Kopieren einer Datenbank mit der `CREATE DATABASE`-Anweisung handelt es sich um einen asynchronen Vorgang. Deshalb muss nicht für die volle Dauer des Kopiervorgangs eine Verbindung mit dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server bestehen. Die `CREATE DATABASE`-Anweisung gibt die Steuerung an den Benutzer zurück, nachdem der Eintrag in „sys.databases“ erstellt, aber bevor der Kopiervorgang der Datenbank abgeschlossen wurde. Das heißt, die `CREATE DATABASE`-Anweisung wird erfolgreich ausgeführt, während der Datenbank-Kopiervorgang noch ausgeführt wird.  
  
-   Überwachen Sie den Kopiervorgang auf einem [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]-Server, indem Sie die `percentage_complete`- oder `replication_state_desc`-Spalten von [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) oder die `state`-Spalte in der Ansicht **sys.databases** abfragen. Die Ansicht [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) kann ebenfalls verwendet werden, da diese den Status von Datenbankvorgängen zurückgibt, z.B. den des Kopiervorgangs der Datenbank.  
  
 Sobald der Kopiervorgang erfolgreich abgeschlossen wurde, ist die Zieldatenbank im Hinblick auf Transaktionen mit der Quelldatenbank konsistent.  
  
 Die folgende Syntax und die folgenden semantischen Regeln gelten für die Verwendung des `AS COPY OF`-Arguments:  
  
-   Der Quellservername und der Servername für das Kopierziel können identisch oder unterschiedlich sein. Wenn diese identisch sind, ist dieser Parameter optional, und es wird standardmäßig der Serverkontext der aktuellen Sitzung verwendet.  
  
-   Die Namen der Quell- und der Zieldatenbank müssen angegeben werden. Diese Namen müssen eindeutig sein und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Regeln für Bezeichner entsprechen. Weitere Informationen finden Sie unter [Bezeichner](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
-   Die `CREATE DATABASE`-Anweisung muss im Kontext der master-Datenbank des [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Servers ausgeführt werden, auf dem die neue Datenbank erstellt wird.  
  
-   Nachdem der Kopiervorgang abgeschlossen wurde, muss die Zieldatenbank als unabhängige Datenbank verwaltet werden. Sie können die `ALTER DATABASE`-Anweisung und die `DROP DATABASE`-Anweisung unabhängig von der Quelldatenbank für die neue Datenbank ausführen. Außerdem können Sie die neue Datenbank in eine andere neue Datenbank kopieren.  
  
-   Der Zugriff auf die Quelldatenbank ist weiterhin möglich, solange der Datenbank-Kopiervorgang ausgeführt wird.  
  
 Weitere Informationen finden Sie unter [Create a copy of an Azure SQL database using Transact-SQL (Erstellen einer Kopie einer Azure SQL-Datenbank mithilfe von Transact-SQL)](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).  
  
## <a name="permissions"></a>Berechtigungen  
 Für das Erstellen einer Datenbank muss das Konto des Benutzers einem der Folgenden entsprechen:  
  
-   Dem Prinzipalkonto auf Serverebene  
  
-   Dem Azure AD-Administrator für den lokalen Azure SQL-Server  
  
-   Einem Konto, das Mitglied der `dbmanager`-Datenbankrolle ist  
  
 **Zusätzliche Anforderungen für die Verwendung der `CREATE DATABASE ... AS COPY OF`-Syntax:** Der Benutzer, der die Anweisung auf dem lokalen Server ausführt, muss mindestens dem `db_owner` (Datenbankbesitzer) des Quellservers entsprechen. Wenn das Konto auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung basiert, muss der Benutzer, der die Anweisung auf dem lokalen Server ausführt, über passende Anmeldeinformationen (mit identischem Namen und Kennwort) für den Quellserver [!INCLUDE[ssSDS](../../includes/sssds-md.md)] besitzen.  
  
## <a name="examples"></a>Beispiele  
Ein Tutorial für den Schnellstart, das das Herstellen einer Verbindung zu einer Datenbank von Azure SQL mithilfe von SQL Server Management Studio veranschaulicht, finden Sie unter [Azure SQL-Datenbank: Verwenden von SQL Server Management Studio zum Herstellen der Verbindung und Abfragen von Daten](/azure/sql-database/sql-database-connect-query-ssms).  
  
### <a name="simple-example"></a>Einfaches Beispiel  
 Ein einfaches Beispiel für das Erstellen einer Datenbank.  
  
```sql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Einfaches Beispiel mit „Edition“  
 Ein einfaches Beispiel für das Erstellen einer Standarddatenbank.  
  
```sql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>Beispiel mit zusätzlichen Optionen  
 Ein Beispiel, bei dem mehrere Optionen verwendet werden.  
  
```sql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>Erstellen einer Kopie  
 Ein Beispiel, in dem die Kopie einer Datenbank erstellt wird.  
  
```sql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>Erstellen einer Datenbank in einem elastischen Pool  
 Erstellt eine neue Datenbank in einem Pool namens „S3M100“:  
  
```sql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>Erstellen einer Kopie einer Datenbank auf einem anderen Server  
 Im folgenden Beispiel wird eine Kopie der Datenbank „db_original“ namens „db_copy“ in der P2-Leistungsstufe für eine einzelne Datenbank erstellt.  Dies gilt unabhängig davon, ob „db_original“ sich in einem elastischen Pool oder in einer Leistungsstufe für eine einzelne Datenbank befindet.  
  
```sql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 Im folgenden Beispiel wird eine Kopie der Datenbank „db_original“ namens „db_copy“ in einem elastischen Pool namens „ep1“ erstellt.  Dies gilt unabhängig davon, ob „db_original“ sich in einem elastischen Pool oder in einer Leistungsstufe für eine einzelne Datenbank befindet.  Wenn es sich bei „db_original“ um einen elastischen Pool mit einem unterschiedlichen Namen handelt, wird „db_copy“ dennoch in „ep1“ erstellt.  
  
```sql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>Erstellen einer Datenbank mit einem angegebenen Wert für die Katalogsortierung

Im folgenden Beispiel wird die Katalogsortierung während der Erstellung der Datenbank auf DATABASE_DEFAULT festgelegt. Dadurch entspricht die Katalogsortierung der Datenbanksortierung.

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>Siehe auch  

-  [sys.dm_database_copies &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40;Azure SQL-Datenbank&#41;](alter-database-azure-sql-database.md)   
    
  

