---
title: "Aktualisiert – SQL Server on Linux Docs | Microsoft Docs"
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für Microsoft SQL Server on Linux Codeausschnitte anzeigen"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 13c237af359c543f6a99a0fce101af81b5eb2bcf
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Neue und zuletzt aktualisiert: SQL Server on Linux Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-05-23** &nbsp; - zu - &nbsp; **2017-07-17**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Microsoft SQL Server on Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Führen Sie die 2017 von SQL Server-Container-Image mit Docker](quickstart-install-connect-docker.md)
2. [Installieren von SQL Server, und erstellen Sie eine Datenbank auf Red Hat](quickstart-install-connect-red-hat.md)
3. [Installieren von SQL Server, und erstellen Sie eine Datenbank auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
4. [Installieren von SQL Server, und erstellen Sie eine Datenbank für Ubuntu](quickstart-install-connect-ubuntu.md)
5. [Beispiel: Für die unbeaufsichtigte SQL Server-Installationsskript für Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
6. [Beispiel: Für die unbeaufsichtigte SQL Server-Installationsskript für SUSE Linux Enterprise Server](sample-unattended-install-suse.md)
7. [Beispiel: Für die unbeaufsichtigte SQL Server-Installationsskript für Ubuntu](sample-unattended-install-ubuntu.md)
8. [Active Directory-Authentifizierung mit SQLServer on Linux](sql-server-linux-active-directory-authentication.md)
9. [Hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md)
10. [Konfigurieren von SQL Server-2017 Container Bilder auf Docker](sql-server-linux-configure-docker.md)
11. [Feedback von Kunden für SQLServer on Linux](sql-server-linux-customer-feedback.md)
12. [Verschlüsseln von Verbindungen zu SQLServer on Linux](sql-server-linux-encrypted-connections.md)
13. [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-sles-cluster-for-sql-server-availability-groupsql-server-linux-availability-group-cluster-slesmd"></a>1. &nbsp;[SLES Cluster für SQL Server-Verfügbarkeitsgruppe zu konfigurieren.](sql-server-linux-availability-group-cluster-sles.md)

*Updated: 2017-06-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 189.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f8d28af253be1dc67615f1ea04135b2f6dff3b71 8be07deddcf0c348d75bf5b4f44615c2383e0722  (PR=2150  ,  Filename=sql-server-linux-availability-group-cluster-sles.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=6dccaff93a6c8b2374a1fad069b2f597898802fc) -->



**Festlegen Sie Clustereigenschaft auf "false" Start-Fehler-ist--Schwerwiegender**


`Start-failure-is-fatal`Gibt an, ob ein Fehler beim Starten einer Ressource auf einem Knoten weiter Start Versuche auf diesem Knoten verhindert. Bei Festlegung auf `false`, der Cluster wird entscheiden Sie, ob auf demselben Knoten erneut basierend auf der Ressource aktuelle Anzahl und Migration Fehlerschwellenwert starten. Daher nach dem Failover unternimmt Schrittmacher starten die verfügbarkeitsgruppenressource auf dem ehemaligen primären SQL-Instanz verfügbar ist. Schrittmacher übernimmt die Herabstufung des sekundäre Replikats, und es wird automatisch die verfügbarkeitsgruppe erneut. Auch wenn `start-failure-is-fatal` festgelegt ist, um `false`, des Clusters wird ein Fallback auf die konfigurierten Failcount Grenzwerte, die mit der Migration Schwellenwert konfiguriert werden, daher müssen Sie Sie sicher, dass der standardanwendung für die Migration Schwellenwert entsprechend aktualisiert wird.

So aktualisieren Sie den Wert der Eigenschaft auf "false" ausführen:
```
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
Wenn die Eigenschaft den Standardwert hat `true`, wenn beim ersten Versuch zum Starten der Ressource nicht erfolgreich war, ein Eingreifen des Benutzers erforderlich, nach der ein automatisches Failover an den Bereinigungstasks, die Anzahl der Ressourcen-Fehler ist und der Konfiguration verwendet zurücksetzen: `sudo crm resource cleanup <resourceName>` Befehl.

Weitere Informationen zur Schrittmacher Clustereigenschaften finden Sie [Clusterressourcen konfigurieren](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

**Konfigurieren von Fencing (STONITH)**

Schrittmacher Cluster Lieferanten erfordern STONITH aktiviert werden und ein Fencing Gerät für ein unterstütztes Clustersetup konfiguriert. Wenn der Cluster-Ressourcen-Manager den Status eines Knotens oder einer Ressource auf einem Knoten nicht ermitteln kann, wird Fencing verwendet, auf den Cluster erneut in einen bekannten Zustand zu versetzen.
Ressource Ebene Zäune hauptsächlich wird sichergestellt, dass es keine beschädigte Daten bei einem Ausfall durch Konfigurieren einer Ressource. Können Sie Ressourcen Ebene Zäune, z. B. mit DRBD (Distributed repliziert Blockgerät), um den Datenträger auf einem Knoten, wie wenn veraltet zu markieren der kommunikationsverbindung ausfällt.




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>2. &nbsp;[Versionshinweise für SQL Server-2017 unter Linux](sql-server-linux-release-notes.md)

*Updated: 2017-06-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 156.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 684da20f7834000886d7a93f83563c55dc3cf9a6 8597bcde7e5754bb7f38de1ec980027245dac6e5  (PR=2115  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=424a23fd98876db808b91f017e7acbcb5b4daa45) -->



**SQL Server Integration Services (SSIS)**

Sie können SSIS-Pakete auf Linux ausführen. Weitere Informationen finden Sie unter der [Blog Post Ankündigung SSIS-Unterstützung für Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Bitte beachten Sie die folgenden bekannten Probleme mit dieser Version.

- Die **Mssql Server ist** Paket wird nur auf Ubuntu zu diesem Zeitpunkt unterstützt.

- Die folgenden Funktionen werden nicht unterstützt, wenn SSIS-Pakete auf Linux ausgeführt wird:
  - SSIS-Katalog DB
  - Planen der Ausführung von Paketen vom SQL-Agent
  - Windows-Authentifizierung
  - Drittanbieter-Komponenten
  - ODBC-Treiber von Drittanbietern
  - ODBC-Verbindungs-Manager, Quelle und Ziel (mit SSIS auf Linux CTP-Version 2.1 aktualisieren unterstützt)
  - Change Data Capture (CDC)
  - Horizontale Hochskalierung
  - Azure Feature Pack
  - Hadoop und HDFS-Unterstützung
  - Microsoft Connector for SAP BW

Mit SSIS auf Linux CTP-Version 2.1 aktualisiert können SSIS-Pakete auf Linux ODBC-Verbindungen. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>Ähnliche Artikel

Dieser Abschnitt enthält sehr ähnlich Artikel für die zuletzt aktualisierten Artikel in anderen Themenbereichen, innerhalb des gleichen "github.com" Repository: [MicrosoftDocs /**Sql-Docs-Pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Die neue oder kürzlich aktualisierten Artikel haben Themenbereiche

- [Neue und aktualisierte (4 + 4): **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (2 + 0): **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (1 + 2): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (6 + 0): **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (13 + 2): **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (1 + 0): **Master Data Services (MDS) für SQL** Docs](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (1 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (8 + 4): **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (2 + 2): **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (0 + 1): **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (1 + 0): **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (1 + 0): **-Tools für SQL** Docs](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die keine Artikel neu oder vor kurzem aktualisiert haben.

- [Neue und aktualisierte (0 + 0): **ActiveX Data Objects (ADO) für SQL** Docs](../ado/new-updated-ado.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [Neue und aktualisierte (0 + 0): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (0 + 0): **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../sample/new-updated-sample.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)


&nbsp;


