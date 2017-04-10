---
title: "Umbenennen eines Computers, der eine eigenst&#228;ndige Instanz von SQL Server hostet | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Remoteanmeldungsfehler [SQL Server]"
  - "Namen eigenständiger Computer [SQL Server]"
  - "Umbenennen, eigenständige Instanzen von SQL Server"
  - "Umbenennen von eigenständigen Instanzen von SQL Server"
  - "sysservers-Systemtabelle"
  - "Entfernen von Remoteanmeldungen"
  - "Löschen von Remoteanmeldungen"
  - "Entfernen von Remoteanmeldungen"
ms.assetid: bbaf1445-b8a2-4ebf-babe-17d8cf20b037
caps.latest.revision: 31
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 31
---
# Umbenennen eines Computers, der eine eigenst&#228;ndige Instanz von SQL Server hostet
  Wenn Sie den Namen des Computers ändern, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird, wird der neue Name beim Starten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erkannt. Sie müssen das Setup nicht erneut ausführen, um den Computernamen zurückzusetzen. Führen Sie stattdessen die folgenden Schritte aus, um die Systemmetadaten zu aktualisieren, die in sys.servers gespeichert sind und von der Systemfunktion @@SERVERNAME gemeldet werden. Aktualisieren Sie die Systemmetadaten, um Änderungen des Computernamens für Remoteverbindungen und -anwendungen widerzuspiegeln, die @@SERVERNAME verwenden oder die den Servernamen von sys.servers abfragen.  
  
 Die folgenden Schritte können nicht verwendet werden, um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]umzubenennen. Die Schritte können nur verwendet werden, um den Teil des Instanznamens umzubenennen, der dem Computernamen entspricht. Sie können beispielsweise einen Computer mit dem Namen MB1 umbenennen (z. B. in MB2), der eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem Namen Instance1 hostet. Der Teil des Namens, der sich auf die Instanz bezieht, Instance1, bleibt jedoch unverändert. In diesem Beispiel wird \\\\*ComputerName*\\*InstanceName* von \\\MB1\Instance1 in \\\MB2\Instance1 geändert.  
  
 **Vorbereitungen**  
  
 Bevor Sie den Umbenennungsprozess beginnen, überprüfen Sie die folgenden Informationen:  
  
