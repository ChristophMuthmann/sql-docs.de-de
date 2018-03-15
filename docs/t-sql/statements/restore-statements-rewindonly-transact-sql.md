---
title: RESTORE REWINDONLY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/10/2017
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
- RESTORE_REWINDONLY_TSQL
- RESTORE REWINDONLY
dev_langs:
- TSQL
helpviewer_keywords:
- closing backup devices
- backup devices [SQL Server], rewinding
- media [SQL Server]
- open back devices
- rewinding backup devices
- RESTORE REWINDONLY statement
ms.assetid: 7f825b40-2264-4608-9809-590d0f09d882
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf67d54e58f08296878c0781158e7b878b0b2a49
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---rewindonly-transact-sql"></a>RESTORE-Anweisungen - REWINDONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt das Zurückspulen und Schließen der angegebenen Bandmedien aus, die durch mit der Option NOREWIND ausgeführte BACKUP- oder RESTORE-Anweisungen offen geblieben sind. Diese Option wird nur für Bandmedien verwendet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RESTORE REWINDONLY   
FROM <backup_device> [ ,...n ]  
[ WITH {UNLOAD | NOUNLOAD}]  
}   
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | TAPE = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}   
```  
  
## <a name="arguments"></a>Argumente  
 **\<backup_device> ::=** 
  
 Gibt das logische oder physische Sicherungsmedium an, das für den Wiederherstellungsvorgang verwendet wird.  
  
 { *logical_backup_device_name* | **@***logical_backup_device_name_var* } Dies ist der logische Name der von **sp_addumpdevice** erstellten Sicherungsmedien, von denen die Datenbank wiederhergestellt wird. Der Name muss den Regeln für Bezeichner entsprechen. Bei der Angabe als Variable (**@***logical_backup_device_name_var*) kann der Name des Sicherungsmediums entweder als Zeichenfolgenkonstante (**@***logical_backup_device_name_var* = *logical_backup_device_name*) oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der Datentypen **ntext** oder **text**) angegeben werden.  
  
 {DISK | TAPE } **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* } Ermöglicht die Wiederherstellung von Sicherungen vom angegebenen Datenträger oder vom Bandmedium. Die Gerätetypen von Datenträgern und Bändern müssen durch die tatsächlichen Namen des Geräts angegeben werden (z.B. vollständiger Pfad und Dateiname): DISK = 'C:\Programme\Microsoft SQL Server\MSSQL\BACKUP\Mybackup.bak' oder TAPE = '\\\\.\TAPE0'. Bei der Angabe als Variable (**@***physical_backup_device_name_var*) kann der Name des Geräts entweder als Zeichenfolgenkonstante (**@***physical_backup_device_name_var* = '*physcial_backup_device_name*') oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der Datentypen **ntext** oder **text**) angegeben werden.  
  
 Wenn Sie einen Netzwerkserver mit einem UNC-Namen (der einen Computernamen enthalten muss) verwenden, geben Sie die Geräteart Datenträger (DISK) an. Weitere Informationen zum Verwenden von UNC-Namen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 Das Konto, unter dem Sie Microsoft SQL Server ausführen, muss Lesezugriff auf den Remotecomputer oder Netzwerkserver besitzen, damit ein RESTORE-Vorgang ausgeführt werden kann.  
  
 *n*  
 Dies ist ein Platzhalter, der anzeigt, dass mehrere Sicherungsmedien und logische Sicherungsmedien angegeben werden können. Die maximale Anzahl von Sicherungsmedien oder logischen Sicherungsmedien beträgt **64**.  
  
 Ob für eine Wiederherstellungssequenz so viele Sicherungsmedien erforderlich sind, wie beim Erstellen des Mediensatzes verwendet wurden, zu dem die Sicherungen gehören, hängt davon ab, ob die Wiederherstellung offline oder online erfolgt. Bei der Offlinewiederherstellung kann eine Sicherung mit weniger Medien wiederhergestellt werden, als zum Erstellen der Sicherung erforderlich waren. Für eine Onlinewiederherstellung sind alle Sicherungsmedien der Sicherung erforderlich. Einer Wiederherstellungsversuch mit weniger Medien erzeugt einen Fehler.  
  
 Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)aufgezeichnet wurde.  
  
> [!NOTE]  
>  Bei der Wiederherstellung einer Sicherung aus einem gespiegelten Mediensatz können Sie für jede Medienfamilie jeweils nur einen einzigen Spiegel angeben. Wenn Fehler auftreten, können jedoch mithilfe des oder der anderen Spiegel einige Wiederherstellungsprobleme schnell gelöst werden. Sie können ein beschädigtes Medienvolume durch das entsprechende Volume eines anderen Spiegels ersetzen. Beachten Sie, dass Sie bei einer Offlinewiederherstellung von weniger Medien als Medienfamilien wiederherstellen können, aber jede Familie wird nur einmal verarbeitet.  
  
 **WITH Options**  
  
 UNLOAD  
 Gibt an, dass das Band automatisch zurückgespult und ausgeworfen wird, wenn der RESTORE-Vorgang vollständig ausgeführt ist. UNLOAD wird standardmäßig festgelegt, wenn eine neue Benutzersitzung gestartet wird. Diese Option bleibt festgelegt, bis NOUNLOAD angegeben wird. Diese Option wird nur für Bandmedien verwendet. Die Option wird ignoriert, wenn ein anderes Medium als ein Bandlaufwerk für RESTORE verwendet wird.  
  
 NOUNLOAD  
 Gibt an, dass das Band nach einem RESTORE-Vorgang nicht automatisch aus dem Bandlaufwerk ausgeworfen wird. NOUNLOAD bleibt festgelegt, bis UNLOAD angegeben wird.  
  
 Gibt an, dass das Band nach einem RESTORE-Vorgang nicht automatisch aus dem Bandlaufwerk ausgeworfen wird. NOUNLOAD bleibt festgelegt, bis UNLOAD angegeben wird.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 RESTORE REWINDONLY ist eine Alternative zu RESTORE LABELONLY FROM TAPE = \<Name> WITH REWIND. Die dynamische Verwaltungssicht [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) stellt eine Liste offener Bandlaufwerke bereit.  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer kann RESTORE REWINDONLY verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

