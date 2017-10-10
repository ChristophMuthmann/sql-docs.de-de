---
title: "Erstellen von ausgelegte Anmeldeinformationen für die Datenbank (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 49ff2aa300fc8f8e74424ae6e334bee823e8176c
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="create-database-scoped-credential-transact-sql"></a>Erstellen von ausgelegte Anmeldeinformationen für die Datenbank (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Erstellt einen Datenbank-Anmeldeinformationen. Datenbank-Anmeldeinformationen wird nicht für einen Server Anmelde- oder Benutzer zugeordnet. Die Anmeldeinformationen werden von der Datenbank verwendet, um den Zugriff auf den externen Speicherort jedes Mal, wenn die Datenbank einen Vorgang ausführt, der Zugriff benötigt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Gibt den Namen der datenbankweite Anmeldeinformationen erstellt wird. *Credential_name* darf nicht mit dem Nummernzeichen (#) beginnen. Systemanmeldeinformationen beginnen mit zwei Nummernzeichen (##).  
  
 Identität **= "***Identity_name***"**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird. Um eine Datei aus dem Azure-Blob-Speicher zu importieren, muss der Name der Identität `SHARED ACCESS SIGNATURE`.  Weitere Informationen zu SAS finden Sie unter [mithilfe von freigegebenen Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
  
 Geheime Schlüssel **= "***geheimen***"**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist. `SECRET`ist erforderlich, um eine Datei aus dem Azure-Blob-Speicher zu importieren.   
>  [!WARNING]
>  Die SAS-Schlüssel-Wert beginnt mit einem "?" (Fragezeichen). Wenn Sie den SAS-Schlüssel verwenden, müssen Sie das führende entfernen "?". Andernfalls können Ihren Aufwand blockiert werden.  
  
## <a name="remarks"></a>Hinweise  
 Datenbankweit gültigen Anmeldeinformationen wird ein Datensatz, der die Authentifizierungsinformationen, die erforderlich sind enthalten, für die Verbindung zu einer Ressource außerhalb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die meisten Anmeldeinformationen schließen einen Windows-Benutzer und ein Kennwort ein.  
  
 Vor dem Erstellen einer Datenbank Anmeldeinformationen als Bereiche besitzen, muss die Datenbank einen Hauptschlüssel zum Schützen der Anmeldeinformationen haben. Weitere Informationen finden Sie unter [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 Falls für IDENTITY ein Windows-Benutzer angegeben ist, kann der geheime Bereich das Kennwort enthalten. Der geheime Bereich wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel neu generiert wird, wird der geheime Bereich mithilfe des neuen Diensthauptschlüssels neu verschlüsselt.  
   
 Informationen zu datenbankbezogenen Anmeldeinformationen werden in der [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) -Katalogsicht angezeigt.  
  
 
 Hereare einige Anwendungen Datenbank beschränkt, Anmeldeinformationen:  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]verwendet eine datenbankbezogenen Anmeldeinformationen den Zugriff auf nicht öffentliche Azure-Blob-Speicher oder Kerberos-gesicherte Hadoop-Cluster mit PolyBase. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]verwendet eine datenbankweite Anmeldeinformationen an, die auf nicht öffentliche Azure-Blob-Speicher mit PolyBase. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]datenbankweit gültige Anmeldeinformationen für die Funktion globale Abfrage-Datenbank verwendet. Dies ist die Möglichkeit, die Abfrage mehrere datenbankshards.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]verwendet datenbankweit gültige Anmeldeinformationen zum Schreiben von Dateien für erweiterte Ereignisse in Azure Blob-Speicher.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]datenbankweit gültige Anmeldeinformationen für elastische Pools-Datenbank verwendet. Weitere Informationen finden Sie unter [komplexe dramatisch für elastische Datenbanken](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)  

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) datenbankweit gültige Anmeldeinformationen Zugriff auf Daten aus dem Azure-Blob-Speicher verwenden. Weitere Informationen finden Sie unter [Beispiele von Bulk Zugriff auf Daten in Azure Blob-Speicher](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md). 
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **Steuerelement** Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. Erstellen einer Datenbank werden Anmeldeinformationen für Ihre Anwendung begrenzt.
 Das folgende Beispiel erstellt die datenbankweite Anmeldeinformationen namens `AppCred`. Die datenbankbezogenen Anmeldeinformationen enthält, die Windows-Benutzer `Mary5` und ein Kennwort anzugeben.  
  
```tsql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. Erstellen einer Datenbank werden Anmeldeinformationen für eine shared Access Signature beschränkt.   
Das folgende Beispiel erstellt die datenbankweit gültigen Anmeldeinformationen, die verwendet werden kann, erstellen eine [externen Datenquelle](../../t-sql/statements/create-external-data-source-transact-sql.md), die möglich Massenvorgänge, z. B. [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). Signaturen für freigegebenen Zugriff kann nicht mit PolyBase in SQL Server, APS oder SQL Data Warehouse verwendet werden.
```tsql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. Erstellen einer Datenbank werden Anmeldeinformationen für die PolyBase-Verbindung mit Azure Data Lake-Speicher beschränkt.  
Das folgende Beispiel erstellt die datenbankweit gültigen Anmeldeinformationen, die verwendet werden kann, erstellen eine [externen Datenquelle](../../t-sql/statements/create-external-data-source-transact-sql.md), die von PolyBase in Azure SQL Data Warehouse verwendet werden können.

Azure Data Lake-Speicher verwendet eine Azure Active Directory-Anwendung für Service to Service-Authentifizierung.
Bitte [erstellen Sie eine AAD-Anwendung](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) und Dokumentieren Sie die "client_id", die OAuth_2.0_Token_EndPoint und den Schlüssel ein, bevor Sie versuchen, eine datenbankweite Anmeldeinformationen zu erstellen.

```tsql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>Weitere Informationen  
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER DATABASE ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

