---
title: Versionsanmerkungen zu SQL Server vNext | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/12/2017
ms.prod: sql-vnext
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 93d6640c3842f36f1da10b035ae32b1f0dfc027b
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-vnext-release-notes"></a>Versionsanmerkungen zu SQL Server vNext
In diesem Thema werden Einschränkungen und Probleme bei [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] beschrieben.

- Informationen über die Neuerungen in dieser Version finden Sie unter [Neues in SQL Server vNext](../sql-server/what-s-new-in-sql-server-vnext.md).
- [Versionsanmerkungen zu SQL Server unter Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes) sind auf unserer neuen und ständig wachsenden Dokumentationsplattform veröffentlicht.
- [SQL Server Reporting Services release notes (Versionshinweise für SQL Server Reporting Services)](../reporting-services/reporting-services-release-notes.md) werden im Abschnitt Reporting Services veröffentlicht.

 **Probieren Sie es aus:**    
   -   [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Download [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] aus dem **[Evaluation Center](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="sql-server-vnext-ctp-14-march--2017"></a>SQL Server vNext CTP 1.4 (März 2017)
### <a name="supported-installation-scenarios-ctp-14"></a>Unterstützte Installationsszenarios (CTP 1.4)

### <a name="documentation-ctp-14"></a>Dokumentation (CTP 1.4)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-13-february--2017"></a>SQL Server vNext CTP 1.3 (Februar 2017)
### <a name="supported-installation-scenarios-ctp-13"></a>Unterstützte Installationsszenarios (CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] dient nur als Testversion.  Produktionsbereitstellungen werden nicht unterstützt. Es wird empfohlen, [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] auf einem virtuellen Computer zu installieren und zu testen.

### <a name="documentation-ctp-13"></a>Dokumentation (CTP 1.3)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SQL Server Integration Services (SSIS) (CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>CDC-Komponenten, die in dieser CTP-Version nicht unterstützt werden.
-   **Problem und Kundenbeeinträchtigung**: Der CDC-Steuerungstask, die CDC-Quelle und der CDC-Splitter werden in dieser CTP-Version nicht unterstützt.
-   **Problemumgehung**: Es gibt keine Problemumgehung.


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-12-january--2017"></a>SQL Server vNext CTP 1.2 (Januar 2017)
### <a name="supported-installation-scenarios-ctp-12"></a>Unterstützte Installationsszenarios (CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] dient nur als Testversion.  Produktionsbereitstellungen werden nicht unterstützt. Es wird empfohlen, [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] auf einem virtuellen Computer zu installieren und zu testen.

### <a name="sql-server-database-engine-ctp-12"></a>SQL Server-Datenbankmodul (CTP 1.2)
- **Problem und der Kundenbeeinträchtigung:** In einigen Fällen bleibt der MSSQLSERVER-Dienst im Anfangsstatus hängen.
- **Problemumgehung:** So umgehen Sie dieses Problem:
  -  Erstellen Sie eine Abhängigkeit zwischen dem `mssqlserver` -Dienst und dem `keyiso` -Dienst. Führen Sie `sc config mssqlserver depend= keyiso`in einer Eingabeaufforderung mit erweiterten Berechtigungen aus.
  - Starten Sie den Computer neu.

### <a name="documentation-ctp-12"></a>Dokumentation (CTP 1.2)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SQL Server Integration Services (SSIS) (CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>Löschen des SSIS-Katalogs schlägt möglicherweise fehl, wenn SSIS für horizontales Hochskalieren installiert ist
**Problem und Kundenbeeinträchtigung:**Wenn die SSIS-Funktion für horizontales Hochskalieren auf einem Computer installiert ist, kann beim Löschen der SSISDB-Katalogdatenbank folgender Fehler auftreten: „Der Anmeldename *'login'* konnte nicht gelöscht werden, da der Benutzer zurzeit angemeldet ist.“
   
**Problemumgehung**:
-   Führen Sie auf dem Mastercomputer für horizontales Hochskalieren den Befehl „services.msc“ aus, um das Fenster „Dienste“ zu öffnen. Beenden Sie den Dienst „SQL Server Integration Services Cluster Master“.
-   Führen Sie auf den Workercomputern für horizontales Hochskalieren, die Verbindungen mit dem Master aufbauen, den Befehl „services.msc“ aus, um das Fenster „Dienste“ zu öffnen. Beenden Sie den Dienst „SQL Server Integration Services Cluster Worker“.

Nun können Sie die SSISDB-Katalogdatenbank löschen.

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services (CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>Möglicherweise funktionieren Transaktionen nicht, wenn der Typ des Entitätstransaktionsprotokolls auf „Attribut“ festgelegt ist
**Problem und Kundenbeeinträchtigung:** Wenn der Typ des Entitätstransaktionsprotokolls in **auf** Attribut [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] festgelegt ist, (der Standardwert ist **Member**), tritt bei den folgenden Szenarien ein Fehler auf:

* Transaktionen für Entitätsänderungen werden auf der Website nicht angezeigt.
* Die Seite **Transaktionen** auf der Website kann nicht geöffnet und eine Transaktion nicht rückgängig gemacht werden.
* Eine Entität kann auf der Website nicht mit einer Transaktionsanmerkung aktualisiert werden.

**Problemumgehung**: Es gibt keine Problemumgehung.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Das Kopieren von Versionen funktioniert möglicherweise nicht, wenn **Nur Versionen kopieren, für die ein Commit ausgeführt wurde** auf FALSCH festgelegt ist
-  **Problem und Kundenbeeinträchtigung:** Wenn die Einstellung **Nur Versionen kopieren, für die ein Commit ausgeführt wurde** auf **Nein** eingestellt ist (der Standardwert ist **Ja**), tritt beim Kopieren von Versionen möglicherweise ein Fehler auf. Es wird keine Fehlermeldung angezeigt.
-  **Problemumgehung**: Es gibt keine Problemumgehung.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-11-december--2016"></a>SQL Server vNext CTP 1.1 (Dezember 2016)
### <a name="supported-installation-scenarios-ctp-11"></a>Unterstützte Installationsszenarios (CTP 1.1)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] dient nur als Testversion.  Produktionsbereitstellungen werden nicht unterstützt. Es wird empfohlen, [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] auf einem virtuellen Computer zu installieren und zu testen.

Im Besonderen wurden die folgenden Szenarien, auch wenn sie bei Ihnen funktionieren können, nicht gründlich getestet und werden in **** nicht [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]unterstützt:
- Deinstallieren von CTP 1.1
- Parallelinstallationen mit anderen Versionen von SQL Server.
- Upgrade von beliebigen früheren Versionen von SQL Server.
- Im Rahmen der [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] -Installation sind keine Komponenten aus dem SQL Server Feature Pack verfügbar.

### <a name="documentation-ctp-11"></a>Dokumentation (CTP 1.1)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Gilt für:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="sql-server-master-data-services-ctp-11"></a>SQL Server Master Data Services (CTP 1.1)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>Möglicherweise funktionieren Transaktionen nicht, wenn der Typ des Entitätstransaktionsprotokolls auf „Attribut“ festgelegt ist
**Problem und Kundenbeeinträchtigung:** Wenn der Typ des Entitätstransaktionsprotokolls in **auf** Attribut [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] festgelegt ist, (der Standardwert ist **Member**), tritt bei den folgenden Szenarien ein Fehler auf:

* Transaktionen für Entitätsänderungen werden auf der Website nicht angezeigt.
* Die Seite **Transaktionen** auf der Website kann nicht geöffnet und eine Transaktion nicht rückgängig gemacht werden.
* Eine Entität kann auf der Website nicht mit einer Transaktionsanmerkung aktualisiert werden.

**Problemumgehung**: Es gibt keine Problemumgehung.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Das Kopieren von Versionen funktioniert möglicherweise nicht, wenn **Nur Versionen kopieren, für die ein Commit ausgeführt wurde** auf FALSCH festgelegt ist
-  **Problem und Kundenbeeinträchtigung:** Wenn die Einstellung **Nur Versionen kopieren, für die ein Commit ausgeführt wurde** auf **Nein** eingestellt ist (der Standardwert ist **Ja**), tritt beim Kopieren von Versionen möglicherweise ein Fehler auf. Es wird keine Fehlermeldung angezeigt.
-  **Problemumgehung**: Es gibt keine Problemumgehung.

### <a name="sql-server-integration-services-ssis-ctp-11"></a>SQL Server Integration Services (SSIS) (CTP 1.1)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>Löschen des SSIS-Katalogs schlägt möglicherweise fehl, wenn SSIS für horizontales Hochskalieren installiert ist
**Problem und Kundenbeeinträchtigung:**Wenn die SSIS-Funktion für horizontales Hochskalieren auf einem Computer installiert ist, kann beim Löschen der SSISDB-Katalogdatenbank folgender Fehler auftreten: „Der Anmeldename *'login'* konnte nicht gelöscht werden, da der Benutzer zurzeit angemeldet ist.“
   
**Problemumgehung**:
-   Führen Sie auf dem Mastercomputer für horizontales Hochskalieren den Befehl „services.msc“ aus, um das Fenster „Dienste“ zu öffnen. Beenden Sie den Dienst „SQL Server Integration Services Cluster Master“.
-   Führen Sie auf den Workercomputern für horizontales Hochskalieren, die Verbindungen mit dem Master aufbauen, den Befehl „services.msc“ aus, um das Fenster „Dienste“ zu öffnen. Beenden Sie den Dienst „SQL Server Integration Services Cluster Worker“.

Nun können Sie die SSISDB-Katalogdatenbank löschen.

#### <a name="odbc-components-are-not-supported-in-this-ctp-release"></a>ODBC-Komponenten werden in dieser CTP-Version nicht unterstützt.
**Problem und Kundenbeeinträchtigung**: Der ODBC-Verbindungs-Manager, Quelle und Ziel werden in dieser CTP-Version nicht unterstützt.

**Problemumgehung**: Es gibt keine Problemumgehung.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-vnext-ctp-10-november-2016"></a>SQL Server vNext CTP 1.0 (November 2016)
### <a name="supported-installation-scenarios-ctp10"></a>Unterstützte Installationsszenarien (CTP&1;.0)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] dient nur als Testversion.  Produktionsbereitstellungen werden nicht unterstützt. Es wird empfohlen, [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] auf einem virtuellen Computer zu installieren und zu testen.

Im Besonderen wurden die folgenden Szenarien, auch wenn sie bei Ihnen funktionieren können, nicht gründlich getestet und werden in **** nicht [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]unterstützt:
- Deinstallieren von CTP 1.0.
- Parallelinstallationen mit anderen Versionen von SQL Server.
- Upgrade von beliebigen früheren Versionen von SQL Server.
- Im Rahmen der [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] -Installation sind keine Komponenten aus dem SQL Server Feature Pack verfügbar.

### <a name="documentation-ctp-10"></a>Dokumentation (CTP 1.0)
- **Problem und Kundenbeeinträchtigung:** Die Dokumentation für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ist eingeschränkt, und die Inhalte sind im [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] -Dokumentationssatz enthalten.  Inhalte in Artikeln, die für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] spezifisch sind, sind mit **Betrifft:**gekennzeichnet. 
- **Problem und Kundenbeeinträchtigung:** Für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]sind keine Offlineinhalte verfügbar.

### <a name="sql-server-database-engine-ctp-10"></a>SQL Server-Datenbankmodul (CTP 1.0)
-  **Problem und Kundenbeeinträchtigung:** Die Funktion `STRING_AGG` in CTP1 gibt als Ergebnis einen LOB-Typ zurück (z. B. `NVARCHAR(MAX)`). In einer zukünftigen CTP-Version wird dieses Verhalten möglicherweise geändert, und `STRING_AGG` gibt möglicherweise `NVARCHAR(4000)` zurück, wenn die Eingabewerte keine LOB-Typen sind. Möglicherweise wird ein Überlauffehler ausgelöst, wenn die verketteten Ergebnisse nicht in `NVARCHAR(4000)`passen.

-  **Problem und Kundenbeeinträchtigung:** Vermeiden Sie die Verwendung von nicht reservierten Schlüsselwörtern, wie etwa `WITHIN`, als Alias für `STRING_AGG`-Ausdrücke. (Beispiel: `SELECT Company.Name, STRING_AGG(Product.Name, ',') AS WITHIN FROM TableA;`.) In einer zukünftigen CTP-Version wird das Token `WITHIN` nach einem `STRING_AGG`-Aufruf möglicherweise als Teil der `STRING_AGG`-Funktion verwendet.

-  **Problemumgehung:** Vermeiden Sie die Verwendung des `WITHIN`-Alias, oder fügen Sie `AS WITHIN` als Aliasspezifikation hinzu, um Konflikte mit zukünftigen Änderungen zu vermeiden, die der `STRING_AGG`-Funktion möglicherweise hinzugefügt werden.


### <a name="sql-server-integration-services-ctp-10"></a>SQL Server Integration Services (CTP 1.0)
#### <a name="stop-operation-in-ssis-catalog-may-fail"></a>Beim Vorgang zum Beenden im SSIS-Katalog tritt möglicherweise ein Fehler auf
**Problem und Kundenbeeinträchtigung:** Beim Beenden eines Vorgangs in [!INCLUDE[ssIS_md](../includes/ssis-md.md)] mithilfe von [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] oder der gespeicherten Prozedur „catalog.stop_operation“ tritt möglicherweise der folgende Fehler auf: „.NET Framework-Fehler beim Ausführen der benutzerdefinierten Routine oder des benutzerdefinierten Aggregats ‚stop_operation_internal‘“.

-  **Problemumgehung:** Öffnen Sie den Windows Task-Manager. Suchen Sie auf der Registerkarte **Prozesse** den Prozess mit dem Namen **ISServerExec** , und klicken Sie auf **Task beenden** , um den Prozess zu beenden.

#### <a name="create-dump-of-ssis-pacakge-execution-may-fail"></a>Beim Erstellen eines Speicherabbilds der Ausführung des SSIS-Pakets tritt möglicherweise ein Fehler auf
**Problem und Kundenbeeinträchtigung:** Beim Erstellen eines Speicherabbilds für die Ausführung eines Pakets mithilfe der gespeicherten Prozedur „catalog.create_execution_dump“ tritt möglicherweise der folgende Fehler auf: „.NET Framework-Fehler beim Ausführen der benutzerdefinierten Routine oder des benutzerdefinierten Aggregats ‚create_execution_dump_internal‘“.

-  **Problemumgehung:** Öffnen Sie den Windows Task-Manager. Suchen Sie auf der Registerkarte **Prozesse** den Prozess mit dem Namen **ISServerExec**, klicken Sie mit der rechten Maustaste auf den Prozess, und klicken Sie dann auf **Abbilddatei erstellen**.

#### <a name="get-perf-counter-of-ssis-package-execution-may-fail"></a>Beim Abrufen des Leistungsindikators für die Ausführung des SSIS-Pakets tritt möglicherweise ein Fehler auf
**Problem und Kundenbeeinträchtigung:** Beim Abfragen der [!INCLUDE[ssIS_md](../includes/ssis-md.md)] -Leistungsindikatoren mithilfe der Tabellenwertfunktion „catalog.dm_execution_performance_counters“ tritt möglicherweise der folgende Fehler auf: „.NET Framework-Fehler beim Ausführen der benutzerdefinierten Routine oder des benutzerdefinierten Aggregats ‚get_execution_perf_counters‘“.

-  **Problemumgehung**: Verwenden Sie den Windows-Systemmonitor, um die Werte der Leistungsindikatoren direkt zu überwachen. Es gibt keine Problemumgehung für Leistungsindikatoren für die Ausführung eines bestimmten Pakets.

#### <a name="deleting-catalog-may-fail-when-ssis-scale-out-master-is-installed"></a>Beim Löschen des Katalogs tritt möglicherweise ein Fehler auf, wenn der SSIS-Master für horizontales Hochskalieren installiert ist
**Problem und Kundenbeeinträchtigung:** Wenn das [!INCLUDE[ssIS_md](../includes/ssis-md.md)] -Feature zum horizontalen Hochskalieren auf einem Computer installiert ist, kann beim Löschen des **SSISDB** -Katalogs der folgende Fehler auftreten: „Der Anmeldename ‚…‘ konnte nicht gelöscht werden, da der Benutzer zurzeit angemeldet ist.“ 

**Problemumgehung**: 
* Führen Sie auf einem Mastercomputer für horizontales Hochskalieren den Befehl „services.msc“ aus, um das Fenster **Dienste** zu öffnen, und beenden Sie den Dienst **SQL Server Integration Services Cluster Master** . 

* Auf den Workercomputern für horizontales Hochskalieren, die Verbindungen mit dem Master aufbauen, führen Sie den Befehl „services.msc“ aus, um das Fenster **Dienste** zu öffnen. Beenden Sie den Dienst **SQL Server Integration Services Cluster Worker** . 

Jetzt sollte es möglich sein, den **SSISDB** -Katalog zu löschen.

#### <a name="odbc-connector-in-ssis-is-not-supported"></a>Der ODBC-Connector in SSIS wird nicht unterstützt
-  **Problem und Kundenbeeinträchtigung:** Der ODCB-Connector in [!INCLUDE[ssIS_md](../includes/ssis-md.md)] wird nicht unterstützt.
-  **Problemumgehung:** Es gibt keine Problemumgehung.

### <a name="sql-server-reporting-services-ctp-10"></a>SQL Server Reporting Services (CTP 1.0)

Für SQL Server Reporting Services werden keine neuen Features für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]veröffentlicht.

