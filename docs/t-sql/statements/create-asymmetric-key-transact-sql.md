---
title: CREATE ASYMMETRIC KEY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 932f8139685c5af4bdf92288ff937529286a1549
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen asymmetrischen Schlüssel in der Datenbank.  
  
 Diese Funktion ist inkompatibel mit Datenbankexport über Data-Tier Application Framework (DACFx). Sie müssen alle asymmetrischen Schlüssel vor dem Export löschen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE ASYMMETRIC KEY Asym_Key_Name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <Asym_Key_Source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<Asym_Key_Source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY Assembly_Name  
   | PROVIDER Provider_Name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>Argumente  
 FROM *Asym_Key_Source*  
 Gibt die Quelle an, aus der das asymmetrische Schlüsselpaar geladen werden soll.  
  
 AUTHORIZATION *database_principal_name*  
 Gibt den Besitzer des asymmetrischen Schlüssels an. Eine Rolle oder Gruppe kann nicht als Besitzer angegeben sein. Wird diese Option ausgelassen, wird der aktuelle Benutzer als Besitzer verwendet.  
  
 FILE ='*path_to_strong-name_file*'  
 Gibt den Pfad zu einer Datei mit starkem Namen an, aus der das Schlüsselpaar geladen werden soll.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 EXECUTABLE FILE ='*path_to_executable_file*'  
 Gibt eine Assemblydatei an, aus der der öffentliche Schlüssel geladen werden soll. Beschränkt auf 260 Zeichen von MAX_PATH von der Windows-API.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 ASSEMBLY *Assembly_Name*  
 Gibt den Namen einer Assembly an, aus der der öffentliche Schlüssel geladen werden soll.  
  
ENCRYPTION BY *\<key_name_in_provider>* gibt an, wie der Schlüssel verschlüsselt wurde. Dabei kann es sich um ein Zertifikat, ein Kennwort oder einen asymmetrischen Schlüssel handeln.  
  
 KEY_NAME ='*key_name_in_provider*'  
 Gibt den Schlüsselnamen des externen Anbieters an. Weitere Informationen zum Verwalten externer Schlüssel finden Sie unter [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 CREATION_DISPOSITION = CREATE_NEW  
 Erstellt einen neuen Schlüssel auf dem Extensible Key Management-Gerät. PROV_KEY_NAME muss verwendet werden, um Schlüsselnamen auf dem Gerät anzugeben. Wenn bereits ein Schlüssel auf dem Gerät vorhanden ist, gibt die Anweisung eine Fehlermeldung zurück.  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 Ordnet einen asymmetrischen Schlüssel von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einem vorhandenen EKM-Schlüssel zu. PROV_KEY_NAME muss verwendet werden, um Schlüsselnamen auf dem Gerät anzugeben. Wenn CREATION_DISPOSITION = OPEN_EXISTING nicht bereitgestellt wird, ist der Standardwert CREATE_NEW.  
  
 ALGORITHM = \<algorithm>  
 Die folgenden fünf Algorithmen können zur Verfügung gestellt werden: RSA_4096, RSA_3072, RSA_2048, RSA_1024 und RSA_512.  
  
 RSA_1024 und RSA_512 sind veraltet. Um RSA_1024 oder RSA_512 zu verwenden (was nicht empfohlen wird), müssen Sie den Kompatibilitätsgrad zwischen Datenbanken auf höchstens 120 festlegen.  
  
 PASSWORD = '*password*'  
 Gibt das Kennwort an, mit dem der private Schlüssel verschlüsselt werden soll. Wenn diese Klausel nicht vorhanden ist, wird der private Schlüssel mit dem Datenbank-Hauptschlüssel verschlüsselt. *password* kann maximal 128 Zeichen umfassen. *password* muss den Anforderungen der Windows-Kennwortrichtlinien des Computers entsprechen, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
## <a name="remarks"></a>Remarks  
 Ein *asymmetrischer Schlüssel* ist eine sicherungsfähige Entität auf Datenbankebene. Standardmäßig enthält diese Entität sowohl einen öffentlichen als auch einen privaten Schlüssel. Bei einer Ausführung ohne die FROM-Klausel generiert CREATE ASYMMETRIC KEY ein neues Schlüsselpaar. Bei einer Ausführung mit FROM-Klausel importiert CREATE ASYMMETRIC KEY ein Schlüsselpaar aus einer Datei oder einen öffentlichen Schlüssel aus einer Assembly.  
  
 Standardmäßig ist der private Schlüssel mit dem Datenbank-Hauptschlüssel geschützt. Falls kein Datenbank-Hauptschlüssel erstellt wurde, ist ein Kennwort zum Schützen des privaten Schlüssels erforderlich. Falls ein Datenbank-Hauptschlüssel vorhanden ist, ist das Kennwort optional.  
  
 Der private Schlüssel kann eine Länge von 512, 1024 oder 2048 Bits aufweisen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE ASYMMETRIC KEY-Berechtigung in der Datenbank. Wenn die AUTHORIZATION-Klausel angegeben ist, ist die IMPERSONATE-Berechtigung für den Datenbankprinzipal oder die ALTER-Berechtigung für die Anwendungsrolle erforderlich. Nur Windows-Anmeldungen, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen und Anwendungsrollen können asymmetrische Schlüssel besitzen. Gruppen und Rollen können keine asymmetrischen Schlüssel besitzen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-an-asymmetric-key"></a>A. Erstellen eines asymmetrischen Schlüssels  
 Im folgenden Beispiel wird der asymmetrische Schlüssel `PacificSales09` mithilfe des `RSA_2048`-Algorithmus erstellt, und der private Schlüssel wird mit einem Kennwort geschützt.  
  
```  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>B. Erstellen eines asymmetrischen Schlüssels aus einer Datei, wobei die Autorisierung an einen Benutzer erteilt wird  
 Im folgenden Beispiel wird der asymmetrische Schlüssel `PacificSales19` aus einem in einer Datei gespeicherten Schlüsselpaar erstellt, und der Benutzer `Christina` wird anschließend zum Verwenden des asymmetrischen Schlüssels autorisiert.  
  
```  
CREATE ASYMMETRIC KEY PacificSales19 AUTHORIZATION Christina   
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp'    
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. Erstellen eines asymmetrischen Schlüssels von einem EKM-Anbieter  
 Im folgenden Beispiel wird der asymmetrische Schlüssel `EKM_askey1` aus einem in einer Datei gespeicherten Schlüsselpaar erstellt. Anschließend wird er unter Verwendung eines Extensible Key Management-Anbieters mit dem Namen `EKMProvider1` und einem Schlüssel mit dem Namen `key10_user1` bei dem Anbieter verschlüsselt.  
  
```  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
