---
title: Sp_addserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9c57567ccbf1ef47ca43797f83dbf55dcc9c070d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Definiert den Namen der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird umbenannt haben, verwenden Sie **Sp_addserver** informiert die Instanz von der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] den neuen Namen des Computers. Diese Prozedur muss in allen auf dem Computer gehosteten [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanzen ausgeführt werden. Der Instanzname des der [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann nicht geändert werden. Installieren Sie zum Ändern des Instanznamens für eine benannte Instanz eine neue Instanz mit dem gewünschten Namen, trennen Sie die Datenbankdateien aus der alten Instanz, fügen Sie der neuen Instanz die Datenbanken an, und löschen Sie die alte Instanz. Alternativ können Sie einen Aliasnamen für den Client auf dem Clientcomputer erstellen, um die Verbindung auf einen anderen Server- und Instanznamen oder die **Server: Port** -Kombination umzuleiten, ohne den Namen der Instanz auf dem Computer zu ändern.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@server =** ] **'***server***'**  
 Der Name des Servers. Servernamen müssen eindeutig sein und den Regeln für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Computernamen entsprechen; es sind jedoch keine Leerzeichen zulässig. *server* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 Wenn mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert werden auf einem Computer eine Instanz ausgeführt wird, als ob er sich auf einem separaten Server befindet. Geben Sie eine benannte Instanz an, indem Sie auf *server* als *servername\instancename*verweisen.  
  
 [ **@local =** ] **'LOCAL'**  
 Gibt an, dass der Server als lokaler Server hinzugefügt wird. **@local** ist **varchar(10)**, hat den Standardwert NULL. Angeben von **@local** als **lokale** definiert **@server** als den Namen des lokalen Servers und der Ursachen der @@SERVERNAME -Funktion den Wert zurückgibt der *Server*.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup legt diese Variable während der Installation auf den Computernamen fest. Standardmäßig der Name des Computers ist die Möglichkeit Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ohne zusätzliche Konfiguration.  
  
 Die lokale Definition wird erst nach dem Neustarten von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wirksam. In jeder Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann nur ein lokaler Server definiert werden.  
  
 [ **@duplicate_ok =** ] **'duplicate_OK'**  
 Gibt an, ob ein doppelter Servername zulässig ist. **@duplicate_OK** ist **varchar(13)**, hat den Standardwert NULL. **@duplicate_OK** Lassen Sie nur den Wert **Duplicate_OK** oder NULL. Wenn **duplicate_OK** angegeben wird und der hinzugefügte Servername bereits vorhanden ist, wird kein Fehler ausgelöst. Wenn keine benannten Parameter verwendet werden, **@local** muss angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie **sp_serveroption**, um Serveroptionen festzulegen oder zu löschen.  
  
 **sp_addserver** kann nicht innerhalb einer benutzerdefinierten Transaktion verwendet werden.  
  
 Die Verwendung von **sp_addserver** zum Hinzufügen eines Remoteservers wird eingestellt. Verwenden Sie stattdessen [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) .  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **setupadmin** .  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel ändert die [!INCLUDE[ssDE](../../includes/ssde-md.md)] Eintrag für den Namen des hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf `ACCOUNTS`.  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Umbenennen eines Computers, das eine eigenständige Instanz von SQLServer hostet](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [Sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Sicherheitsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