### <a name="sql-server-master-data-services-ctp-10"></a>SQL Server Master Data Services (CTP 1.0)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>Möglicherweise funktionieren Transaktionen nicht, wenn der Typ des Entitätstransaktionsprotokolls auf „Attribut“ festgelegt ist
**Problem und Kundenbeeinträchtigung:** Wenn der Typ des Entitätstransaktionsprotokolls in **auf** Attribut [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] festgelegt ist, (der Standardwert ist **Member**), tritt bei den folgenden Szenarien ein Fehler auf:

* Transaktionen für Entitätsänderungen werden auf der Website nicht angezeigt.
* Die Seite **Transaktionen** auf der Website kann nicht geöffnet und eine Transaktion nicht rückgängig gemacht werden.
* Eine Entität kann auf der Website nicht mit einer Transaktionsanmerkung aktualisiert werden.

**Problemumgehung**: Es gibt keine Problemumgehung.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>Das Kopieren von Versionen funktioniert möglicherweise nicht, wenn **Nur Versionen kopieren, für die ein Commit ausgeführt wurde** auf FALSCH festgelegt ist
**Problem und Kundenbeeinträchtigung:** Wenn die Einstellung **Nur Versionen kopieren, für die ein Commit ausgeführt wurde** auf **Nein** eingestellt ist (der Standardwert ist **Ja**), tritt beim Kopieren von Versionen möglicherweise ein Fehler auf. Es wird keine Fehlermeldung angezeigt.

**Problemumgehung**: Es gibt keine Problemumgehung.
 
### <a name="sql-server-management-studio-ssms-ctp-10"></a>SQL Server Management Studio (SSMS) (CTP 1.0)
SQL Server Management Studio ist ein separater Download.  Die neuesten Informationen finden Sie in den [Versionshinweisen zu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238486.aspx).

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Kontaktaufnahme mit dem SQL Server-Entwicklungsteam 
- [Stack Overflow (Tag „sql-server“): Anlaufstelle für technische Fragen](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN-Foren: Anlaufstelle für technische Fragen](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: Meldung von Programmfehlern und Vorschlagen von Features](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: Allgemeine Diskussion zu R](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


