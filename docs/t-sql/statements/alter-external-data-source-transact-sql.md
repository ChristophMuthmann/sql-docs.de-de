---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft-Dokumentation
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

  Ändert eine externe Datenquelle, die zum Erstellen einer externen Tabelle verwendet wird. Bei der externen Datenquelle kann es sich um einen Hadoop oder Azure Blob Storage (WASB) handeln.
  
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
  
 LOCATION = 'server_name_or_IP' gibt den Namen des Servers oder eine IP-Adresse an.
  
 RESOURCE_MANAGER_LOCATION = \<'IP address;Port'> gibt den Speicherort des Hadoop-Ressourcen-Managers an. Wenn angegeben, kann der Abfrageoptimierer festlegen, dass Daten für eine PolyBase-Abfrage mithilfe der Berechnungsfunktionen von Hadoop vorverarbeitet werden. Dies ist eine kostenbasierte Entscheidung. Dies wird Prädikatweitergabe genannt und kann die Menge der zwischen Hadoop und SQL übertragenen Daten deutlich reduzieren und damit die Abfrageleistung verbessern.
  
 CREDENTIAL = Credential_Name gibt die benannten Anmeldeinformationen an. Informationen hierzu finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

TYPE = BLOB_STORAGE   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Nur bei Massenvorgängen muss `LOCATION` die gültige URL für den Azure Blob Storage sein. Fügen Sie weder **/**, Dateinamen noch Shared Access Signature-Parameter am Ende der `LOCATION`-URL ein.
Die verwendeten Anmeldeinformationen müssen mithilfe von `SHARED ACCESS SIGNATURE` als Identität erstellt werden. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  
  
## <a name="remarks"></a>Remarks
 Es kann immer jeweils nur eine Quelle geändert werden. Gleichzeitige Anforderungen zur Änderung derselben Quelle führen dazu, dass eine Anweisung warten muss. Unterschiedliche Quellen können jedoch gleichzeitig geändert werden. Diese Anweisung kann gleichzeitig mit anderen Anweisungen ausgeführt werden.
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert eine ALTER ANY EXTERNAL DATA SOURCE-Berechtigung.
 > [!IMPORTANT]  
 >  Mit der Berechtigung ALTER ANY EXTERNAL DATA SOURCE besitzt jeder Prinzipal die Fähigkeit, beliebige externe Datenquellenobjekte zu erstellen und zu ändern. Damit ist auch der Zugriff auf alle datenbankweit gültigen Anmeldeinformationen der Datenbank möglich. Da es sich hierbei um eine weitreichende Berechtigung handelt, darf sie nur vertrauenswürdigen Prinzipalen innerhalb des Systems erteilt werden.

  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Speicherort und der Ressourcen-Manager-Speicherort einer vorhandenen Datenquelle geändert.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```  

 Im folgenden Beispiel werden die Anmeldeinformationen zur Verbindung mit einer vorhandenen Datenquelle geändert.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```