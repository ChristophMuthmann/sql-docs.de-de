---
title: "Ändern der EXTERNEN Datenquelle (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16ea77011039c1b48ab83bfd335028c83c6f3c3e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ändert eine externe Datenquelle verwendet, um eine externe Tabelle zu erstellen. Die externe Datenquelle kann Hadoop oder Azure Blob Storage (WASB) sein.
  
## <a name="syntax"></a>Syntax  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later)
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumente  
 Data_source_name gibt den benutzerdefinierten Namen für die Datenquelle an. Der Name muss eindeutig sein.
  
 Speicherort = "Server_name_or_IP" gibt den Namen des Servers oder eine IP-Adresse.
  
 RESOURCE_MANAGER_LOCATION = "\<IP-Adresse; Port > "gibt den Speicherort der Hadoop-Ressourcen-Manager. Wenn angegeben, kann der Abfrageoptimierer entscheiden, um Daten für eine PolyBase-Abfrage mithilfe Hadoops-Datenverarbeitungsfunktionen vorab zu verarbeiten. Dies ist eine kostenbasierte Entscheidung. Prädikatweitergabe wird aufgerufen, kann dies erheblich reduzieren die Datenmenge, die zwischen Hadoop und SQL übertragen und aus diesem Grund die abfrageleistung.
  
 Anmeldeinformationen = Credential_Name gibt die benannten Anmeldeinformationen. Finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

TYP = BLOB_STORAGE   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Für Massenvorgänge nur `LOCATION` muss gültig sein. die URL in den Azure-Blob-Speicher. Nehmen Sie nicht  **/** , Dateinamen an oder freigegebene Signatur Zugriffsparameter am Ende der `LOCATION` URL.
Die Anmeldeinformationen verwendet, muss erstellt werden, mithilfe von `SHARED ACCESS SIGNATURE` als Identität. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  
  
## <a name="remarks"></a>Hinweise
 Nur einzelne Quelle kann zu einem Zeitpunkt geändert werden. Viele gleichzeitige Anforderungen die gleiche Quelle zu ändern dazu führen, dass eine Anweisung, die gewartet wird. Allerdings können die verschiedene Quellen gleichzeitig geändert werden. Diese Anweisung kann gleichzeitig mit anderen Anweisungen ausgeführt.
  
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