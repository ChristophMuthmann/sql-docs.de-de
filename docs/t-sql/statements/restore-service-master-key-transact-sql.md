---
title: RESTORE SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f88ab43c6e452bbbb3b6cfa32e858ee1f091e366
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Importiert einen Diensthauptschlüssel aus einer Sicherungsdatei.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
## <a name="arguments"></a>Argumente  
 Datei **= "***Dateipfad***"**  
 Gibt den vollständigen Pfad, einschließlich des Dateinamens, zum gespeicherten Diensthauptschlüssel an. *Dateipfad* kann ein lokaler Pfad oder einen UNC-Pfad zu einem Netzwerkspeicherort sein.  
  
 Kennwort **= "***Kennwort***"**  
 Gibt das Kennwort an, das zum Entschlüsseln des aus einer Datei importierten Diensthauptschlüssels erforderlich ist.  
  
 FORCE  
 Erzwingt die Ersetzung des Diensthauptschlüssels, auch wenn Daten bei diesem Vorgang verloren gehen können.  
  
## <a name="remarks"></a>Hinweise  
 Bei der Wiederherstellung des Diensthauptschlüssels werden alle Schlüssel und geheimen Bereiche von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entschlüsselt, die mit dem aktuellen Diensthauptschlüssel verschlüsselt wurden. Diese Schlüssel werden dann mit dem aus der Sicherungsdatei geladenen Diensthauptschlüssel verschlüsselt.  
  
 Falls einer dieser Entschlüsselungsvorgänge nicht erfolgreich ausgeführt werden kann, tritt bei der Wiederherstellung ein Fehler auf. Sie können die FORCE-Option verwenden, um Fehler zu ignorieren, dies kann jedoch zum Verlust von Daten führen, die nicht entschlüsselt werden können.  
  
> [!CAUTION]  
>  Der Diensthauptschlüssel ist der Stamm der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verschlüsselungshierarchie. Mit dem Diensthauptschlüssel werden alle Schlüssel in der Struktur direkt oder indirekt geschützt. Wenn ein abhängiger Schlüssel während der erzwungenen Wiederherstellung nicht entschlüsselt werden kann, gehen die durch diesen Schlüssel geschützten Daten verloren.  
  
 Das Neugenerieren der Verschlüsselungshierarchie ist ein ressourcenintensiver Vorgang. Die Ausführung dieses Vorgangs sollte außerhalb der Hauptzeiten geplant werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Diensthauptschlüssel aus einer Sicherungsdatei wiederhergestellt.  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Diensthauptschlüssel](../../relational-databases/security/encryption/service-master-key.md)   
 [ALTER SERVICE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
