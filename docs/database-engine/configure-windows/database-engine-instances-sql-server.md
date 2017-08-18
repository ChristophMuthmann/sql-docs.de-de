---
title: Datenbankmodulinstanzen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 629b0c63a6dfe888b64c665fe02de93134acb320
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="database-engine-instances-sql-server"></a>Datenbankmodulinstanzen (SQL Server)
  Eine Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)] s ist eine Kopie der ausführbaren Datei **sqlservr.exe** , die als Betriebssystemdienst ausgeführt wird. Von jeder Instanz werden mehrere Systemdatenbanken und eine oder mehrere Benutzerdatenbanken verwaltet. Auf einem Computer können mehrere Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]ausgeführt werden. Anwendungen stellen eine Verbindung mit der Instanz her, um Tasks in einer durch die Instanz verwalteten Datenbank auszuführen.  
  
## <a name="instances"></a>Instanzen  
 Eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wird als Dienst ausgeführt, der alle Anwendungsanforderungen für Daten in den Datenbanken behandelt, die von der betreffenden Instanz verwaltet werden. Es handelt sich um das Ziel der Verbindungsanforderungen (Anmeldungen) von Anwendungen. Wenn sich Anwendung und Instanz auf getrennten Computern befinden, wird die Verbindung über eine Netzwerkverbindung hergestellt. Wenn sich Anwendung und Instanz auf demselben Computer befinden, kann die SQL Server-Verbindung als Netzwerkverbindung oder als Verbindung im Arbeitsspeicher ausgeführt werden. Wenn eine Verbindung hergestellt wurde, sendet eine Anwendung über die Verbindung [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen an die Instanz. Die Instanz löst die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen in Vorgänge für die Daten und Objekte in den Datenbanken auf, und wenn den Anmeldeinformationen die erforderlichen Berechtigungen gewährt wurden, werden die Tasks ausgeführt. Alle abgerufenen Daten werden zusammen mit gegebenenfalls vorhandenen Meldungen, z. B. zu Fehlern, an die Anwendung zurückgegeben.  
  
 Sie können mehrere Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf demselben Computer ausführen. Bei einer Instanz kann es sich um die Standardinstanz handeln. Die Standardinstanz hat keinen Namen. Wenn eine Verbindungsanforderung nur den Namen des Computers angibt, wird die Verbindung mit der Standardinstanz hergestellt. Für benannte Instanzen geben Sie beim Installieren der Instanz jeweils einen Instanznamen an. Verbindungsanforderungen müssen sowohl den Computernamen als auch den Instanznamen angeben, damit eine Verbindung mit der Instanz hergestellt werden kann. Die Installation einer Standardinstanz ist nicht obligatorisch. Alle Instanzen, die auf einem Computer ausgeführt werden, können benannte Instanzen sein.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie die Eigenschaften einer Instanz konfiguriert werden. Konfigurieren Sie Standardeinstellungen wie Speicherorte und Datumsformate und die Verwendung der Betriebssystemressourcen durch die Instanz, z. B. des Arbeitsspeichers oder von Threads.|[Konfigurieren von Datenbankmodulinstanzen &#40;SQL Server&#41;](../../database-engine/configure-windows/configure-database-engine-instances-sql-server.md)|  
|Beschreibt, wie die Sortierung für eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]verwaltet wird. Sortierungen definieren die Bitmuster, die zum Darstellen von Zeichen und zugeordneten Verhaltensweisen wie der Sortierung und Groß-/Kleinschreibung und Akzenten in Vergleichsvorgängen verwendet werden.|[Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)|  
|Beschreibt, wie Verbindungsserverdefinitionen konfiguriert werden, die in einer Instanz ausgeführte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen zulassen, um in getrennten OLE DB-Datenquellen gespeicherte Daten zu verwenden.|[Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|Beschreibt, wie ein LOGON-Trigger erstellt wird, der auszuführende Aktionen angibt, die nach der Überprüfung des Anmeldeversuchs, aber vor dem Beginn der Verwendung von Ressourcen in der Instanz ausgeführt werden sollen. LOGON-Trigger unterstützen Aktionen wie die Protokollierung der Verbindungsaktivität die logikbasierte Einschränkung von Anmeldungen, die zusätzlich zur Authentifizierung der Anmeldeinformationen durch Windows und SQL Server verwendet wird.|[Logon-Trigger](../../relational-databases/triggers/logon-triggers.md)|  
|Beschreibt, wie der einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]zugeordnete Dienst verwaltet wird. Dazu zählen Aktionen wie das Starten und Beenden des Diensts und das Konfigurieren von Startoptionen.|[Verwalten der Datenbankmoduldienste](../../database-engine/configure-windows/manage-the-database-engine-services.md)|  
|Beschreibt, wie Servernetzwerk-Konfigurationstasks ausgeführt werden müssen, z. B. das Aktivieren von Protokollen, das Ändern eines von einem Protokoll verwendeten Ports oder einer Pipe, das Konfigurieren von Verschlüsselungen, das Konfigurieren des SQL Server-Browserdiensts, das Anzeigen oder das Ausblenden vom SQL Server-Datenbankmodul im Netzwerk und das Registrieren des Serverprinzipalnamens.|[Server-Netzwerkkonfiguration](../../database-engine/configure-windows/server-network-configuration.md)|  
|Beschreibt, wie Clientnetzwerk-Konfigurationstasks (beispielsweise das Konfigurieren von Clientprotokollen und das Erstellen oder Löschen eines Serveralias) ausgeführt werden.|[Client-Netzwerkkonfiguration](../../database-engine/configure-windows/client-network-configuration.md)|  
|Beschreibt die [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Editoren, die zum Entwerfen, Debuggen und Ausführen von Skripts, z. B. [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts, verwendet werden können. Beschreibt darüber hinaus, wie Windows PowerShell-Skripts für die Verwendung mit SQL Server-Komponenten codiert werden.|[Datenbankmodul-Skripterstellung](../../relational-databases/scripting/database-engine-scripting.md)|  
|Beschreibt, wie Wartungspläne verwendet werden, um für eine Instanz einen Workflow für allgemeine Verwaltungsaufgaben anzugeben. Workflows schließen Tasks wie das Sichern von Datenbanken und das Aktualisieren von Statistiken zur Leistungsverbesserung ein.|[Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|Beschreibt, wie die Ressourcenkontrolle zum Verwalten von Ressourcenverbrauch und Arbeitslasten verwendet wird, indem Beschränkungen für die CPU- und Arbeitsspeicherressourcen angegeben werden, die von Anwendungsanforderungen verwendet werden können.|[Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)|  
|Beschreibt, wie Datenbankanwendungen Datenbank-E-Mails verwenden können, um E-Mail-Nachrichten von [!INCLUDE[ssDE](../../includes/ssde-md.md)]aus zu senden.|[Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)|  
|Beschreibt, wie erweiterte Ereignisse verwendet werden, um Leistungsdaten für die Erstellung von Leistungsbaselines oder die Diagnostizierung von Leistungsproblemen aufzuzeichnen. Erweiterte Ereignisse sind hoch skalierbares System mit geringem Ressourcenverbrauch zum Erfassen von Leistungsdaten.|[Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)|  
|Beschreibt, wie die SQL-Ablaufverfolgung zum Erstellen eines benutzerdefinierten Systems zum Erfassen und Aufzeichnen von Ereignissen in [!INCLUDE[ssDE](../../includes/ssde-md.md)]verwendet wird.|[SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)|  
|Beschreibt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Profiler zum Erfassen von Ablaufverfolgungen für Anwendungsanforderungen verwendet wird, die bei einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]eingehen. Diese Ablaufverfolgungen können später für Aktivitäten wie Leistungstests oder die Problemdiagnose wiedergegeben werden.|[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|Beschreibt die Funktionen Change Data Capture (CDC) und Änderungsnachverfolgung und beschreibt, wie mit diesen Änderungen von Daten in einer Datenbank nachverfolgt werden können.|[Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|Beschreibt, wie der Protokolldatei-Viewer zum Suchen und Anzeigen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlern und -Meldungen in verschiedenen Protokollen verwendet wird, z. B. dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Auftragsverlauf, den SQL Server-Protokollen oder Windows-Ereignisprotokollen.|[Protokolldatei-Viewer](../../relational-databases/logs/log-file-viewer.md)|  
|Beschreibt, wie der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber zum Analysieren von Datenbanken und für Empfehlungen zur Behandlung von potenziellen Leistungsproblemen verwendet wird.|[Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|Beschreibt, wie die Produktionsdatenbankadministratoren eine Diagnoseverbindung mit Instanzen herstellen können, wenn Standardverbindungen nicht akzeptiert werden.|[Diagnoseverbindung für Datenbankadministratoren](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)|  
|Beschreibt, wie die veraltete Remoteserver-Funktion verwendet wird, um den Zugriff von einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf eine andere zu aktivieren. Der bevorzugte Mechanismus für diese Funktionalität ist ein Verbindungsserver.|[Remoteserver](../../database-engine/configure-windows/remote-servers.md)|  
|Beschreibt die Funktionen von Service Broker für Messaging- und Warteschlangenanwendungen und enthält Zeiger auf die Service Broker-Dokumentation.|[Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)|  
|Beschreibt, wie die Pufferpoolerweiterung verwendet werden kann, um eine nahtlose Integration von nicht flüchtigen Erweiterungen des Arbeitsspeichers, d. h. von Festkörperlaufwerken (SSD), in den Pufferpool des Datenbankmoduls bereitzustellen, durch die der E/A-Durchsatz deutlich verbessert wird.|[Pufferpool-Erweiterungsdatei](../../database-engine/configure-windows/buffer-pool-extension.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [sqlservr (Anwendung)](../../tools/sqlservr-application.md)   
 [Datenbankfunktionen](../../relational-databases/database-features.md)   
 [Instanzübergreifende Datenbankmodulfunktionen](../../relational-databases/database-engine-cross-instance-features.md)  
  
  
