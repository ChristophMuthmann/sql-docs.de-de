---
title: ALTER DATABASE (Parallel Data Warehouse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0dd532ce7001c52d9fef2f3fd030fd6cf53e8a77
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Ändert die Optionen für die maximale Datenbankgröße für replizierte Tabellen und verteilte Tabellen sowie für das Transaktionsprotokoll in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Verwenden Sie diese Anweisung, um die Speicherplatzzuordnungen für eine Datenbank zu verwalten, wenn sich diese vergrößert oder verkleinert.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]  
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll. Um eine Liste von Datenbanken auf dem Gerät anzuzeigen, verwenden Sie [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 AUTOGROW = { ON | OFF }  
 Aktualisiert die Option AUTOGROW. Wenn AUTOGROW ON ist, erhöht [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] automatisch den zugeordneten Speicherplatz für replizierte Tabellen und verteilte Tabellen sowie das Transaktionsprotokoll nach Bedarf, um den gesteigerten Speicheranforderungen gerecht zu werden. Wenn AUTOGROW OFF ist, gibt [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] einen Fehler zurück, wenn replizierte Tabellen, verteilte Tabellen oder das Transaktionsprotokoll die Einstellung für die maximale Größe überschreiten.  
  
 REPLICATED_SIZE = *size* [GB]  
 Gibt die neue maximale Anzahl von Gigabyte pro Computeknoten für die Speicherung aller replizierten Tabellen in der Datenbank an, die geändert werden. Wenn Sie Appliancespeicherplatz planen, müssen Sie REPLICATED_SIZE mit der Anzahl der Computeknoten in der Appliance multiplizieren.  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 Gibt die neue maximale Anzahl von Gigabyte pro Datenbank für die Speicherung aller verteilten Tabellen in der Datenbank an, die geändert werden. Die Größe wird auf alle Computeknoten der Appliance verteilt.  
  
 LOG_SIZE = *size* [GB]  
 Gibt die neue maximale Anzahl von Gigabyte pro Datenbank für die Speicherung aller Transaktionsprotokolle in der Datenbank an, die geändert werden. Die Größe wird auf alle Computeknoten der Appliance verteilt.  
  
 ENCRYPTION { ON | OFF }  
 Legt fest, ob die Datenbank verschlüsselt (ON) oder nicht verschlüsselt (OFF) werden soll. Die Verschlüsselung kann nur für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] konfiguriert werden, wenn [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) auf **1** festgelegt wurde. Ein Datenbank-Verschlüsselungsschlüssel muss erstellt werden, bevor Transparent Data Encryption konfiguriert werden kann. Weitere Informationen zur Datenbankverschlüsselung finden Sie unter [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die Werte für REPLICATED_SIZE, DISTRIBUTED_SIZE und LOG_SIZE können größer, gleich oder kleiner als die aktuellen Werte für die Datenbank sein.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Vergrößerungs- und Verkleinerungsvorgänge sind ungenau. Die resultierenden tatsächlichen Größen können von den Größenparametern abweichen.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] führt die ALTER DATABASE-Anweisung nicht als unteilbaren Vorgang aus. Wenn die Anweisung während der Ausführung abgebrochen wird, bleiben Änderungen, die bereits durchgeführt wurden, erhalten.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Führt eine gemeinsame Sperre für das DATABASE-Objekt durch. Sie können eine Datenbank, die von einem anderen Benutzer im Lese- oder Schreibmodus verwendet wird, nicht ändern. Dies schließt auch Sitzungen ein, die eine [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15)-Anweisung für die Datenbank ausgeführt haben.  
  
## <a name="performance"></a>Leistung  
 Das Verkleinern einer Datenbank kann, abhängig von der Größe der tatsächlichen Daten innerhalb der Datenbank und der Menge der Fragmentierung auf dem Datenträger, viel Zeit und viele Systemressourcen in Anspruch nehmen. Das Verkleinern einer Datenbank könnte beispielsweise mehrere Stunden oder noch länger dauern.  
  
## <a name="determining-encryption-progress"></a>Bestimmen des Verschlüsselungsfortschritts  
 Verwenden Sie die folgende Abfrage, um den Fortschritt der transparenten Datenverschlüsselung für die Datenbank als Prozentsatz zu bestimmen:  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 Ein umfangreiches Beispiel mit allen Schritten zur Implementierung von TDE finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Ändern der AUTOGROW-Einstellung  
 Legen Sie AUTOGROW für die Datenbank `CustomerSales` auf ON fest.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Ändern des maximalen Speicherplatzes für replizierte Tabellen  
 Im folgenden Beispiel wird die Speicherbegrenzung für replizierte Tabellen für die Datenbank `CustomerSales` auf 1 GB festgelegt. Dabei handelt es sich um die Speicherbegrenzung pro Computeknoten.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Ändern des maximalen Speicherplatzes für verteilte Tabellen  
 Im folgenden Beispiel wird die Speicherbegrenzung für verteilte Tabellen für die Datenbank `CustomerSales` auf 1000 GB (ein Terabyte) festgelegt. Dabei handelt es sich um die gemeinsame Speicherbegrenzung für alle Computeknoten der Appliance und nicht um die Speicherbegrenzung pro Computeknoten.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Ändern des maximalen Speicherplatzes für das Transaktionsprotokoll  
 Im folgenden Beispiel wird die Datenbank `CustomerSales` so aktualisiert, dass die maximale Größe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Transaktionsprotokolls für die Appliance 10 GB beträgt.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
