---
title: "CREATE DATABASE (Azure SQL­Datenbank) | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/28/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: cccf648270523e86e502caebfbc7f6ba6a55cfd7
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Erstellt eine neue Datenbank.  
  
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
    | ( EDITION = {  'basic' | 'standard' | 'premium' | 'premiumrs'}   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

[ AS COPY OF [source_server_name.]source_database_name ]

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>Argumente  
 Das Syntaxdiagramm veranschaulicht die in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] unterstützten Argumente.  
  
 *database_name*  
 Der Name der neuen Datenbank. Dieser Name muss auf dem SQL-Server, die beide hosten können eindeutig sein [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Datenbanken und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] -Datenbanken und entsprechen dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Regeln für Bezeichner entsprechen. Weitere Informationen finden Sie unter [Bezeichner](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
 *Sortierungsname*  
 Gibt die Standardsortierung für die Datenbank an. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Wenn keine Angabe erfolgt, wird der Datenbank die Standardsortierung, SQL_Latin1_General_CP1_CI_AS, zugewiesen.  
  
 Weitere Informationen zu den Windows- und SQL-Sortierungsnamen [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
 *CATALOG_COLLATION*  
Gibt die standardsortierung für den Metadatenkatalog an. *DATABASE_DEFAULT* gibt an, dass für die Metadatenkatalog verwendet Systemsichten und Systemtabellen, die die standardsortierung für die Datenbank entsprechend sortiert werden.  Dies ist das Verhalten in SQL Server gefunden. 

*SQL_Latin1_General_CP1_CI_AS* gibt an, dass für die Metadatenkatalog verwendet Systemsichten und-Tabellen in eine feste SQL_Latin1_General_CP1_CI_AS-Sortierung sortiert werden.  Dies ist die Standardeinstellung für Azure SQL-Datenbank, sofern nicht angegeben.

 *EDITION*  
 Gibt die Dienstebene der Datenbank an. Die verfügbaren Werte sind: 'basic','standard', 'Premium' und 'Premiumrs'.  
  
 Wenn EDITION angegeben ist, aber MAXSIZE nicht angegeben ist, wird MAXSIZE auf die restriktivste Größe festgelegt, die die Edition unterstützt.  
  
 *MAXSIZE*  
 Gibt die maximale Größe der Datenbank an. MAXSIZE muss für die angegebene EDITION (Dienstebene) gültig sein. Im Folgenden sind die unterstützten MAXSIZE-Werte und die Standardwerte (S) für die Dienstebenen aufgeführt.  
  
|**MAXSIZE**|**Standard**|**S0 S2**|**S3-S12**|**P1-P6 und PRS1 PRS6**| **P11-P15** 
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
|Von 1024 GB bis zu 4096 GB in Inkrementen von 256 GB * |–|–|–|–|√|√|  
  
 \*P11 und P15 können Sie MAXSIZE mit 1024 GB wird die standardmäßige Größe bis zu 4 TB.  P11 und P15 können bis zu 4 TB Speicher enthalten Aufpreis verwenden. In der Premium-Dienstebene MAXSIZE größer als 1 TB ist zurzeit in der folgenden Regionen verfügbar: uns East2, USA (Westen), uns Gov Virginia, Westeuropa, Deutschland zentralen, Süd Ostasien, Japan OST, Australien Osten, Kanada zentralen und Kanada Osten. Aktuelle Einschränkungen finden Sie unter [einzelner Datenbanken](https://docs.microsoft.com/azure/sql-database-single-database-resources).  
  
 Die folgenden Regeln gelten für das MAXSIZE-Argument und das EDITION-Argument:  
  
-   Falls angegeben, muss der MAXSIZE-Wert einem gültigen, in der Tabelle oben aufgeführten Wert entsprechen.  
  
-   Wenn EDITION angegeben ist, MAXSIZE jedoch nicht, wird der Standardwert für die Edition verwendet. Z. B. wenn die EDITION auf Standard festgelegt und MAXSIZE nicht angegeben ist, ist Klicken Sie dann der MaxSize-Wert automatisch auf 250 MB festgelegt.  
  
-   Wenn weder MAXSIZE noch EDITION angegeben ist, wird die EDITION, Standard (S0) festgelegt ist, und MAXSIZE auf 250 GB festgelegt.  
  
 SERVICE_OBJECTIVE  
 Gibt die Leistungsebene an. Dienst dienstzielbeschreibungen und Weitere Informationen über die Größe, Editionen und dienstzielkombinationen finden Sie unter [Azure SQL-Datenbank-Dienstebenen und Leistungsstufen](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) und [Ressource der SQL-Datenbank Grenzwerte](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits). Wenn der angegebene SERVICE_OBJECTIVE von der EDITION nicht unterstützt wird, erhalten Sie eine Fehlermeldung.  
  
 ELASTIC_POOL (Name = \<Elastic_pool_name >) zum Erstellen einer neuen Datenbank in einem elastischen Pool die SERVICE_OBJECTIVE von der Datenbank auf ELASTIC_POOL festgelegt, und geben Sie den Namen des Pools. Weitere Informationen finden Sie unter [erstellen und verwalten Sie einen Pool für elastische Datenbanken SQL-Datenbank (Vorschau)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/).  
  
 *ALS COPY OF [Name des Quellservers.] Name der Quelldatenbank*  
 Zum Kopieren einer Datenbank auf demselben oder einem anderen [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server.  
  
 *Name des Quellservers*  
 Der Name des [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Servers, auf dem sich die Quelldatenbank befindet. Dieser Parameter ist optional, wenn sich die Quell- und die Zieldatenbank auf demselben [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server befinden sollen.  
  
 Hinweis: Das `AS COPY OF`-Argument unterstützt nicht die vollqualifizierten eindeutigen Domänennamen. Das heißt, wenn der vollqualifizierte Domänenname des Servers `serverName.database.windows.net` ist, verwenden Sie `serverName` nur während des Datenbankkopiervorgangs.  
  
 *Name der Quelldatenbank*  
 Der Name der zu kopierenden Datenbank.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]unterstützt nicht die folgenden Argumente und Optionen bei Verwendung der `CREATE DATABASE` Anweisung:  
  
-   Parameter im Zusammenhang mit der physischen Platzierung der Datei, z. B. \<Filespec > und \<Dateigruppe >  
  
-   Externe Zugriffsoptionen wie DB_CHAINING und TRUSTWORTHY  
  
-   Anfügen einer Datenbank  
  
-   Service Broker-Optionen, wie ENABLE_BROKER, NEW_BROKER und ERROR_BROKER_CONVERSATIONS  
  
-   Datenbankmomentaufnahme  
  
 Weitere Informationen zu den Argumenten und der `CREATE DATABASE` -Anweisung finden Sie unter [CREATE DATABASE &#40; SQL Server Transact-SQL &#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Datenbanken in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] weisen einige Standardeinstellungen auf, die beim Erstellen der Datenbank festgelegt werden. Weitere Informationen zu diesen Standardeinstellungen finden Sie in der Liste der Werte in [DATABASEPROPERTYEX &#40; Transact-SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE bietet die Möglichkeit, die Größe der Datenbank zu beschränken. Die Größe der Datenbank den Wert für MAXSIZE erreicht, wird der Fehlercode 40544. In diesem Fall können Sie keine Daten einfügen oder aktualisieren oder neue Objekte (wie Tabellen, gespeicherte Prozeduren. Sichten und Funktionen) erstellen. Sie können jedoch weiterhin Daten lesen und löschen, Tabellen abschneiden, Tabellen und Indizes löschen sowie Indizes neu erstellen. Anschließend können Sie MAXSIZE auf einen Wert aktualisieren, der größer als die aktuelle Datenbankgröße ist, oder Sie löschen einige Daten, um Speicherplatz freizugeben. Eine Verzögerung von bis zu fünfzehn Minuten ist möglich, bevor Sie neue Daten einfügen können.  
  
> [!IMPORTANT]  
>  Die `CREATE DATABASE`-Anweisung muss die einzige Anweisung in einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch sein. 
  
 Um die Größe, Edition oder dienstzielwerte später ändern, verwenden [ALTER DATABASE &#40; Azure SQL-Datenbank &#41; ](../../t-sql/statements/alter-database-azure-sql-database.md).  

Das Argument CATALOG_COLLATION ist nur beim Erstellen der Datenbank verfügbar. 
  
## <a name="database-copies"></a>Datenbankkopien  
 Das Kopieren einer Datenbank mit der `CREATE DATABASE` Anweisung ist ein asynchroner Vorgang. Deshalb muss nicht für die volle Dauer des Kopiervorgangs eine Verbindung mit dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server bestehen. Die `CREATE DATABASE` Anweisung Steuerelement an den Benutzer zurückgegeben, nachdem der Eintrag in sys.databases erstellt, aber vor dem Kopieren der Datenbank abgeschlossen ist. Das heißt, die `CREATE DATABASE`-Anweisung wird erfolgreich ausgeführt, während der Datenbank-Kopiervorgang noch ausgeführt wird.  
  
-   Überwachung des Kopiervorgangs auf eine [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Server: Abfrage der `percentage_complete` oder `replication_state_desc` Spalten in der [Dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) oder `state` Spalte in der **sys.databases** Zeigen Sie an. Die [dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) Ansicht kann ebenfalls verwendet werden, wie er den Status von Datenbankvorgängen, wie die Datenbankkopie zurückgibt.  
  
 Sobald der Kopiervorgang erfolgreich abgeschlossen wurde, ist die Zieldatenbank im Hinblick auf Transaktionen mit der Quelldatenbank konsistent.  
  
 Die folgende Syntax und die folgenden semantischen Regeln gelten für die Verwendung des `AS COPY OF`-Arguments:  
  
-   Der Quellservername und der Servername für das Kopierziel können identisch oder unterschiedlich sein. Wenn sie identisch sind, wird dieser Parameter ist optional und standardmäßig der Serverkontext der aktuellen Sitzung verwendet wird.  
  
-   Die Namen der Quell- und der Zieldatenbank müssen angegeben werden. Diese Namen müssen eindeutig sein und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Regeln für Bezeichner entsprechen. Weitere Informationen finden Sie unter [Bezeichner](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
-   Die `CREATE DATABASE`-Anweisung muss im Kontext der master-Datenbank des [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Servers ausgeführt werden, auf dem die neue Datenbank erstellt wird.  
  
-   Nachdem der Kopiervorgang abgeschlossen wurde, muss die Zieldatenbank als unabhängige Datenbank verwaltet werden. Sie können die `ALTER DATABASE`-Anweisung und die `DROP DATABASE`-Anweisung unabhängig von der Quelldatenbank für die neue Datenbank ausführen. Außerdem können Sie die neue Datenbank in eine andere neue Datenbank kopieren.  
  
-   Der Zugriff auf die Quelldatenbank ist weiterhin möglich, solange der Datenbank-Kopiervorgang ausgeführt wird.  
  
 Weitere Informationen finden Sie unter [erstellen Sie eine Kopie einer Azure SQL-Datenbank mithilfe von Transact-SQL-](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Erstellen einer Datenbank ein Anmeldename müssen eine der folgenden sein:  
  
-   Der prinzipalanmeldung auf Serverebene  
  
-   Die Azure AD-Administrator für den lokalen Azure SQL-Server  
  
-   Eine Anmeldung ein Mitglied der `dbmanager` -Datenbankrolle  
  
 **Zusätzliche Anforderungen für die Verwendung von `CREATE DATABASE ... AS COPY OF` Syntax:** Anmeldenamens die Anweisung ausführt, auf dem lokalen Server zudem muss mindestens die `db_owner` auf dem Quellserver. Wenn die Anmeldung basiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung und die Anmeldung, die Ausführung der Anweisung auf dem lokalen Server benötigen kein entsprechenden Anmeldename für die Quelle [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Server, mit identischen Namen und Kennwort.  
  
## <a name="examples"></a>Beispiele  
Eine quick Start-Lernprogramm veranschaulicht, wie Sie mit einer Azure SQL-Datenbank mit SQL Server Management Studio eine Verbindung herstellen, finden Sie unter [Azure SQL-Datenbank: mit SQL Server Management Studio eine Verbindung herstellen und Daten Abfragen](/azure/sql-database/sql-database-connect-query-ssms).  
  
### <a name="simple-example"></a>Einfaches Beispiel  
 Ein einfaches Beispiel zum Erstellen einer Datenbank.  
  
```tsql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Einfaches Beispiel mit der Edition  
 Ein einfaches Beispiel zum Erstellen einer standard-Datenbank.  
  
```tsql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>Beispiel mit zusätzlichen Optionen  
 Ein Beispiel für mehrere Optionen.  
  
```tsql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>Eine Kopie erstellen  
 Beispiel für die Erstellung einer Kopie einer Datenbank.  
  
```tsql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>Erstellen einer Datenbank in einem elastischen Pool  
 Neue Datenbank erstellt mit dem Namen S3M100 Pool:  
  
```tsql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>Erstellen eine Kopie einer Datenbank auf einem anderen Server  
 Das folgende Beispiel erstellt eine Kopie der Db_original-Datenbank, in der Leistungsstufe P2 Db_copy für eine einzelne Datenbank.  Dies gilt unabhängig davon, ob Db_original in einem elastischen Pool oder eine Leistungsstufe für eine einzelne Datenbank.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 Das folgende Beispiel erstellt eine Kopie der Db_original-Datenbank, in einem elastischen Pool mit dem Namen ep1 Db_copy.  Dies gilt unabhängig davon, ob Db_original in einem elastischen Pool oder eine Leistungsstufe für eine einzelne Datenbank.  Wenn Db_original in einem elastischen Pool mit einem anderen Namen befindet, wird Db_copy weiterhin in ep1 erstellt.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>Erstellen Sie die Datenbank mit dem Wert der angegebenen Katalog-Sortierung

Im folgenden Beispiel wird die katalogsortierung zu DATABASE_DEFAULT, beim Erstellen der Datenbank, wodurch versetzt wird die katalogsortierung mit der Sortierung der Datenbank identisch sein.

```tsql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>Siehe auch  

-  [Sys. dm_database_copies &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40; Azure SQL-Datenbank &#41;](/sql-docs/docs/t-sql/statements/alter-database-azure-sql-database)   
    
  


