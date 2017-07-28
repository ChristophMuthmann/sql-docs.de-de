---
title: Versionsanmerkungen zu SQL Server 2017 | Microsoft Docs
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: de-de
ms.lasthandoff: 07/17/2017

---
# <a name="sql-server-2017-release-notes"></a>Versionsanmerkungen zu SQLServer 2017
In diesem Thema werden Einschränkungen und Probleme bei [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]beschrieben. Verwandte Informationen finden Sie in den folgenden Artikeln:

- [Neuigkeiten in SQLServer 2017](../sql-server/what-s-new-in-sql-server-2017.md).
- [SQL Server auf Linux-Versionshinweise](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes).
- [SQL Server Reporting Services release notes (Versionshinweise für SQL Server Reporting Services)](../reporting-services/reporting-services-release-notes.md)beschrieben.

 **Probieren Sie es aus:**    
   -   [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Download [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] aus dem **[Evaluation Center](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 Release Candidate (RC1 – Juli 2017)

### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1 – Juli 2017)
- **Problem und Kundenbeeinträchtigung:** Der Parameter *runincluster* der gespeicherten Prozedur **[catalog].[create_execution]** wird hinsichtlich Konsistenz und Lesbarkeit in *runinscaleout* umbenannt.
- **Problemumgehung:** Wenn Sie vorhandene Skripts zum Ausführen von Paketen in Scale Out haben, müssen Sie den Parameternamen von *runincluster* in *runinscaleout* ändern, damit die Skripts in RC1 arbeiten.

- **Problem und Kundenbeeinträchtigung:** SQL Server Management Studio (SSMS) 17.1 und frühere Versionen können die Ausführung des Pakets in Scale Out in RC1 nicht auslösen. Die Fehlermeldung lautet: "*@runincluster* is not a parameter for procedure **create_execution** (ist kein Parameter für die Prozedur create_execution)." Dieses Problem wurde in der nächsten Version von SSMS, (Version 17.2) behoben. Die Version 17.2 und spätere SSMS-Versionen unterstützen den neuen Parameternamen und die Paketausführung in Scale Out. 
- **Problemumgehung:** Bis die SSMS-Version 17.2 verfügbar ist, können Sie Ihre vorhandene Version von SSMS verwenden, um das Paketausführungsskript zu generieren. Ändern Sie anschließend im Skript den Namen des Parameters *runincluster* in *runinscaleout*, und führen Sie das Skript aus.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>2.1 (Mai 2017) 2017 CTP für SQL Server
### <a name="documentation-ctp-21"></a>Die Dokumentation (CTP-Version 2.1)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP-Version 2.1)

- **Problem und kundenbeeinträchtigung:** , wenn Sie SQL Server Reporting Services und Power BI Berichtsserver auf demselben Computer aus, und Deinstallieren eines davon haben, Sie werden nicht mehr auf dem verbleibenden Berichtsserver mit Berichtsserver Konfigurations-Manager eine Verbindung herstellen können.
- **Problemumgehung** um dieses Problem zu umgehen, müssen Sie nach der Deinstallation von einem der Server die folgenden Vorgänge ausführen.

    1. Starten Sie eine Eingabeaufforderung im Administratormodus.
    2. Wechseln Sie zu dem Verzeichnis, in dem die verbleibenden Berichtsserver installiert ist.

        *Standardspeicherort für Power BI-Berichtsserver: C:\Program Files\Microsoft Power BI-Berichtsserver*

        *Standardspeicherort für SQL Server Reporting Services: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. Wechseln Sie dann zu dem Ordner. Diese werden entweder *SSRS* oder *PBIRS* je nachdem, welche verfügbare Spannung anzeigt.
    4. Wechseln Sie zu den WMI-Ordner.
    5. Führen Sie den folgenden Befehl aus:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Wenn es angezeigt wird, können Sie den folgenden Fehler ignorieren.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP-Version 2.1)

- **Problem und kundenbeeinträchtigung:** nach der Installation auf einem Computer mit einer Version von 2016 *TSqlLanguageService.msi* (entweder über SQL-Setup oder als eigenständige verteilbare) v13.* (SQL 2016)-Versionen installiert *Microsoft.SqlServer.Management.SqlParser.dll* und *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* werden entfernt. Jede Anwendung, die eine Abhängigkeit für die 2016 Versionen dieser Assemblys verfügen werden dann nicht mehr ordnungsgemäß, wodurch eine Fehlermeldung ähnlich: *Fehler: konnten nicht geladen werden, Datei oder Assembly ' Microsoft.SqlServer.Management.SqlParser, Version = 13.0.0.0, Culture = Neutral, PublicKeyToken = 89845dcd8080cc91 "oder eine ihrer Abhängigkeiten. Die angegebene Datei wurde nicht gefunden.*

   Darüber hinaus versucht, eine Version von TSqlLanguageService.msi 2016 neu installieren mit der Meldung fehl: *Installation von Microsoft SQL Server 2016 T-SQL Language Service ist fehlgeschlagen, da bereits eine höhere Version auf dem Computer vorhanden ist*.

- **Problemumgehung** gehen Sie folgendermaßen vor, um die Version der Assemblys, dieses Problem zu umgehen, und Beheben von einer Anwendung, von denen die v13 abhängt:

   1. Wechseln Sie zu **Programme hinzufügen/entfernen**
   1. Suchen *Microsoft SQL Server vNext T-SQL Language Service CTP2. 1*mit der rechten Maustaste auf ihn, und wählen Sie **Deinstallieren**.
   1. Nach dem Entfernen der Komponente, reparieren Sie die Anwendung, die unterbrochen wird (oder installieren Sie die entsprechende Version von *TSqlLanguageService.MSI*)

   Diese problemumgehung wird die 14-Version dieser Assemblys entfernt, damit jede Anwendung, die abhängig von der 14-Versionen nicht mehr funktionieren. Wenn diese Assemblys erforderlich sind, ist eine separate Installation ohne Seite-an-Seite 2016 Installationen erforderlich.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>2017 CTP 2.0 (April 2017) für SQL Server
### <a name="documentation-ctp-20"></a>Die Dokumentation (CTP 2.0)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="always-on-availability-groups"></a>AlwaysOn-Verfügbarkeitsgruppen

- **Problem und kundenbeeinträchtigung:** einer SQL Server-Instanz, die auf ein sekundären Replikat der verfügbarkeitsgruppe gehostet stürzt ab, wenn die SQL Server-Hauptversion kleiner als die Instanz ist, die das primäre Replikat hostet. Wirkt sich auf Upgrades von allen unterstützten Versionen von SQL Server, die zu SQL Server-Verfügbarkeitsgruppen hosten [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. Dies geschieht unter die folgenden Schritte aus. 

> 1. Benutzer aktualisiert die SQL Server-Instanz Hostens sekundäres Replikat in Abhängigkeit von [bewährte Methoden](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Nach dem Upgrade ein Failover auftritt und aktualisierten sekundäre Replikat zum primären, vor dem Abschluss der Aktualisierung für alle sekundären Replikate der verfügbarkeitsgruppe angehören. Das frühere primäre ist jetzt ein sekundäres Replikat die niedrigere Version als primäre ist.
> 3. Die verfügbarkeitsgruppe befindet sich eine nicht unterstützte Konfiguration und die verbleibenden sekundären Replikaten zum Absturz Sicherheitsrisiken ausgesetzt sein. 

- **Problemumgehung** Herstellen einer Verbindung mit SQL Server-Instanz hostet das neue primäre Replikat und das Entfernen der fehlerhaften sekundäres Replikat aus der Konfiguration.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   Die Instanz von SQL Server, die das sekundäre Replikat gehostet wird wiederhergestellt.

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Kontaktaufnahme mit dem SQL Server-Entwicklungsteam 
- [Stack Overflow (Tag „sql-server“): Anlaufstelle für technische Fragen](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN-Foren: Anlaufstelle für technische Fragen](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: Meldung von Programmfehlern und Vorschlagen von Features](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: Allgemeine Diskussion zu R](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
