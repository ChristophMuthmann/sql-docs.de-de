---
title: ALTER CREDENTIAL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f939a257a427007e4b0a101a933aafbff9e50546
ms.sourcegitcommit: 3ed9be04cc7fb9ab1a9ec230c298ad2932acc71b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/17/2018
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Ändert die Eigenschaften von Anmeldeinformationen.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Gibt den Namen der Anmeldeinformationen an, die geändert werden.  
  
 IDENTITY **='***identity_name***'**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird.  
  
 SECRET **='***secret***'**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist. *secret* ist optional.  
  
## <a name="remarks"></a>Remarks  
 Wenn Anmeldeinformationen geändert werden, werden die Werte von *identity_name* und *secret* zurückgesetzt. Falls das optionale SECRET-Argument nicht angegeben wird, wird der Wert des gespeicherten Kennworts auf NULL festgelegt.  
  
 Das Kennwort wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel erneut generiert wird, wird das Kennwort erneut mithilfe des neuen Diensthauptschlüssels verschlüsselt.  
  
 Informationen zu Anmeldeinformationen werden in der **sys.credentials**-Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY CREDENTIAL-Berechtigung. Falls es sich bei dem Anmeldeinformationen um Systemanmeldeinformationen handelt, ist die CONTROL SERVER-Berechtigung erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. Ändern des Kennworts für Anmeldeinformationen  
 Im folgenden Beispiel wird das Kennwort, das in den Anmeldeinformationen namens `Saddles` gespeichert ist, geändert. Diese Anmeldeinformationen enthalten den Windows-Anmeldenamen `RettigB` und das zugehörige Kennwort. Das neue Kennwort wird den Anmeldeinformationen mithilfe der SECRET-Klausel hinzugefügt.  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Entfernen des Kennworts aus Anmeldeinformationen  
 Im folgenden Beispiel wird das Kennwort aus Anmeldeinformationen namens `Frames` entfernt. Diese Anmeldeinformationen enthalten den Windows-Anmeldenamen `Aboulrus8` und ein Kennwort. Nach der Ausführung der Anweisung weisen die Anmeldeinformationen ein NULL-Kennwort auf, weil die Option SECRET nicht angegeben ist.  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
