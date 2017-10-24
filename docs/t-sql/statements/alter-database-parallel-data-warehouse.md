---
title: ALTER_DATABASE (Parallel Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74b47bec1033728d47e5fe577af29c6d43e9af65
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (Parallel Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Ändert die maximale Größe Datenbankoptionen für replizierte Tabellen, verteilte Tabellen und das Transaktionsprotokoll in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Verwenden Sie diese Anweisung, um die speicherplatzzuordnungen für eine Datenbank zu verwalten, wie es vergrößert oder verkleinert die Größe.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Der Name der Datenbank geändert werden. Verwenden Sie zum Anzeigen einer Liste der Datenbanken auf dem Gerät [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 AUTOMATISCHE VERGRÖSSERUNG = {ON | {OFF}  
 Die Option "AUTOGROW" wird aktualisiert. Wenn die automatische VERGRÖßERUNG auf ON festgelegt ist [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] automatisch nach Bedarf für Wachstum in speicheranforderungen erhöht die speicherplatzbelegung für replizierte Tabellen, verteilte Tabellen und das Transaktionsprotokoll. Wenn die automatische VERGRÖßERUNG auf OFF festgelegt ist [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gibt einen Fehler zurück, wenn Tabellen repliziert verteilte Tabellen oder das Transaktionsprotokoll überschreitet die maximale Größe festlegen.  
  
 REPLICATED_SIZE = *Größe* [GB]  
 Gibt die neue maximale Gigabyte pro Serverknoten zum Speichern von allen replizierten Tabellen in der Datenbank geändert wird. Wenn Sie bei der Planung für Appliance Speicherplatz müssen Sie die Anzahl von Serverknoten in der Einheit REPLICATED_SIZE multiplizieren.  
  
 DISTRIBUTED_SIZE = *Größe* [GB]  
 Gibt die neue maximale GB pro Datenbank zum Speichern von allen verteilte Tabellen in der Datenbank geändert wird. Die Größe wird auf alle der Serverknoten in der Anwendung verteilt.  
  
 LOG_SIZE = *Größe* [GB]  
 Gibt die neue maximale GB pro Datenbank zum Speichern aller den Transaktionsprotokollen in der Datenbank geändert wird. Die Größe wird auf alle der Serverknoten in der Anwendung verteilt.  
  
 VERSCHLÜSSELUNG {ON | {OFF}  
 Legt fest, ob die Datenbank verschlüsselt (ON) oder nicht verschlüsselt (OFF) werden soll. Verschlüsselung kann nur konfiguriert werden, für die [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Wenn [sp_pdw_database_encryption aktiviert werden](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) vorsieht **1**. Datenbank-Verschlüsselungsschlüssel muss erstellt werden, bevor die transparente datenverschlüsselung konfiguriert werden kann. Weitere Informationen über die datenbankverschlüsselung finden Sie unter [transparente datenverschlüsselung &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank an.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die Werte für REPLICATED_SIZE DISTRIBUTED_SIZE und LOG_SIZE kann größer als, gleich oder kleiner als die aktuellen Werte für die Datenbank.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Wachsen und Verkleinerungsvorgänge sind ungefähre Werte. Die resultierende tatsächliche Größe können von den Größenparameter abweichen.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]führt keine ALTER DATABASE-Anweisung als atomarer Vorgang. Wenn die Anweisung während der Ausführung abgebrochen wird, bleiben Änderungen, die bereits aufgetreten sind.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Akzeptiert eine gemeinsame Sperre für das Datenbankobjekt. Sie können eine Datenbank, die von einem anderen Benutzer zum Lesen oder Schreiben verwendet wird, nicht ändern. Dies schließt Sitzungen, die ausgegeben haben eine [verwenden](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) -Anweisung für die Datenbank.  
  
## <a name="performance"></a>Leistung  
 Verkleinern einer Datenbank dauert eine große Menge an Zeit und Ressourcen, je nach Größe der tatsächlichen Daten innerhalb der Datenbank und die Menge der Fragmentierung auf dem Datenträger. Verkleinern einer Datenbank kann z. B. die mehrere Stunden oder länger dauern.  
  
## <a name="determining-encryption-progress"></a>Bestimmen des Status der Verschlüsselung  
 Verwenden Sie die folgende Abfrage, um Fortschritt der transparenten datenbankverschlüsselung als Prozentsatz zu bestimmen:  
  
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
  
 Ein umfangreiches Beispiel für alle Schritte bei der Implementierung von TDE veranschaulichen, finden Sie unter [transparente datenverschlüsselung &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Die Einstellung für die automatische VERGRÖßERUNG ändern  
 Automatische VERGRÖßERUNG für die Datenbank auf ON festgelegt `CustomerSales`.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Ändern den maximalen Speicherplatz für replizierte Tabellen  
 Im folgenden Beispiel wird die Speicherobergrenze für den replizierten Tabelle auf 1 GB für die Datenbank `CustomerSales`. Dies ist die speicherbegrenzung pro Compute-Knoten.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Ändern den maximalen Speicherplatz für verteilte Tabellen  
 Im folgenden Beispiel wird die Speicherobergrenze für den verteilten Tabelle bis zu 1000 GB (ein Terabyte), für die Datenbank `CustomerSales`. Dies ist die Speicherobergrenze für den kombinierten für das Gerät für alle von der Compute-Knoten nicht die Speicherobergrenze für pro-Serverknoten.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Ändern den maximalen Speicherplatz für das Transaktionsprotokoll  
 Das folgende Beispiel aktualisiert die Datenbank `CustomerSales` höchstens verfügen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Größe des Transaktionsprotokolls von 10 GB für die Anwendung.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die Datenbank &#40; Parallel Datawarehouse &#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  

