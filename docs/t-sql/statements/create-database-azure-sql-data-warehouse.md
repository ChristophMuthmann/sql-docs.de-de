---
title: CREATE DATABASE (Azure SQL Data Warehouse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/14/20178
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 3a802dc74793ef79ca35b177b4416d9464a8c34f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="create-database-azure-sql-data-warehouse"></a>CREATE DATABASE (Azure SQL Data Warehouse)
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
Der Name der neuen Datenbank. Dieser Name muss auf dem SQL-Server eindeutig sein, der [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]- und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]-Datenbanken hosten kann, und muss den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Regeln für Bezeichner entsprechen. Weitere Informationen finden Sie unter [Bezeichner](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*collation_name*  
Gibt die Standardsortierung für die Datenbank an. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Wenn keine Angabe erfolgt, wird der Datenbank die Standardsortierung „SQL_Latin1_General_CP1_CI_AS“ zugewiesen.  
  
Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
*EDITION*  
Gibt die Dienstebene der Datenbank an. Verwenden Sie für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] „datawarehouse“.  
  
*MAXSIZE*  
Der Standardwert ist 245.760 GB (240 TB).  

**Gilt für:** Optimiert für Elastizitätsleistungsstufe

Der Wert für die maximal zulässige Größe der Datenbank Die Datenbank kann nicht größer sein als MAXSIZE. 

**Gilt für:** Optimiert für Computeleistungsstufe

Die maximal zulässige Größe für Rowstore-Daten in der Datenbank Daten, die in Rowstore-Tabellen, dem Deltastore eines Columnstore-Index oder einem nicht gruppierten Index für einen gruppierten Columnstore-Index gespeichert sind, können MAXSIZE nicht übersteigen.  Daten, die im Columnstore-Format komprimiert sind, haben kein Größenlimit und werden nicht durch MAXSIZE beschränkt.
  
SERVICE_OBJECTIVE  
Gibt die Leistungsebene an. Weitere Informationen zu Dienstzielen für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] finden Sie unter [Leistungsstufen](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Verwenden Sie [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md), um die Datenbankeigenschaften anzuzeigen.  
  
Verwenden Sie [ALTER DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md), um die Maximalgröße oder die Dienstzielwerte später zu ändern.   

SQL Data Warehouse ist auf COMPATIBILITY_LEVEL 130 festgelegt und kann nicht verändert werden. Weitere Informationen finden Sie unter [Verbesserte Abfrageleistung mit Kompatibilitätsgrad 130 in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
## <a name="permissions"></a>Berechtigungen  
Erforderliche Berechtigungen:  
  
-   Im Rahmen des Bereitstellungsprozesses erstellte Prinzipalanmeldung auf Serverebene oder  
  
-   Mitgliedschaft in der `dbmanager`-Datenbankrolle  
  
## <a name="error-handling"></a>Fehlerbehandlung  
Wenn die Größe der Datenbank den Wert von MAXSIZE erreicht, erhalten Sie den Fehlercode 40544. In diesem Fall können Sie keine Daten einfügen oder aktualisieren und keine neuen Objekte (wie Tabellen, gespeicherte Prozeduren, Ansichten und Funktionen) erstellen. Sie können jedoch weiterhin Daten lesen und löschen, Tabellen abschneiden, Tabellen und Indizes löschen, sowie Indizes neu erstellen. Anschließend können Sie MAXSIZE auf einen Wert aktualisieren, der größer als die aktuelle Datenbankgröße ist, oder Sie löschen einige Daten, um Speicherplatz freizugeben. Eine Verzögerung von bis zu fünfzehn Minuten ist möglich, bevor Sie neue Daten einfügen können.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
Es muss eine Verbindung mit der master-Datenbank bestehen, um eine neue Datenbank zu erstellen.  
  
Die `CREATE DATABASE`-Anweisung muss die einzige Anweisung in einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch sein.

Nachdem die Datenbank erstellt wurde, kann die Datenbanksortierung nicht mehr geändert werden.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
Ein einfaches Beispiel zum Erstellen einer Data Warehouse-Datenbank. Dadurch wird die Datenbank mit der kleinsten Maximalgröße von 10240 GB, der Standardsortierung „SQL_Latin1_General_CP1_CI_AS“ und der geringsten Computeleistung von DW100 erstellt.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Erstellen Sie eine Data Warehouse-Datenbank mit allen Optionen.  
Ein Beispiel zum Erstellen eines 10-TB-Data Warehouses mit allen Optionen.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[ALTER DATABASE &#40;Azure SQL Data Warehouse&#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
[CREATE TABLE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) 
[DROP DATABASE &#40;Transact-SQL&#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  

