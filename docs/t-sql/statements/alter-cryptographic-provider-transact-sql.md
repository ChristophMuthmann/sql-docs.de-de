---
title: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft-Dokumentation
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

  Ändert einen Kryptografieanbieter innerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem EKM-Anbieter (Extensible Key Management) aus.  
  
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
 Der Pfad der DLL-Datei, die die EKM-Schnittstelle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementiert.  
  
 ENABLE | DISABLE  
 Aktiviert bzw. deaktiviert einen Anbieter.  
  
## <a name="remarks"></a>Remarks  
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
 Im folgenden Beispiel wird ein Kryptografieanbieter mit dem Namen `SecurityProvider` in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in eine neuere Version einer DLL-Datei geändert. Diese neue Version erhält den Namen `c:\SecurityProvider\SecurityProvider_v2.dll` und wird auf dem Server installiert. Das Zertifikat des Anbieters muss auf dem Server installiert sein.  
  
1. Deaktivieren Sie den Anbieter, um das Upgrade durchzuführen. Dadurch werden alle geöffneten kryptografischen Sitzungen beendet.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. Aktualisieren Sie die DLL-Datei des Anbieters. Die GUID muss mit der vorherigen Version identisch sein, die Version kann sich jedoch unterscheiden.  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
