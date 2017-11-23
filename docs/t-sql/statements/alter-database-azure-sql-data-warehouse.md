---
title: ALTER_DATABASE (Azure SQL Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: "20"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 758f303efd228d806db53075f92cc8dd4664d40b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE (Azure SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Ändert den Namen, eine maximale Größe oder ein dienstziel für eine Datenbank.  
  
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
Gibt den Namen der Datenbank geändert werden.  

MODIFY NAME = *Name der neuen Datenbank*  
Benennt die Datenbank mit dem angegebenen als Namen *Name der neuen Datenbank*.  
  
MAXSIZE  
Der Standardwert ist 10.240 GB (10 TB).  

**Gilt für:** für Ebene von Elastizität Leistung optimiert

Die maximal zulässige Größe für die Datenbank. Die Datenbank kann nicht über MaxSize-Wert zu vergrößern. 

**Gilt für:** für Leistung berechnungsschicht optimiert

Die maximal zulässige Größe für Rowstore-Daten in der Datenbank. MAXSIZE können nicht in die Rowstore-Tabellen, Deltastore für einen columnstore-Index oder ein nicht gruppierter Index für einen gruppierten columnstore-Index gespeicherte Daten übersteigen.  Daten, die in den columnstore-Format komprimiert eine größenbeschränkung verfügt nicht über und werden von MAXSIZE nicht eingeschränkt. 
  
SERVICE_OBJECTIVE  
Gibt die Leistungsebene an. Weitere Informationen zu dienstziele für [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], finden Sie unter [Leistung Ebenen](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="permissions"></a>Berechtigungen  
Diese Berechtigungen sind erforderlich:  
  
-   Prinzipalanmeldung auf Serverebene (die 1 im Rahmen des Bereitstellungsprozesses erstellt), oder  
  
-   Mitglied der `dbmanager` -Datenbankrolle.  
  
Der Besitzer der Datenbank kann nicht die Datenbank nicht geändert werden, es sei denn, der Besitzer Mitglied ist die `dbmanager` Rolle.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Die aktuelle Datenbank muss auf einer anderen Datenbank als der Sie, daher ändern sind **ALTER muss ausgeführt werden, während mit der master-Datenbank verbunden**.  
  
SQL Data Warehouse ist in "130" COMPATIBILITY_LEVEL festgelegt und kann nicht geändert werden. Weitere Informationen finden Sie unter [verbessert die Abfrageleistung mit Kompatibilität Ebene 130 in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
Um die Größe einer Datenbank zu reduzieren, verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
Zum Ausführen von ALTER DATABASE, wird die Datenbank muss online sein und darf sich nicht in einem angehaltenen Zustand.  
  
ALTER DATABASE-Anweisung muss im Autocommit-Modus ausgeführt, das ist der Standardmodus zur transaktionsverwaltung. Dies wird in den Verbindungseinstellungen festgelegt.  
  
ALTER DATABASE-Anweisung darf nicht Teil einer benutzerdefinierten Transaktion sein.

Sie können die Sortierung der Datenbank nicht ändern.  
  
## <a name="examples"></a>Beispiele  
Bevor Sie diese Beispiele ausführen, stellen Sie sicher, dass die Datenbank aus, die Sie ändern möchten, nicht der aktuellen Datenbank ist. Die aktuelle Datenbank muss auf einer anderen Datenbank als der Sie, daher ändern sind **ALTER muss ausgeführt werden, während mit der master-Datenbank verbunden**.  

### <a name="a-change-the-name-of-the-database"></a>A. Ändern Sie den Namen der Datenbank  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. Ändern Sie die maximale Größe für die Datenbank  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. Ändern der Leistungsebene  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. Ändern der maximalen Größe und Leistungsstufe  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>Siehe auch  
[CREATE DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[SQL Data Warehouse-Liste der Referenzthemen](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
