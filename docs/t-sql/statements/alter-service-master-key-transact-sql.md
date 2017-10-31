---
title: ALTER SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVICE_MASTER_KEY_TSQL
- ALTER SERVICE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- FORCE option
- ALTER SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- modifying Service Master Key
- decryption [SQL Server], Service Master Key
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], modifying
ms.assetid: a1e9be0e-4115-47d8-9d3a-3316d876a35e
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ee9fd8a888ed796b4d01b007aec5f8217cce5d9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-service-master-key-transact-sql"></a>ALTER SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den Diensthauptschlüssel einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER SERVICE MASTER KEY   
    [ { <regenerate_option> | <recover_option> } ] [;]  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE  
  
<recover_option> ::=  
    { WITH OLD_ACCOUNT = 'account_name' , OLD_PASSWORD = 'password' }  
    |      
    { WITH NEW_ACCOUNT = 'account_name' , NEW_PASSWORD = 'password' }  
```  
  
## <a name="arguments"></a>Argumente  
 FORCE  
 Gibt an, dass der Diensthauptschlüssel neu generiert werden soll, auch wenn Daten bei diesem Vorgang verloren gehen können. Weitere Informationen finden Sie unter [Ändern des SQL Server-Dienstkontos](#_changing) weiter unten in diesem Thema.  
  
 REGENERATE  
 Gibt an, dass der Diensthauptschlüssel neu generiert werden soll.  
  
 OLD_ACCOUNT **= "***Account_name***"**  
 Gibt den Namen des alten Windows-Dienstkontos an.  
  
> [!WARNING]  
>  Diese Option ist veraltet. Darf nicht verwendet werden. Verwenden Sie stattdessen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager.  
  
 OLD_PASSWORD **= "***Kennwort***"**  
 Gibt das Kennwort des alten Windows-Dienstkontos an.  
  
> [!WARNING]  
>  Diese Option ist veraltet. Darf nicht verwendet werden. Verwenden Sie stattdessen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager.  
  
 NEW_ACCOUNT **= "***Account_name***"**  
 Gibt den Namen des neuen Windows-Dienstkontos an.  
  
> [!WARNING]  
>  Diese Option ist veraltet. Darf nicht verwendet werden. Verwenden Sie stattdessen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager.  
  
 Neues_Kennwort **= "***Kennwort***"**  
 Gibt das Kennwort des neuen Windows-Dienstkontos an.  
  
> [!WARNING]  
>  Diese Option ist veraltet. Darf nicht verwendet werden. Verwenden Sie stattdessen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager.  
  
## <a name="remarks"></a>Hinweise  
 Der Diensthauptschlüssel wird automatisch generiert, wenn er zum ersten Mal benötigt wird, um ein Kennwort für einen Verbindungsserver, Anmeldeinformationen oder den Datenbank-Hauptschlüssel zu verschlüsseln. Der Diensthauptschlüssel wird mithilfe des auf dem lokalen Computer verwendeten Computerschlüssels oder der Windows-Datenschutz-API (DPAPI) verschlüsselt. Diese API verwendet einen Schlüssel, der von den Windows-Anmeldeinformationen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkontos abgeleitet wird.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQL Server 2016 schützt den Diensthauptschlüssel (Service Master Key, SMK) und den Datenbank-Hauptschlüssel (Database Master Key, DMK) mithilfe des AES-Verschlüsselungsalgorithmus. AES ist ein neuerer Verschlüsselungsalgorithmus als der in früheren Versionen verwendete 3DES-Algorithmus. Nach dem Aktualisieren einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] sollten SMK und DMK erneut generiert werden, um die Hauptschlüssel auf AES zu aktualisieren. Weitere Informationen zum Neugenerieren des DMK finden Sie unter [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md).  
  
##  <a name="_changing"></a>Ändern des SQL Server-Dienstkontos  
 Verwenden Sie zur Änderung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkontos den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager. Um eine Änderung des Dienstkontos zu verwalten, speichert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine redundante Kopie des Diensthauptschlüssels, die von dem Computerkonto geschützt wird, das die notwendigen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstgruppe gewährten Berechtigungen hat. Wenn der Computer neu eingerichtet wird, kann der gleiche Domänenbenutzer, der zuvor vom Dienstkonto verwendet wurde, den Diensthauptschlüssel wiederherstellen. Dies funktioniert nicht mit lokalen Konten oder die Konten Lokales System, lokaler Dienst oder Netzwerkdienst. Wenn Sie gleitenden sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einen anderen Computer migrieren Sie den Diensthauptschlüssel mit Sicherung und Wiederherstellung.  
  
 Mit REGENERATE wird der Diensthauptschlüssel neu generiert. Nach der Neugenerierung des Diensthauptschlüssels werden alle Schlüssel, die mit diesem Schlüssel verschlüsselt wurden, von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entschlüsselt und mit dem neuen Diensthauptschlüssel verschlüsselt. Dies ein ressourcenintensiver Vorgang. Die Ausführung dieses Vorgangs sollte außerhalb der Hauptzeiten geplant werden, es sei denn, der Schlüssel ist nicht mehr sicher. Falls einer dieser Entschlüsselungsvorgänge nicht erfolgreich beendet wird, wird für die gesamte Anweisung ein Fehler zurückgegeben.  
  
 Mit der FORCE-Option wird der Vorgang der Schlüsselneugenerierung fortgesetzt, auch wenn der aktuelle Hauptschlüssel nicht abgerufen werden kann oder wenn nicht alle privaten Schlüssel entschlüsselt werden können, die mit ihm verschlüsselt wurden. Verwenden Sie FORCE nur, wenn Regenerierung fehlschlägt und Sie können nicht mit dem Diensthauptschlüssel wiederherstellen, indem Sie mit der [RESTORE SERVICE MASTER KEY](../../t-sql/statements/restore-service-master-key-transact-sql.md) Anweisung.  
  
> [!CAUTION]  
>  Der Diensthauptschlüssel ist der Stamm der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verschlüsselungshierarchie. Mit dem Diensthauptschlüssel werden alle Schlüssel und geheimen Bereiche in der Struktur direkt oder indirekt geschützt. Wenn ein abhängiger Schlüssel während der erzwungenen Neugenerierung nicht entschlüsselt werden kann, gehen die durch den Schlüssel geschützten Daten verloren.  
  
 Wenn Sie SQL auf einen anderen Computer verschieben, müssen Sie dasselbe Dienstkonto zur SMK-Entschlüsselung verwenden. Das Computerkonto wird von SQL Server automatisch verschlüsselt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Diensthauptschlüssel neu generiert.  
  
```  
ALTER SERVICE MASTER KEY REGENERATE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [RESTORE SERVICE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

