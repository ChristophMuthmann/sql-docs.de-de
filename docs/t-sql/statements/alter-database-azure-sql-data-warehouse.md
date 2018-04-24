---
title: ALTER DATABASE (Azure SQL Data Warehouse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/15/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 893d777d40446be2feeb5583312877222be6707d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Ändert den Namen, die maximale Größe oder das Dienstziel einer Datenbank.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>Argumente  
*database_name*  
Gibt den Namen der zu ändernden Datenbank an.  

MODIFY NAME = *new_database_name*  
Benennt die Datenbank in den angegebenen Namen *new_database_name* um.  
  
MAXSIZE  
Der Standardwert ist 245.760 GB (240 TB).  

**Gilt für:** Optimiert für Elastizitätsleistungsstufe

Der Wert für die maximal zulässige Größe der Datenbank Die Datenbank kann nicht größer sein als MAXSIZE. 

**Gilt für:** Optimiert für Computeleistungsstufe

Die maximal zulässige Größe für Rowstore-Daten in der Datenbank Daten, die in Rowstore-Tabellen, dem Deltastore eines Columnstore-Index oder einem nicht gruppierten Index für einen gruppierten Columnstore-Index gespeichert sind, können MAXSIZE nicht übersteigen.  Daten, die im Columnstore-Format komprimiert sind, haben kein Größenlimit und werden nicht durch MAXSIZE beschränkt. 
  
SERVICE_OBJECTIVE  
Gibt die Leistungsebene an. Weitere Informationen zu Dienstzielen für [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] finden Sie unter [Leistungsstufen](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="permissions"></a>Berechtigungen  
Folgende Berechtigungen sind erforderlich:  
  
-   Der Prinzipalanmeldename auf Serverebene (der während des Bereitstellungsprozesses erstellt wurde) oder  
  
-   Mitgliedschaft in der `dbmanager`-Datenbankrolle  
  
Der Datenbankbesitzer kann die Datenbank nur ändern, wenn er Mitglied der Rolle `dbmanager` ist.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Bei der aktuellen Datenbank muss es sich um eine andere Datenbank als die handeln, die Sie ändern. Deshalb muss **ALTER ausgeführt werden, während eine Verbindung zur Masterdatenbank besteht**.  
  
SQL Data Warehouse ist auf COMPATIBILITY_LEVEL 130 festgelegt und kann nicht verändert werden. Weitere Informationen finden Sie unter [Verbesserte Abfrageleistung mit Kompatibilitätsgrad 130 in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
Verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md), um die Größe einer Datenbank zu reduzieren.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
Für die Ausführung von ALTER DATABASE muss die Datenbank online sein und darf sich nicht im angehaltenen Zustand befinden.  
  
Die ALTER DATABASE-Anweisung muss im Autocommitmodus ausgeführt werden. Dabei handelt es sich um den Standardmodus für die Transaktionsverwaltung. Dies wird in den Verbindungseinstellungen festgelegt.  
  
Die ALTER DATABASE-Anweisung darf nicht Teil einer benutzerdefinierten Transaktion sein.

Sie können die Datenbanksortierung nicht ändern.  
  
## <a name="examples"></a>Beispiele  
Stellen Sie vor dem Ausführen dieser Beispiele sicher, dass es sich bei der Datenbank, die Sie ändern, nicht um die aktuelle Datenbank handelt. Bei der aktuellen Datenbank muss es sich um eine andere Datenbank als die handeln, die Sie ändern. Deshalb muss **ALTER ausgeführt werden, während eine Verbindung zur Masterdatenbank besteht**.  

### <a name="a-change-the-name-of-the-database"></a>A. Ändern des Datenbanknamens  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. Ändern der maximalen Datenbankgröße  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. Ändern der Leistungsebene  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. Ändern der maximalen Größe und der Leistungsebene  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[CREATE DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[SQL Data Warehouse list of reference topics (Liste der SQL Data Warehouse-Referenzthemen)](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
