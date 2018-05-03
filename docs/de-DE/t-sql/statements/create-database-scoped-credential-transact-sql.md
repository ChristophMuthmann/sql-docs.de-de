---
title: CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE SCOPED CREDENTIAL
- DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_TSQL
- CREATE_DATABASE_SCOPED_CREDENTIAL
- CREATE_DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL
helpviewer_keywords:
- DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], DATABASE SCOPED CREDENTIAL statement
ms.assetid: fe830577-11ca-44e5-953b-2d589d54d045
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fed9bd89f0e1fbabb42458aa8901f0530dfaa859
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-database-scoped-credential-transact-sql"></a>CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Erstellt Datenbank-Anmeldeinformationen. Datenbank-Anmeldeinformationen werden nicht einer Serveranmeldung oder einem Datenbankbenutzer zugeordnet. Stattdessen werden sie von der Datenbank verwendet, damit immer dann der Zugriff auf den externen Speicherort gestattet wird, wenn die Datenbank einen Vorgang ausführt und hierfür eine Zugriffsberechtigung benötigt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Gibt den Namen für die datenbankweit gültigen Anmeldeinformationen an, die erstellt werden sollen. *credential_name* darf nicht mit dem Nummernzeichen (#) beginnen. Systemanmeldeinformationen beginnen mit zwei Nummernzeichen (##).  
  
 IDENTITY **='***identity_name***'**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird. Der Identitätsname muss `SHARED ACCESS SIGNATURE` entsprechen, um eine Datei aus Azure Blob Storage mithilfe eines Freigabeschlüssels zu importieren. Jeder gültige Wert kann für die Identität verwendet werden, um Daten in SQL Data Warehouse zu laden. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
  
 SECRET **='***secret***'**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist. `SECRET` ist erforderlich, um eine Datei aus Azure Blob Storage zu importieren. Der geheime Schlüssel muss der Azure Storage-Schlüssel sein, um von Azure Blob Storage in SQL Data Warehouse zu laden.  
>  [!WARNING]
>  Der SAS-Schlüssel beginnt mit einem Fragezeichen (?). Wenn Sie den SAS-Schlüssel verwenden, müssen Sie das vorangestellte Fragezeichen entfernen. Andernfalls funktioniert der Vorgang nicht.  
  
## <a name="remarks"></a>Remarks  
 Datenbezogene Anmeldeinformationen sind in einem Datensatz gespeichert, in dem die Authentifizierungsinformationen enthalten sind, die zum Herstellen einer Verbindung mit einer Ressource außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich sind. Die meisten Anmeldeinformationen schließen einen Windows-Benutzer und ein Kennwort ein.  
  
 Vor dem Erstellen von datenbankweit gültigen Anmeldeinformationen muss die Datenbank über einen Hauptschlüssel zum Schützen der Anmeldeinformationen verfügen. Weitere Informationen finden Sie unter [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 Falls für IDENTITY ein Windows-Benutzer angegeben ist, kann der geheime Bereich das Kennwort enthalten. Der geheime Bereich wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel neu generiert wird, wird der geheime Bereich mithilfe des neuen Diensthauptschlüssels neu verschlüsselt.  
   
 Informationen zu datenbankweit gültigen Anmeldeinformationen werden in der [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)-Katalogsicht angezeigt.  
  
 
 Im Folgenden werden einige Anwendungen datenbankweit gültiger Anmeldeinformationen aufgezeigt:  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verwendet datenbankweit gültige Anmeldeinformationen, um auf den nicht öffentlichen Blobspeicher von Azure Blob Storage oder auf durch Kerberos gesicherte Hadoop-Cluster mit PolyBase zuzugreifen. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] verwendet datenbankweit gültige Anmeldeinformationen, um mit PolyBase auf den nicht öffentlichen Blobspeicher von Azure Blob Storage zuzugreifen. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] verwendet datenbankweit gültige Anmeldeinformationen für das Feature für globale Abfragen. Dadurch können Abfragen für mehrere Datenbank-Shards gestellt werden.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] verwendet datenbankweit gültige Anmeldeinformationen, um Dateien für erweiterte Ereignisse in den Blobspeicher von Azure Blob Storage zu schreiben.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] verwendet datenbankweit gültige Anmeldeinformationen für Pools für elastische Datenbanken. Weitere Informationen finden Sie unter [Tame explosive growth with elastic databases (Verwenden von elastischen Datenbanken zum Abfangen von Lastspitzen)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/).  

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) verwenden datenbankweit gültige Anmeldeinformationen, um auf Daten aus dem Blobspeicher von Azure Blob Storage zuzugreifen. Weitere Informationen finden Sie unter [Beispiele für Massenzugriff auf Daten in Azure Blob Storage](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md). 
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **CONTROL**-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. Erstellen von datenbankweit gültigen Anmeldeinformationen für eine Anwendung
 Im folgenden Beispiel werden datenbankweit gültige Anmeldeinformationen mit der Bezeichnung `AppCred` erstellt. Die datenbankweit gültigen Anmeldeinformationen enthalten den Windows-Benutzer `Mary5` und ein Kennwort.  
  
```sql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. Erstellen von datenbankweit gültigen Anmeldeinformationen für eine SAS   
Im folgenden Beispiel werden datenbankweit gültige Anmeldeinformationen erstellt, durch die sich eine [externe Datenquelle](../../t-sql/statements/create-external-data-source-transact-sql.md) erstellen lässt. Mit dieser können Massenvorgänge wie [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) ausgeführt werden. Shared Access Signatures können nicht mit PolyBase in SQL Server, APS oder SQL Data Warehouse verwendet werden.
```sql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. Erstellen von datenbankweit gültigen Anmeldeinformationen für PolyBase-Konnektivität mit Azure Data Lake Store  
Im folgenden Beispiel werden datenbankweit gültige Anmeldeinformationen erstellt, durch die sich eine [externe Datenquelle](../../t-sql/statements/create-external-data-source-transact-sql.md) erstellen lässt. Diese kann von PolyBase in Azure SQL Data Warehouse verwendet werden.

Azure Data Lake Store verwendet eine Azure Active Directory-Anwendung für Dienst-zu-Dienst-Authentifizierungen.
Bevor Sie versuchen, datenbankweit gültige Anmeldeinformationen zu erstellen, ist es erforderlich, dass Sie [eine AAD-Anwendung](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) erstellen und sich die Werte für „client_id“, „OAuth_2.0_Token_EndPoint“ und „key“ notieren.

```sql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>Weitere Informationen  
 [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
