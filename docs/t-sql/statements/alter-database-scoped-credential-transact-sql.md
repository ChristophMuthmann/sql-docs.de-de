---
title: ALTER DATABASE ausgelegte CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b45b0d87b846c50abc678692021c427006b3152e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE ausgelegte CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Ändert die Eigenschaften einer Datenbank im Bereich einer Anmeldeinformationen aus.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Gibt den Namen der datenbankweite Anmeldeinformationen, die geändert wird.  
  
 Identität **= "***Identity_name***"**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird. Um eine Datei aus dem Azure-Blob-Speicher zu importieren, muss der Name der Identität `SHARED ACCESS SIGNATURE`.  Weitere Informationen zu SAS finden Sie unter [mithilfe von freigegebenen Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
    
  
 Geheime Schlüssel **= "***geheimen***"**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist. *geheime* ist erforderlich, um eine Datei aus dem Azure-Blob-Speicher zu importieren. *geheime* möglicherweise für andere Zwecke ausgelassen werden.   
>  [!WARNING]
>  Die SAS-Schlüssel-Wert beginnt mit einem "?" (Fragezeichen). Wenn Sie den SAS-Schlüssel verwenden, müssen Sie das führende entfernen "?". Andernfalls können Ihren Aufwand blockiert werden.    
  
## <a name="remarks"></a>Hinweise  
 Wenn eine datenbankweite Anmeldeinformationen geändert werden, die Werte der beiden *Identity_name* und *geheimen* werden zurückgesetzt. Falls das optionale SECRET-Argument nicht angegeben wird, wird der Wert des gespeicherten Kennworts auf NULL festgelegt.  
  
 Das Kennwort wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel erneut generiert wird, wird das Kennwort erneut mithilfe des neuen Diensthauptschlüssels verschlüsselt.  
  
 Informationen zu datenbankbezogenen Anmeldeinformationen werden in der [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert `ALTER` -Berechtigung für die Anmeldeinformationen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. Ändern des Kennworts für eine Datenbank im Bereich einer Anmeldeinformationen  
 Im folgenden Beispiel wird den geheime Schlüssel in eine datenbankweite Anmeldeinformationen namens gespeicherten `Saddles`. Die datenbankbezogenen Anmeldeinformationen enthält, die Windows-Anmeldung `RettigB` und das zugehörige Kennwort. Das neue Kennwort wird die datenbankbezogenen Anmeldeinformationen mithilfe der SECRET-Klausel hinzugefügt.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Entfernen des Kennworts aus Anmeldeinformationen  
 Im folgenden Beispiel wird das Kennwort von datenbankweit gültigen Anmeldeinformationen mit dem Namen `Frames`. Die datenbankbezogenen Anmeldeinformationen enthält Windows-Anmeldung `Aboulrus8` und ein Kennwort anzugeben. Nachdem die Anweisung ausgeführt wird, müssen die datenbankbezogenen Anmeldeinformationen ein NULL-Kennwort, da die Option SECRET nicht angegeben ist.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Erstellen Sie die Datenbank ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
