---
title: Erstellen der Datenbank (Azure SQL Datawarehouse) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/14/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 42819b93-b757-4b2c-8179-d4be3c512c19
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a178756610f0d0e463c21a2a62a287ada6c863a1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-azure-sql-data-warehouse"></a>Erstellen der Datenbank (Azure SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Erstellt eine neue Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB ,]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' }  
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
Die maximale Größe der Datenbank erreichen kann. Das Festlegen dieses Werts wird verhindert, dass die Vergrößerung der Datenbankgröße außerhalb der festgelegten Größe. Die Standardeinstellung *MAXSIZE* Wenn nicht angegeben ist 10240 GB (10 TB).  Weitere mögliche Werte reichen von 250 GB bis zu 240 TB.  
  
SERVICE_OBJECTIVE  
Gibt die Leistungsebene an. Weitere Informationen zu dienstziele für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], finden Sie unter [Skalierung Leistung auf SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-performance-scale/).  
  
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
  


