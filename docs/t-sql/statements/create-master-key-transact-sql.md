---
title: Erstellen Sie MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
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
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaec4d28dc95d792faa6406ef68df50167d0f091
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt einen Datenbank-Hauptschlüssel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password'  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE MASTER KEY [ ENCRYPTION BY PASSWORD ='password' ]
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 Kennwort = "*Kennwort*"  
 Das zum Verschlüsseln des Datenbank-Hauptschlüssels verwendete Kennwort. *Kennwort* erfüllt die Anforderungen der Windows-Kennwortrichtlinien des Computers, der die Instanz ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Kennwort* ist optional, [!INCLUDE[ssSDS](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
## <a name="remarks"></a>Hinweise  
 Der Datenbank-Hauptschlüssel ist ein symmetrischer Schlüssel, der zum Schützen von privaten Schlüsseln der in der Datenbank vorhandenen Zertifikate und asymmetrischen Schlüssel verwendet wird. Beim Erstellen wird der Hauptschlüssel mithilfe des AES_256-Algorithmus und eines vom Benutzer angegebenen Kennworts verschlüsselt. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]wird der Triple DES-Algorithmus verwendet. Die automatische Entschlüsselung für den Hauptschlüssel kann aktiviert werden, indem eine Kopie des Schlüssels mit dem Diensthauptschlüssel verschlüsselt und sowohl in der Datenbank als auch in master gespeichert wird. In der Regel wird die in master gespeicherte Kopie im Hintergrund aktualisiert, sobald der Hauptschlüssel geändert wird. Diese Standardeinstellung kann geändert werden, mithilfe der DROP ENCRYPTION BY SERVICE MASTER KEY-Option von [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md). Ein Hauptschlüssel, der nicht mit dem Diensthauptschlüssel verschlüsselt ist muss geöffnet werden, mithilfe der [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) -Anweisung und eines Kennworts.  
  
 In der is_master_key_encrypted_by_server-Spalte der sys.databases-Katalogsicht in master wird angezeigt, ob der Datenbank-Hauptschlüssel mit dem Diensthauptschlüssel verschlüsselt ist.  
  
 Informationen zum Datenbank-Hauptschlüssel werden in der sys.symmetric_keys-Katalogsicht angezeigt.  

Für SQL Server und Parallel Data Warehouse wird der Hauptschlüssel in der Regel durch den Diensthauptschlüssel und mindestens ein Kennwort geschützt. Bei der Datenbank auf einen anderen Server (Log shipping, Wiederherstellung, Sicherung usw.) physisch versetzt enthält die Datenbank eine Kopie des Hauptschlüssels mit dem ursprünglichen Server mit dem Diensthauptschlüssel verschlüsselt wird, (es sei denn, diese Verschlüsselung mit explizit entfernt wurde ALTER MASTER KEY DDL), und eine Kopie des Zertifikats jedes Verschlüsselungskennwort angegeben werden, während CREATE MASTER KEY oder nachfolgende ALTER MASTER KEY-DDL-Vorgänge. Zum Wiederherstellen der Master-Schlüssel und alle Daten verschlüsselt, mit dem Hauptschlüssel als Stamm in die Schlüsselhierarchie, nachdem die Datenbank verschoben wurde, wird der Benutzer entweder mit OPEN MASTER KEY-Anweisung mit einem Kennwort verwendet, um die Hauptschlüssel geschützt haben. , Wiederherstellen einer Sicherung des Hauptschlüssels aus, oder stellen Sie eine Sicherung der ursprünglichen Service Master Key, auf dem neuen Server wieder her. 

Für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], den Kennwortschutz wird nicht als ein Sicherheitsmechanismus, um einem Datenverlust in Situationen, in denen möglicherweise die Datenbank von einem Server, in eine andere verschoben werden, zu verhindern, wie der Diensthauptschlüssel Schutz auf den Hauptschlüssel wird verwaltet von Microsoft Azure-Plattform. Deshalb ist das Kennwort für den Schlüssel Maser optional in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].
  
> [!IMPORTANT]  
>  Sichern Sie den Hauptschlüssel mithilfe von [BACKUP MASTER KEY](../../t-sql/statements/backup-master-key-transact-sql.md) und die Sicherungskopie an einem sicheren Ort außerhalb Ihrer Geschäftsräume aufbewahren.  
  
 Der Diensthauptschlüssel und die Datenbank-Hauptschlüssel werden mit dem AES-256-Algorithmus geschützt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt einen Datenbank-Hauptschlüssel für die aktuelle Datenbank. Der Schlüssel wird mit dem Kennwort `23987hxJ#KL95234nl0zBe` verschlüsselt.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>Siehe auch  
 [Sys. symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Öffnen Sie MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


