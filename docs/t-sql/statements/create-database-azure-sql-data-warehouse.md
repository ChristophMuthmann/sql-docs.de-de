---
title: Erstellen der Datenbank (Azure SQL Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 10/16/2017
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 7406a538eb4c0f236f2e0d444e96fd2c4fa5d585
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-database-azure-sql-data-warehouse"></a>Erstellen der Datenbank (Azure SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Erstellt eine neue Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 
        | 153600 | 204800 | 245760 
      } GB ,
    ]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' 
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' 
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' 
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }  
)  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
*database_name*  
Der Name der neuen Datenbank. Dieser Name muss auf dem SQL-Server, die beide hosten können eindeutig sein [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Datenbanken und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] -Datenbanken und entsprechen dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Regeln für Bezeichner entsprechen. Weitere Informationen finden Sie unter [Bezeichner](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*Sortierungsname*  
Gibt die Standardsortierung für die Datenbank an. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Wenn nicht angegeben, wird der Datenbank die standardsortierung zugewiesen, also SQL_Latin1_General_CP1_CI_AS.  
  
Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
*EDITION*  
Gibt die Dienstebene der Datenbank an. Für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] "Data Warehouse" verwenden.  
  
*MAXSIZE*  
Der Standardwert ist 10.240 GB (10 TB).  

**Gilt für:** für Ebene von Elastizität Leistung optimiert

Die maximal zulässige Größe für die Datenbank. Die Datenbank kann nicht über MaxSize-Wert zu vergrößern. 

**Gilt für:** für Leistung berechnungsschicht optimiert

Die maximal zulässige Größe für Rowstore-Daten in der Datenbank. MAXSIZE können nicht in die Rowstore-Tabellen, Deltastore für einen columnstore-Index oder ein nicht gruppierter Index für einen gruppierten columnstore-Index gespeicherte Daten übersteigen.  Daten, die in den columnstore-Format komprimiert eine größenbeschränkung verfügt nicht über und werden von MAXSIZE nicht eingeschränkt.
  
SERVICE_OBJECTIVE  
Gibt die Leistungsebene an. Weitere Informationen zu dienstziele für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], finden Sie unter [Leistung Ebenen](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Verwendung [DATABASEPROPERTYEX &#40; Transact-SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md) um die Datenbankeigenschaften anzuzeigen.  
  
Verwendung [ALTER DATABASE &#40; Azure SQL Datawarehouse &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) zum Ändern der maximalen Größe oder Objective-Werte später service.   

SQL Data Warehouse ist in "130" COMPATIBILITY_LEVEL festgelegt und kann nicht geändert werden. Weitere Informationen finden Sie unter [verbessert die Abfrageleistung mit Kompatibilität Ebene 130 in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
## <a name="permissions"></a>Berechtigungen  
Erforderliche Berechtigungen:  
  
-   Serverebenenprinzipal-Anmeldung, indem Sie im Rahmen des Bereitstellungsprozesses erstellt oder  
  
-   Mitglied der `dbmanager` -Datenbankrolle.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
Wenn die Größe der Datenbank den Wert für MAXSIZE erreicht, erhalten Sie Fehlercode 40544 ausgegeben. In diesem Fall können Sie eingefügt und Daten aktualisieren oder neue Objekte (z. B. Tabellen, gespeicherte Prozeduren, Sichten und Funktionen) erstellen. Sie können weiterhin lesen und Löschen von Daten, Tabellen abschneiden, Tabellen und Indizes löschen und Neuerstellen von Indizes. Anschließend können Sie MAXSIZE auf einen Wert aktualisieren, der größer als die aktuelle Datenbankgröße ist, oder Sie löschen einige Daten, um Speicherplatz freizugeben. Eine Verzögerung von bis zu fünfzehn Minuten ist möglich, bevor Sie neue Daten einfügen können.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
Es muss eine Verbindung mit der master-Datenbank bestehen, um eine neue Datenbank zu erstellen.  
  
Die `CREATE DATABASE`-Anweisung muss die einzige Anweisung in einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch sein.

Die Sortierung der Datenbank kann nicht geändert werden, nachdem die Datenbank erstellt wird.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>Beispiele:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
Ein einfaches Beispiel zum Erstellen einer Datawarehouse-Datenbank. Dadurch wird die Datenbank mit der kleinsten Max. Größe, die ist 10240 GB, die standardsortierung, SQL_Latin1_General_CP1_CI_AS also und das kleinste rechenleistung DW100 also erstellt.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Erstellen Sie eine Datawarehouse-Datenbank mit allen Optionen  
Ein Beispiel zum Erstellen einer ein 10-TB-Datawarehouse mit allen Optionen.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>Siehe auch  
[ALTER DATABASE &#40; Azure SQL Datawarehouse &#40; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 
 [CREATE TABLE &#40; Azure SQL Datawarehouse &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)  
 [DROP DATABASE &#40; Transact-SQL &#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  