-   Wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Teil eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusters ist, unterscheidet sich der Umbenennungsvorgang des Computers von einem Computer, der eine eigenständige Instanz hostet.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nicht die Umbenennung von Computern, die an einer Replikation beteiligt sind. Eine Ausnahme stellt die Verwendung des Protokollversands mit Replikation dar. Der sekundäre Computer beim Protokollversand kann umbenannt werden, wenn eine Wiederherstellung des primären Computers nicht mehr möglich ist. Weitere Informationen finden Sie unter [Protokollversand und Replikation &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
-   Wenn Sie einen Computer umbenennen, der für die Verwendung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] konfiguriert wurde, kann es sein, dass [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nach der Namensänderung nicht mehr zur Verfügung steht. Weitere Informationen finden Sie unter [Umbenennen eines Berichtsservercomputers](../../reporting-services/report-server/rename-a-report-server-computer.md).  
  
-   Wenn Sie einen für die Verwendung der Datenbankspiegelung konfigurierten Computer umbenennen, müssen Sie die Datenbankspiegelung vor dem Umbenennungsvorgang deaktivieren. Aktivieren Sie Datenbankspiegelung dann mit dem neuen Computernamen erneut. Die Metadaten für die Datenbankspiegelung werden nicht automatisch aktualisiert, um den neuen Namen des Computers widerzuspiegeln. Führen Sie die folgenden Schritte aus, um die Systemmetadaten zu aktualisieren.  
  
-   Es kann sein, dass Benutzer, die über eine Windows-Gruppe mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind, in der ein hartcodierter Verweis auf den Computernamen verwendet wird, die Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht herstellen können. Dies kann nach der Umbenennung passieren, wenn die Windows-Gruppe den alten Computernamen angibt. Aktualisieren Sie die Windows-Gruppe für die Verwendung des neuen Computernamens, um sicherzustellen, dass solche Windows-Gruppen nach dem Umbenennungsvorgang für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden können.  
  
 Sie können mithilfe des neuen Computernamens eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen, nachdem Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu gestartet haben. Um sicherzustellen, dass @@SERVERNAME den aktualisierten Namen der lokalen Serverinstanz zurückgibt, führen Sie manuell eine der folgenden Prozeduren aus, die für Ihr Szenario zutrifft. Die verwendete Prozedur hängt davon ab, ob Sie einen Computer aktualisieren, der eine Standardinstanz oder eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hostet.  
  
### So benennen Sie einen Computer um, der eine eigenständige Instanz hostet von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Führen Sie für einen umbenannten Computer, der eine Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hostet, die folgenden Prozeduren aus:  
  
    ```  
    sp_dropserver <old_name>;  
    GO  
    sp_addserver <new_name>, local;  
    GO  
    ```  
  
     Starten Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu.  
  
-   Führen Sie für einen umbenannten Computer, der eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hostet, die folgenden Prozeduren aus:  
  
    ```  
    sp_dropserver <old_name\instancename>;  
    GO  
    sp_addserver <new_name\instancename>, local;  
    GO  
    ```  
  
     Starten Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu.  
  
## Nach dem Umbenennungsvorgang  
 Nachdem ein Computer umbenannt wurde, müssen alle Verbindungen, bei denen der alte Computername verwendet wurde, mithilfe des neuen Namens hergestellt werden.  
  
#### So überprüfen Sie, ob der Umbenennungsvorgang erfolgreich abgeschlossen wurde  
  
-   Wählen Sie entweder Informationen von @@SERVERNAME oder von sys.servers aus. Die @@SERVERNAME-Funktion gibt den neuen Namen zurück, und in der sys.servers-Tabelle wird der neue Name angezeigt. Das folgende Beispiel zeigt die Verwendung von @@SERVERNAME.  
  
    ```  
    SELECT @@SERVERNAME AS 'Server Name';  
    ```  
  
## Weitere Überlegungen  
 **Remoteanmeldungen**: Wenn der Computer über Remoteanmeldungen verfügt, wird beim Ausführen von **sp_dropserver** ggf. ein Fehler generiert, der dem Folgenden ähnelt:  
  
 `Server: Msg 15190, Level 16, State 1, Procedure sp_dropserver, Line 44 There are still remote logins for the server 'SERVER1'.`  
  
 Um den Fehler zu beheben, müssen Sie Remoteanmeldungen für diesen Server löschen.  
  
#### So löschen Sie Remoteanmeldungen  
  
-   Führen Sie für eine Standardinstanz die folgende Prozedur aus:  
  
    ```  
    sp_dropremotelogin old_name;  
    GO  
    ```  
  
-   Führen Sie für eine benannte Instanz die folgende Prozedur aus:  
  
    ```  
    sp_dropremotelogin old_name\instancename;  
    GO  
    ```  
  
 **Verbindungsserverkonfigurationen**: Das Umbenennen von Computern wirkt sich auf die Verbindungsserverkonfigurationen aus. Verwenden Sie **sp_addlinkedserver** oder **sp_setnetname**, um Verweise auf Computernamen zu aktualisieren. Weitere Informationen finden Sie unter [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) oder [sp_setnetname &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md).  
  
 **Clientaliasnamen**: Das Umbenennen von Computern wirkt sich auf Clientaliasnamen aus, die Named Pipes verwenden. Wenn z. B. ein Alias "PROD_SRVR" erstellt wurde, um auf SRVR1 zu verweisen, und dieser das Named Pipes-Protokoll verwendet, lautet der Pipe-Name `\\SRVR1\pipe\sql\query`. Nachdem der Computer umbenannt wurde, ist der Pfad der Named Pipe nicht mehr gültig. Weitere Informationen zu Named Pipes finden Sie unter [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von Named Pipes](http://go.microsoft.com/fwlink/?LinkId=111063).  
  
## Siehe auch  
 [Installieren von SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)  
  
  