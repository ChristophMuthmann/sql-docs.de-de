---
title: SQL Server 2017 Release Notes | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/30/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: fe3554aa067ef7e7fd0c1ffa2e8ac3adc5aaaa07
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-2017-release-notes"></a>Versionsanmerkungen zu SQL Server 2017
In den folgenden Artikeln werden Einschränkungen und Probleme mit SQL Server 2017 beschrieben. Verwandte Informationen finden Sie unter:
- [Neues in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
- [SQL Server unter Linux: Anmerkungen zu dieser Version](https://docs.microsoft.com/sql/linux/sql-server-linux-release-notes)
- [SQL Server 2017 Cumulative updates (Kumulative Updates für SQL Server 2017)](http://aka.ms/sql2017cu) für Informationen zu den aktuellen kumulativen Updates

**Probieren Sie SQL Server aus!**
- [![Download aus dem Evaluierungscenter](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [SQL Server 2017 herunterladen](http://go.microsoft.com/fwlink/?LinkID=829477)
- [![Erstellen eines virtuellen Computers](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [Starten von virtuellen Computern mit SQL Server 2017](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)

## <a name="sql-server-2017---general-availability-release-october-2017"></a>SQL Server 2017: allgemein verfügbare Releaseversion (Oktober 2017)
### <a name="database-engine"></a>Datenbankmodul

- **Problem- und Kundenbeeinträchtigung**: Nach dem Upgrade ist die bestehende FILESTREAM-Netzwerkfreigabe möglicherweise nicht mehr verfügbar.

- **Problemumgehung**: Starten Sie den Computer neu, und prüfen Sie, ob die FILESTREAM-Netzwerkfreigabe verfügbar ist. Führen Sie folgende Schritte aus, wenn die Freigabe danach noch immer nicht verfügbar ist:

    1. Klicken Sie im SQL Server-Konfigurations-Manager erst mit der rechten Maustaste auf die SQL Server-Instanz und anschließend auf **Eigenschaften**. 
    2. Deaktivieren Sie in der Registerkarte **FILESTREAM** die Funktion **FILESTREAM für E/A-Streamingzugriff auf Datei aktivieren**, und klicken Sie anschließend auf **Anwenden**.
    3. Aktivieren Sie dann erneut **FILESTREAM für E/A-Streamingzugriff auf Datei aktivieren** mit dem ursprünglichen Freigabenamen, und klicken Sie auf **Anwenden**.

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- **Problem- und Kundenbeeinträchtigung**: Auf der Benutzerberechtigungsseite wird Ihnen der folgende Fehler angezeigt, wenn sie in der Strukturansicht auf Stammebene eine Berechtigung erteilen: `"The model permission cannot be saved. The object guid is not valid"`

- **Problemumgehungen:** 
  - Grant permission on the sub nodes in the tree view instead of the root level (Erteilen Sie Berechtigung auf den vorhandenen Knoten in der Strukturansicht anstatt auf Stammebene).
  - oder
  - Führen Sie das Skript aus, das im MDS-Teamblogpost [error applying permission on entity level (Fehler bei der Erteilung von Berechtigungen auf Entitätsebene)](http://sqlblog.com/blogs/mds_team/archive/2017/09/05/sql-server-2016-sp1-cu4-regression-error-while-applying-permission-on-entity-level-quick-workaround.aspx) beschrieben wird.

### <a name="analysis-services"></a>Analysis Services
- **Problem und Kundenbeeinträchtigung**: Datenconnectors für die folgenden Quellen sind für tabellarische Modelle mit Kompatibilitätsgrad 1400 noch nicht verfügbar.
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **Problemumgehung:** Keine   

- **Problem- und Kundenbeeinträchtigung**: Direkte Abfragemodelle mit Perspektiven und dem Kompatibilitätsgrad 1400 können fehlschlagen, wenn Metadaten abgefragt oder ermittelt werden.
- **Problemumgehung**: Entfernen Sie Perspektiven, und stellen Sie diese erneut bereit.

### <a name="tools"></a>Tools
- **Problem- und Kundenbeeinträchtigung**: Das Ausführen von *DReplay* schlägt fehl, und die folgende Fehlermeldung wird angezeigt: "Error DReplay Unexpected error occurred!" (Fehler DReplay: Es ist ein unerwarteter Fehler aufgetreten!).
- **Problemumgehung:** Keine

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc2---august-2017"></a>SQL Server 2017 Release Candidate (RC2: August 2017)
Es gibt keine Anmerkungen zu dieser Version von SQL Server für Windows. Siehe: [SQL Server on Linux Release notes (Versionsanmerkungen zu SQL Server unter Linux)](https://docs.microsoft.com/sql/linux/sql-server-linux-release-notes).


![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 Release Candidate (RC1 – Juli 2017)
### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SQL Server Integration Services (SSIS) (RC1 – Juli 2017)
- **Problem und Kundenbeeinträchtigung:** Der Parameter *runincluster* der gespeicherten Prozedur **[catalog].[create_execution]** wird hinsichtlich Konsistenz und Lesbarkeit in *runinscaleout* umbenannt.
- **Problemumgehung:** Wenn Sie vorhandene Skripts zum Ausführen von Paketen in Scale Out haben, müssen Sie den Parameternamen von *runincluster* in *runinscaleout* ändern, damit die Skripts in RC1 arbeiten.

- **Problem und Kundenbeeinträchtigung:** SQL Server Management Studio (SSMS) 17.1 und frühere Versionen können die Ausführung des Pakets in Scale Out in RC1 nicht auslösen. Die Fehlermeldung lautet: "*@runincluster* is not a parameter for procedure **create_execution** (ist kein Parameter für die Prozedur create_execution)." Dieses Problem wurde in der nächsten Version von SSMS, (Version 17.2) behoben. Die Version 17.2 und spätere SSMS-Versionen unterstützen den neuen Parameternamen und die Paketausführung in Scale Out. 
- **Problemumgehung**, bis Version 17.2 von SSMS verfügbar ist:
  1. Verwenden Sie Ihre bestehende Version von SSMS, um das Paketausführungsskript zu generieren.
  2. Ändern Sie den Namen des Parameters *runincluster* im Skript zu *runinscaleout*.
  3. Führen Sie das Skript aus.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (Mai 2017)
### <a name="documentation-ctp-21"></a>Dokumentation (CTP 2.1)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **Problem und Kundenbeeinträchtigung**: Wenn Sie sowohl SQL Server Reporting Services als auch Power BI-Berichtsserver auf demselben Computer installiert haben und eines davon deinstallieren, können Sie keine Verbindung mit dem verbleibenden Berichtsserver mit dem Berichtsserver-Konfigurations-Manager herstellen.
- **Problemumgehung:** Um dieses Problem zu umgehen, müssen Sie nach der Deinstallation einer der Server die folgenden Vorgänge ausführen.

    1. Starten Sie eine Eingabeaufforderung im Administratormodus.
    2. Wechseln Sie zu dem Verzeichnis, in dem der verbleibenden Berichtsserver installiert ist.

        *Standardspeicherort für den Power BI-Berichtsserver: C:\Programme\Microsoft Power BI-Berichtsserver*

        *Standardspeicherort für SQL Server Reporting Services: C:\Programme\Microsoft SQL Server Reporting Services*

    3. Wechseln Sie dann zum nächsten Ordner. Dabei handelt es sich entweder um *SSRS* oder um *PBIRS*, je nachdem, was verbleibt.
    4. Wechseln Sie zum WMI-Ordner.
    5. Führen Sie den folgenden Befehl aus:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Wenn die folgende Fehlermeldung angezeigt wird, ignorieren Sie diese.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **Problem und Kundenbeeinträchtigung:** Nach der Installation auf einem Computer mit 2016er-Version von *TSqlLanguageService.msi* (entweder über SQL-Setup oder als eigenständiges Redistributable) werden die v13.* (SQL 2016)-Versionen von *Microsoft.SqlServer.Management.SqlParser.dll* und *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* entfernt. Jede Anwendung mit einer Abhängigkeit von den 2016er-Versionen dieser Assemblys funktioniert dann nicht mehr und generiert einen Fehler ähnlich dem folgenden: *error : Could not load file or assembly 'Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. (Fehler: Die Datei oder Assembly „Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91“ oder eine Abhängigkeit davon wurde nicht gefunden.) Das System kann die angegebene Datei nicht finden.*

   Darüber hinaus wird beim Versuch, eine 2016er-Version von „TSqlLanguageService.msi“ neu zu installieren, die folgende Fehlermeldung angezeigt: *Fehler bei der Installation von Microsoft SQL Server 2016 T-SQL-Sprachdienst, da eine neuere Version bereits auf dem Computer vorhanden ist*.

- **Problemumgehung:** Um dieses Problem zu umgehen und eine Anwendung zu korrigieren, die von der v13-Version des Assemblys abhängt, gehen Sie folgendermaßen vor:

   1. Wechseln Sie zu **Programme hinzufügen/entfernen**.
   2. Suchen Sie nach *Microsoft SQL Server vNext T-SQL-Sprachdienst CTP2.1*, klicken Sie mit der rechten Maustaste darauf, und klicken Sie dann auf **Deinstallieren**.
   3. Nachdem die Komponente entfernt wurde, reparieren Sie die kaputte Anwendung oder installieren Sie die entsprechende Version von *TSqlLanguageService.MSI* neu.

   Diese Problemumgehung entfernt die v14-Version dieser Assemblys, sodass alle Anwendungen, die von den v14-Versionen abhängen, nicht mehr funktionieren. Wenn diese Assemblys erforderlich sind, ist eine separate Installation ohne parallele 2016er-Installationen erforderlich.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (April 2017)
### <a name="documentation-ctp-20"></a>Dokumentation (CTP 2.0)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="always-on-availability-groups"></a>AlwaysOn-Verfügbarkeitsgruppen

- **Problem und Kundenbeeinträchtigung:** Eine SQL Server-Instanz, die ein sekundäres Replikat einer Verfügbarkeitsgruppe hostet, stürzt ab, wenn die Hauptversion von SQL Server älter ist als die Instanz, die das primäre Replikat hostet. Hat Auswirkungen auf Upgrades von allen unterstützten Versionen von SQL Server, die Verfügbarkeitsgruppen für SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0 hosten. Dieses Problem tritt unter den folgenden Bedingungen auf. 

> 1. Ein Benutzer aktualisiert die SQL Server-Instanz, die ein sekundäres Replikat hostet, gemäß den [bewährten Methoden](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).
> 2. Nach dem Upgrade tritt ein Failover auf, und ein neu aktualisiertes sekundäres Replikat wird zum primären Replikat, bevor das Upgrade für alle sekundären Replikate in der Verfügbarkeitsgruppe abgeschlossen ist. Das frühere primäre Replikat ist nun ein sekundäres Replikat, d.h. mit niedrigerer Version als das primäre Replikat.
> 3. Die Verfügbarkeitsgruppe befindet sich in einer nicht unterstützten Konfiguration, und für die verbleibenden sekundären Replikate könnte die Gefahr bestehen, dass sie abstürzen. 

- **Problemumgehung:** Stellen Sie eine Verbindung mit der SQL Server-Instanz her, die das neue primäre Replikat hostet, und entfernen Sie das fehlerhafte sekundäre Replikat aus der Konfiguration.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   Die SQL Server-Instanz, die das sekundäre Replikat hostet, wird wiederhergestellt.

## <a name="more-information"></a>Weitere Informationen
- [SQL Server Reporting Services release notes (Versionshinweise für SQL Server Reporting Services)](../reporting-services/reporting-services-release-notes.md)beschrieben.
- [Known Issues for Machine Learning Services (Bekannte Probleme bei Machine Learning-Diensten)](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
- [SQL Server-Update Center – Links und Informationen zu allen unterstützten Versionen](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
