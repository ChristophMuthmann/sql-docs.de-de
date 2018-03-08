---
title: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
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
- ALTER_CRYPTOGRAPHIC_PROVIDER_TSQL
- ALTER CRYPTOGRAPHIC PROVIDER
- ALTER_CRYPTOGRAPHIC_TSQL
- ALTER CRYPTOGRAPHIC
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER CRYPTOGRAPHIC PROVIDER
ms.assetid: 876b6348-fb29-49e1-befc-4217979f6416
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe377a27978cdae372a7bfc8545d7cad1f514820
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-cryptographic-provider-transact-sql"></a>ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert einen Kryptografieanbieter innerhalb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem Anbieter (Extensible Key Management, EKM).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  
## <a name="arguments"></a>Argumente  
 *provider_name*  
 Der Name des EKM-Anbieters.  
  
 *Path_of_DLL*  
 Pfad der DLL-Datei, die implementiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extensible Key Management-Schnittstelle.  
  
 ENABLE | DISABLE  
 Aktiviert bzw. deaktiviert einen Anbieter.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Anbieter die DLL-Datei ändert, mit der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die erweiterbare Schlüsselverwaltung implementiert wird, müssen Sie die ALTER CRYPTOGRAPHIC PROVIDER-Anweisung verwenden.  
  
 Wenn der Pfad der DLL-Datei mithilfe der ALTER CRYPTOGRAPHIC PROVIDER-Anweisung aktualisiert wird, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] folgende Aktionen aus:  
-   Deaktiviert den Anbieter.  
-   Überprüft die DLL-Signatur und stellt sicher, dass die DLL-Datei über den GUID verfügt, der auch im Katalog aufgezeichnet ist.  
-   Aktualisiert die DLL-Version im Katalog.  
  

Wenn ein EKM-Anbieter auf DISABLE festgelegt wird, tritt bei neuen Verbindungen bei dem Versuch, den Anbieter mit Verschlüsselungsanweisungen zu verwenden, ein Fehler auf.  
  
Um einen Anbieter zu deaktivieren, müssen alle Sitzungen, die den Anbieter verwenden, beendet werden.  
  
Wenn von einer DLL des EKM-Anbieters nicht alle erforderlichen Methoden implementiert werden, kann ALTER CRYPTOGRAPHIC PROVIDER den Fehler 33085 zurückgeben:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
Wenn die Headerdatei, mit der die DLL des EKM-Anbieters erstellt wurde, veraltet ist, kann ALTER CRYPTOGRAPHIC PROVIDER den Fehler 33032 zurückgeben:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den Kryptografieanbieter.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird einen Kryptografieanbieter mit aufgerufen `SecurityProvider` in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], auf eine neuere Version einer DLL-Datei. Diese neue Version erhält den Namen `c:\SecurityProvider\SecurityProvider_v2.dll` und wird auf dem Server installiert. Das Zertifikat des Anbieters muss auf dem Server installiert sein.  
  
1. Deaktivieren Sie den Anbieter aus, um das Upgrade ausführen. Dadurch werden alle geöffneten kryptografische Sitzungen beendet.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. Aktualisieren Sie die Anbieter-DLL-Datei. Die GUID muss identisch mit der vorherigen Version, aber die Version kann unterschiedlich sein.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. Aktivieren Sie den aktualisierten Anbieter.   
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
ENABLE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
