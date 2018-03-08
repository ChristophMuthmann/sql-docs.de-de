---
title: "SQL-Tools und Hilfsprogramme für SQLServer, Azure SQL-Datenbank und Azure SQL Datawarehouse | Microsoft Docs"
ms.custom: 
ms.date: 02/22/2018
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9d45d1a682689fdfb87f6693a95e10bad079fdc9
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/24/2018
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL-Tools und Hilfsprogramme für SQLServer, Azure SQL-Datenbank und SQL Azure Datawarehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Zum Verwalten (Abfrage, Monitor, usw.) der Datenbank, die Sie benötigen ein Tool. Es stehen mehrere Datenbanktools. Während die Datenbanken ausgeführt werden können, in der Cloud, die unter Windows oder auf [Linux](../linux/sql-server-linux-overview.md), muss das Tool nicht für dieselbe Plattform wie die Datenbank ausführen. 

Dieser Artikel enthält Informationen zu den verfügbaren Tools zum Arbeiten mit SQL-Datenbanken. 


## <a name="tools-to-run-queries-and-manage-databases"></a>Tools zum Ausführen von Abfragen und Verwalten von Datenbanken  

| Tool | Description |
|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] ist eine kostenlose, leicht-Tool zum Verwalten von Datenbanken, wo sie ausgeführt werden. Diese Preview-Version stellt die Datenbank-Verwaltungsfunktionen, z. B. eine erweiterte Transact-SQL-Editor und anpassbare Einblicke in den Betriebsstatus Ihrer Datenbanken bereit. **[!INCLUDE[name-sos](../includes/name-sos-short.md)] unter Windows, Mac OS und Linux ausgeführt wird**.|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | Verwenden Sie SQL Server Management Studio (SSMS), um Abfragen, Entwerfen und Verwalten Ihrer SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse. **SSMS unter Windows ausgeführt wird**.|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | Umwandeln von Visual Studio in einer leistungsstarken Entwicklungsumgebung für SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse. **SSDT unter Windows ausgeführt wird**.|
|[mssql-cli](mssql-cli.md)|MSSQL-Cli-ist ein interaktives Befehlszeilen-Tool zum Abfragen von SQL Server. **MSSQL-Cli unter Windows, Mac OS und Linux ausgeführt wird**|
| [Visual Studio-Code](https://code.visualstudio.com/)| Installieren Sie nach der Installation von Visual Studio-Code, der [Mssql-Erweiterung](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) zum Entwickeln von Microsoft SQL Server, Azure SQL-Datenbank und SQL Data Warehouse. **Visual Studio-Code ausgeführt wird, unter Windows, Mac OS und Linux**.|

## <a name="which-tool-should-i-choose"></a>Welches Tool muss werden ausgewählt?

- Möchten Sie eine SQL Server-Instanz oder Datenbank in einer Lightweight-Editor unter Windows, Linux oder Mac verwalten? Wählen Sie [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- Möchten Sie eine SQL Server-Instanz oder Datenbank auf Windows mit vollständiger GUI-Unterstützung verwalten? Wählen Sie [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- Führen Sie zum Erstellen oder Verwalten von Datenbankcode, einschließlich der Kompilierung bei der Überprüfung werden sollen, Umgestaltung und Designer-Unterstützung unter Windows? Choose [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- Möchten Sie den SQL Server mit einem Befehlszeilentool Abfragen, die Syntax hoch-Beleuchtung, IntelliSense-Funktionen und vieles mehr? Wählen Sie [Mssql-Cli](mssql-cli.md)
- Möchten Sie die T-SQL-Skripts in einer Lightweight-Editor unter Windows, Linux oder Mac schreiben? Wählen Sie [Visual Studio Code](https://code.visualstudio.com/) und [Mssql-Erweiterung](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="additional-tools"></a>Zusätzliche tools

| Tool | Description |
|:--|:--|
| [Configuration Manager](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Verwenden Sie SQL Server Configuration Manager, zum Konfigurieren von SQL Server-Dienste und Netzwerkkonnektivität. Konfigurations-Manager unter Windows ausgeführt wird.|
|[mssql-conf](../linux/sql-server-linux-configure-mssql-conf.md)|Verwenden Sie Mssql-Conf so konfigurieren Sie SQL Server auf dem Linux ausgeführt wird.|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | Verwenden Sie SQL Server Migration Assistant zur Automatisierung der Datenbankmigration zu SQL Server aus Microsoft Access, DB2, MySQL, Oracle und Sybase.|
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Verwenden Sie die Distributed Replay-Funktion können Sie das Bewerten der Auswirkungen zukünftiger Upgrades von SQL Server. Verwenden des Distributed Replay auch Bewerten der Auswirkungen von Hardware- und Betriebssystemupgrades sowie SQL Server-Computer optimieren. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Die Ssbdiagnose (Hilfsprogramm) meldet Probleme in Service Broker-Konversationen oder die Konfiguration von Service Broker-Dienste. |


## <a name="command-line-utilities"></a>Befehlszeilenhilfsprogramme

  Befehlszeilen-Hilfsprogramme versetzen Sie in Skripts [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Vorgänge. Die folgende Tabelle enthält eine Liste der Eingabeaufforderung-Hilfsprogramme, die im Lieferumfang von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]enthalten sind.  
  
|**Hilfsprogramm**|**Beschreibung**|**Installiert in**|  
|-----------------|---------------------|----------------------|  
|[bcp (Hilfsprogramm)](../tools/bcp-utility.md)|Wird verwendet, um Daten in einem benutzerdefinierten Format zwischen einer [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz und einer Datendatei zu kopieren.|\<*Laufwerk*: > \Programme Dateien\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta (Hilfsprogramm)](../tools/dta/dta-utility.md)|Wird verwendet, um eine Arbeitsauslastung zu analysieren und Empfehlungen zu physischen Entwurfsstrukturen auszugeben, um die Serverleistung für diese Arbeitsauslastung zu optimieren.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[DTExec (Hilfsprogramm)](../integration-services/packages/dtexec-utility.md)|Wird verwendet, um ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket zu konfigurieren und auszuführen. Unter dem Namen **DTExecUI**steht eine Version dieses Hilfsprogramms mit Benutzeroberfläche zur Verfügung, über die das Paketausführungsprogramm aufgerufen wird.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Dtutil (Hilfsprogramm)](../integration-services/dtutil-utility.md)|Wird für die Verwaltung von SSIS-Paketen verwendet.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Wird verwendet, um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekte für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Instanzen bereitzustellen.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[MSSQL-Skripter (öffentliche Vorschau)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|Zum Generieren von CREATE "und" Einfügen von T-SQL-Skripts für Datenbankobjekte in SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse verwendet.|Finden Sie in unserem [GitHub-Repository](https://github.com/Microsoft/sql-xplat-cli) für Download und Nutzungsinformationen.| 
|[Osql (Hilfsprogramm)](../tools/osql-utility.md)|Ermöglicht es Ihnen, [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen, Systemprozeduren und Skriptdateien an der Eingabeaufforderung einzugeben.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Profiler-Hilfsprogramm](../tools/profiler-utility.md)|Wird verwendet, um [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] von der Eingabeaufforderung zu starten.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe-Hilfsprogramm &#40; SSRS &#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|Wird verwendet, um Skripts für die Verwaltung von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Berichtsservern auszuführen.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RSConfig-Hilfsprogramm &#40; SSRS &#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|Wird zum Konfigurieren einer Berichtsserververbindung verwendet.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt-Hilfsprogramm &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|Wird für die Verwaltung von Verschlüsselungsschlüsseln auf einem Berichtsserver verwendet.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 (Anwendung)](../tools/sqlagent90-application.md)|Wird verwendet, um den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Agent von der Eingabeaufforderung zu starten.|\<drive>:\Program Files\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd (Hilfsprogramm)](../tools/sqlcmd-utility.md)|Ermöglicht es Ihnen, [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen, Systemprozeduren und Skriptdateien an der Eingabeaufforderung einzugeben.|\<*Laufwerk*: > \Programme Dateien\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag (Hilfsprogramm)](../tools/sqldiag-utility.md)|Wird zum Sammeln von Diagnoseinformationen für den [!INCLUDE[msCoName](../includes/msconame-md.md)] -Kundenservice und -support verwendet.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Anwendung sqllogship](../tools/sqllogship-application.md)|Wird von Anwendungen zum Ausführen von Sicherungs-, Kopier- und Wiederherstellungsvorgängen und zugeordneten Cleanups für eine Protokollversandkonfiguration verwendet, ohne Sicherungs-, Kopier- und Wiederherstellungsaufträge auszuführen.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB-Hilfsprogramm](../tools/sqllocaldb-utility.md)|Ein Ausführungsmodus von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , der speziell für Programmentwickler konzipiert wurde.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint (Hilfsprogramm)](../tools/sqlmaint-utility.md)|Wird verwendet, um Datenbank-Wartungspläne auszuführen, die in früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]erstellt wurden.|\<drive>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[sqlps (Hilfsprogramm)](../tools/sqlps-utility.md)|Wird zum Ausführen von PowerShell-Befehlen und -Skripts verwendet. Lädt und registriert den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell-Anbieter sowie cmdlets.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](../tools/sqlservr-application.md)|Wird verwendet, um eine Instanz von [!INCLUDE[ssDE](../includes/ssde-md.md)] zur Problembehandlung von der Eingabeaufforderung aus zu starten und zu beenden.|\<drive>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Ssms-Hilfsprogramm](../tools/sql-server-management-studio/ssms-utility.md)|Wird verwendet, um [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] von der Eingabeaufforderung zu starten.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff (Hilfsprogramm)](../tools/tablediff-utility.md)|Wird verwendet, um Daten in zwei Tabellen im Hinblick auf Nichtkonvergenz zu vergleichen, was im Rahmen der Problembehandlung in einer Replikationstopologie hilfreich sein kann.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>SQL-Eingabeaufforderungs-Hilfsprogramme geltende Syntaxkonventionen  
  
|**Konvention**|**Syntaxelemente**|  
|--------------------|------------------|  
|GROSSBUCHSTABEN|Anweisungen und Ausdrücke, die auf Betriebssystemebene verwendet werden.|  
|`monospace`|Beispielbefehle und Programmcode.|  
|*Kursiv*|Vom Benutzer angegebene Parameter.|  
|**Fett**|Befehle, Parameter und sonstige Syntaxelemente, die genau wie angezeigt eingegeben werden müssen.|  



