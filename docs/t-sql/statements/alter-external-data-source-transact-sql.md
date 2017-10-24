---
title: "Ändern der EXTERNEN Datenquelle (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: f74a105226f1ae113287f1c337c1c33e81bb09ae
ms.contentlocale: de-de
ms.lasthandoff: 09/06/2017

---
# <a name="alter-external-data-source-transact-sql"></a>Ändern der EXTERNEN Datenquelle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Ändert eine externe Datenquelle verwendet, um eine externe Tabelle zu erstellen. Die externe Datenquelle kann Hadoop oder Azure Blob Storage (WASB) sein.  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later), Azure SQL Data Warehouse,
               Parallel Data Warehouse    
ALTER EXTERNAL DATA SOURCE data_source_name SET  
    {   
        LOCATION = 'server_name_or_IP' [,] |  
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |  
        CREDENTIAL = credential_name  
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017), Azure SQL Database,
               Azure SQL Data Warehouse, Parallel Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumente  
 data_source_name  
 Gibt den benutzerdefinierten Namen für die Datenquelle. Der Name muss eindeutig sein.  
  
 Speicherort = "Server_name_or_IP"  
 Gibt den Namen des Servers oder eine IP-Adresse.  
  
 RESOURCE_MANAGER_LOCATION = "\<IP-Adresse; Port > "  
 Gibt an, das Hadoop Ressourcenmanager-Speicherort. Wenn angegeben, kann der Abfrageoptimierer entscheiden, um Daten für eine PolyBase-Abfrage mithilfe Hadoops-Datenverarbeitungsfunktionen vorab zu verarbeiten. Dies ist eine kostenbasierte Entscheidung. Prädikatweitergabe wird aufgerufen, kann dies erheblich reduzieren die Datenmenge, die zwischen Hadoop und SQL übertragen und aus diesem Grund die abfrageleistung.  
  
 Anmeldeinformationen = Credential_Name  
 Gibt die benannten Anmeldeinformationen. Finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  

TYP = BLOB_STORAGE   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Für Massenvorgänge nur `LOCATION` muss gültig sein. die URL in den Azure-Blob-Speicher. Nehmen Sie nicht  **/** , Dateinamen an oder freigegebene Signatur Zugriffsparameter am Ende der `LOCATION` URL.   
Die Anmeldeinformationen verwendet, muss erstellt werden, mithilfe von `SHARED ACCESS SIGNATURE` als Identität. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  
  
## <a name="remarks"></a>Hinweise  
 Nur einzelne Quelle kann zu einem Zeitpunkt geändert werden. Viele gleichzeitige Anforderungen die gleiche Quelle zu ändern dazu führen, dass eine Anweisung, die gewartet wird. Allerdings können die verschiedene Quellen gleichzeitig geändert werden. Zudem kann dadurch diese Anweisung gleichzeitig mit anderen Anweisungen ausführen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY EXTERNAL DATA SOURCE-Berechtigung.  
 > [!IMPORTANT]  
 >  Die Berechtigung ALTER ANY EXTERNAL DATA SOURCE gewährt Prinzipal die Fähigkeit zum Erstellen und ändern alle externen Datenquellenobjekt und daher auch erteilt den Zugriff auf alle datenbankweit gültige Anmeldeinformationen für die Datenbank. Diese Berechtigung muss berücksichtigt werden, wie hoch privilegierten und daher im System nur für vertrauenswürdige Prinzipale erteilt werden müssen.

  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel ändert den Speicherort und Ressourcenmanager-Speicherort einer vorhandenen Datenquelle.  
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET  
     LOCATION = 'hdfs://10.10.10.10:8020',  
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'  
    ;  
  
```  
  
 Im folgenden Beispiel wird die Anmeldeinformationen zur Verbindung mit einer vorhandenen Datenquelle.  
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET  
   CREDENTIAL = new_hadoop_user  
    ;  
```  
  
  

