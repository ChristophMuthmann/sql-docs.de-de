---
title: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b64dc761f5af95ab913291d6aa488ced8fba8cf
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Ändert die Eigenschaften von datenbankweit gültigen Anmeldeinformationen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Gibt den Namen der datenbankweit gültigen Anmeldeinformationen an, die geändert werden.  
  
 IDENTITY **='***identity_name***'**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird. Zum Importieren einer Datei aus dem Azure Blob Storage muss `SHARED ACCESS SIGNATURE` als Identitätsname festgelegt werden.  Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
    
  
 SECRET **='***secret***'**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist. *secret* ist erforderlich, um eine Datei aus dem Azure Blob Storage zu importieren. *secret* kann für andere Zwecke optional sein.   
>  [!WARNING]
>  Der SAS-Schlüssel beginnt mit einem Fragezeichen (?). Wenn Sie den SAS-Schlüssel verwenden, müssen Sie das vorangestellte Fragezeichen entfernen. Andernfalls funktioniert der Vorgang nicht.    
  
## <a name="remarks"></a>Remarks  
 Wenn datenbankweit gültige Anmeldeinformationen geändert werden, werden die Werte von *identity_name* und *secret* zurückgesetzt. Falls das optionale SECRET-Argument nicht angegeben wird, wird der Wert des gespeicherten Kennworts auf NULL festgelegt.  
  
 Das Kennwort wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel erneut generiert wird, wird das Kennwort erneut mithilfe des neuen Diensthauptschlüssels verschlüsselt.  
  
 Informationen zu datenbankweit gültigen Anmeldeinformationen werden in der [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)-Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `ALTER`-Berechtigung für die Anmeldeinformationen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. Ändern des Kennworts für datenbankweit gültige Anmeldeinformationen  
 Im folgenden Beispiel wird das Kennwort, das in den datenbankweit gültigen Anmeldeinformationen namens `Saddles` gespeichert ist, geändert. Diese datenbankweit gültigen Anmeldeinformationen enthalten den Windows-Anmeldenamen `RettigB` und das zugehörige Kennwort. Das neue Kennwort wird den datenbankweit gültigen Anmeldeinformationen mithilfe der SECRET-Klausel hinzugefügt.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Entfernen des Kennworts aus Anmeldeinformationen  
 Im folgenden Beispiel wird das Kennwort aus datenbankweit gültigen Anmeldeinformationen namens `Frames` entfernt. Diese datenbankweit gültigen Anmeldeinformationen enthalten den Windows-Anmeldenamen `Aboulrus8` und ein Kennwort. Nach der Ausführung der Anweisung weisen die datenbankweit gültigen Anmeldeinformationen ein NULL-Kennwort auf, weil die Option SECRET nicht angegeben ist.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
