---
title: SQLServer on Linux – häufig gestellte Fragen | Microsoft Docs
description: Dieser Artikel enthält Antworten auf häufig gestellte Fragen zu SQL Server auf dem Linux ausgeführt wird.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Active
ms.openlocfilehash: 4d59b7f4d2c88640f3f925949f8938e689d1e029
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Häufig gestellte Fragen (FAQS) SQLServer on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Die folgenden Abschnitte enthalten allgemeine Fragen und Antworten für SQL Server auf Linux laufende.

## <a name="general-questions"></a>Allgemeine Fragen

1. **Welche Linux-Plattformen unterstützt werden?**

   SQL Server wird derzeit auf Red Hat Enterprise Server, SUSE Linux Enterprise Server und Ubuntu unterstützt. Sie unterstützt auch in einem Container mit Docker. Aktuelle Informationen zu den unterstützten Versionen finden Sie unter [unterstützte Plattformen](sql-server-linux-setup.md#supportedplatforms).

1. **Wird SQL Server on Linux auf anderen Plattformen funktionieren**?

   SQL Server wird getestet und für die zuvor aufgelisteten Verteilungen unter Linux unterstützt. Andere Linux-Distributionen sind eng miteinander verknüpft und kann in der Lage, SQL Server ausgeführt wird (z. B. CentOS ist eng mit Red Hat Enterprise Server). Aber wenn Sie entscheiden, SQL Server auf ein nicht unterstütztes Betriebssystem zu installieren, lesen Sie bitte die **Supportrichtlinie** Teil der [technischen Support-Richtlinie für Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) zu verstehen, die Unterstützung Auswirkungen auf. Beachten Sie außerdem, dass einige Community-, dass die Linux-Distributionen keine formale Möglichkeit verwaltet, die Unterstützung zu erhalten, wenn das zugrunde liegende Betriebssystem, das Problem ist.

1. **Welche SQL Server-Funktionen unter Linux unterstützt werden?**

   Eine vollständige Liste der unterstützten Funktionen und bekannten Probleme, finden Sie unter der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md).

1. **Was ist der Supportrichtlinie für SQL Server?**

   Um die Support-Richtlinie zu verstehen, überprüfen Sie die [technischen Support-Richtlinie für SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

1. **Ich bin aus dem Microsoft SQL Server-Umfeld stammen. Gibt es Ressourcen, die Informationen zum Verwenden von SQL Server on Linux helfen?**

   Die [Schnellstarts](sql-server-linux-setup.md#platforms) enthalten schrittweise Anleitungen zum Installieren von SQL Server unter Linux und Ausführen von Transact-SQL-Abfragen. Weitere Lernprogramme enthalten zusätzliche Anweisungen zur Verwendung von SQL Server unter Linux. Tipps, eine Liste von Drittanbietern finden Sie unter der [MSSQLTIPS Liste der SQL Server on Linux Tipps](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/).

## <a name="installation"></a>Installation

1. **Wie erhalte ich auf Meine Linux-Server installierten SQL Server?**

   Microsoft Paket-Repositorys für die Installation von SQL Server verwaltet und unterstützt die Installation über systemeigenen Paket-Manager, z. B. Yum Zypper, und apt. Um schnell zu installieren, finden Sie in der [Schnellstarts](sql-server-linux-setup.md#platforms).

1. **Können SQL Server auf dem Linux-Subsystem für Windows 10 werden installiert?**

   Nein. Windows 10 unter Linux ist zurzeit nicht unterstützte Plattform für SQL Server und verwandte Tools.

1. **Die Linux-Dateisysteme können 2017 von SQL Server für Datendateien werden verwendet?**

   Zurzeit unterstützt SQL Server on Linux ext4 und XFS. Unterstützung für andere Dateisysteme wird hinzugefügt werden, da in Zukunft benötigt.

1. **Kann ich die Installationspakete aus, um SQL Server offline-Installation herunterladen?**

   Ja. Weitere Informationen finden Sie in das Paket herunterladen von Links in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Überprüfen Sie außerdem die [Anweisungen für offline-Installationen](sql-server-linux-setup.md#offline).

1. **Kann ich eine unbeaufsichtigte Installation von SQL Server on Linux ausführen?**

   Ja. Eine Erläuterung der für die unbeaufsichtigte Installation, finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md#unattended). Finden Sie unter der Beispielskripts für [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), und [Ubuntu](sample-unattended-install-ubuntu.md). Sie können auch überprüfen, [dieses Beispielskript](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) erstellt, indem die SQL Server-Kundenberatungsteams.

## <a name="tools"></a>Tools

1. **Können ich die SQL Server Management Studio-Client unter Windows Sie SQL Server on Linux zugreifen?**

   Ja, können Sie Ihre vorhandenen Tools verwenden, die unter Windows den Zugriff auf SQL Server unter Linux ausgeführt werden. Dazu gehören Tools von Microsoft z. B. SQL Server Management Studio (SSMS), SQL Server Data Tools (SSDT) und Betriebssysteme und Drittanbieter-Tools.

1. **Gibt es ein Tool wie SSMS, die auf dem Linux ausgeführt wird?**

   Die neue Microsoft SQL Operations Studio (preview) ist eine plattformübergreifende-Tool zum Verwalten von SQL Server. Weitere Informationen finden Sie unter [Neuigkeiten von Microsoft SQL Operations Studio (Vorschau)](../sql-operations-studio/what-is.md).

1. **Sind Sie Befehle wie Sqlcmd und Bcp unter Linux verfügbar?**

   Ja, [Sqlcmd und Bcp](sql-server-linux-setup-tools.md) systemintern stehen unter Linux, Mac OS und Windows. Darüber hinaus verwenden Sie die neue [Mssql Skripter](https://github.com/Microsoft/mssql-scripter) Befehlszeilentool unter Linux, Mac OS oder Windows zum Generieren von T-SQL-Skripts für Ihre SQL-Datenbank, die überall ausführen. Siehe auch die Vorschau, um eine [Mssql-Cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/).

1. **Ist es möglich, Anzeigen von Aktivitätsmonitor, wenn für eine Instanz über SSMS unter Windows verbunden auf Linux werden ausgeführt?**

   Ja, Sie können SSMS unter Windows verwenden, um eine Remoteverbindung herstellen, und verwenden Extras / Funktionen, z. B. als Aktivitätsmonitor Befehle auf einem Linux-Instanzen.

1. **Welche Tools zum Überwachen der Leistung von SQL Server on Linux verfügbar sind?**

   Sie können [dynamische Verwaltungssichten (DMVs) für System](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) auf verschiedene Arten von Informationen zu SQL Server, einschließlich Linux Prozessinformationen zu sammeln. Sie können [Abfragespeicher](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) abfrageleistung zu verbessern. Andere Tools, z. B. die integrierten [Performance Dashboard](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/), funktioniert Remote in SQL Server Management Studio (SSMS) von Windows.

## <a name="administration"></a>Verwaltung

1. **Hat Microsoft eine app wie die SQL Server-Konfigurations-Manager unter Linux erstellt?**

   Ja, es wird ein Configuration Tool für SQL Server on Linux: [Mssql-Conf](sql-server-linux-configure-mssql-conf.md).

1. **Unterstützt SQL Server on Linux mehrere Instanzen auf demselben Host?**

   Es wird empfohlen, mehrere Container auf einem Host, mehrere unterschiedliche Instanzen ausgeführt. Jeder Container muss an einen anderen Port lauschen. Weitere Informationen finden Sie unter [führen Sie mehrere SQL Server-Container](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers).

1. **Werden Active Directory-Authentifizierung wird unter Linux unterstützt?**

   Ja. Weitere Informationen finden Sie unter [Active Directory-Authentifizierung mit SQL Server on Linux](sql-server-linux-active-directory-authentication.md).

1. **Befinden sich immer auf und unterstützt clustering unter Linux?**

   Failoverclustering und hohe Verfügbarkeit unter Linux werden mit Schrittmacher unter Linux erzielt. Weitere Informationen finden Sie unter [Business Continuity und Datenbank Wiederherstellung: SQL Server on Linux](sql-server-linux-business-continuity-dr.md).

1. **Ist es möglich, die Replikation von unter Linux, Windows und umgekehrt zu konfigurieren?**

   Skalieren von Lesevorgängen Replikate können für die unidirektionale Datenreplikation zwischen Windows- und Linux verwendet werden.

1. **Ist es möglich, vorhandene Datenbanken in früheren Versionen von SQL Server von Windows, Linux migrieren?**

   Ja, es gibt [mehrere Methoden](sql-server-linux-migrate-overview.md) dies zu erreichen.

1. **Kann ich meine Daten aus Oracle und andere Datenbankmodule, SQL Server on Linux migrieren?**

   Ja. SSMA unterstützt die Migration verschiedener Arten von Datenbankmodule: Microsoft Access, DB2, MySQL, Oracle und SAP ASE (früher SAP Sybase ASE). Ein Beispiel zum Verwenden von SSMA finden Sie unter [migrieren Sie eine Oracle-Schema zu SQL Server-2017 unter Linux mit SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json).

1. **Welche Berechtigungen sind erforderlich, damit SQL Server-Dateien?**

   Alle Dateien in der `/var/opt/mssql` Dateiordner sollten im Besitz der **Mssql** Benutzer und gehören zu den **Mssql** Gruppe. Sowohl die **Mssql** Benutzer- und Lese-/ Schreibberechtigungen für alle Dateien und Verzeichnisse verfügen. Beachten Sie die folgenden speziellen Szenarien im Zusammenhang mit Datei- und Verzeichnisberechtigungen aus:

   * Berechtigungen für Mssql-Besitzer und die Gruppe sind erforderlich, damit bereitgestellte Netzwerkfreigaben, die zum Speichern von SQL Server-Dateien verwendet werden.
   * Wenn Sie Datenbankdateien oder die Sicherungen in einem Nichtstandard-Verzeichnis gefunden haben, müssen Sie auch Berechtigungen für dieses Verzeichnis festlegen.
   * Wenn Sie die Standard-Stamm-Umask 0022 ändern, schlägt die SQL Server-Konfiguration nach der Installation fehl. Sie müssen dann manuell erforderliche Berechtigungen auf SQL Server-Startkonto anwenden.

1. **Kann ich den Besitz von SQL Server-Dateien und Verzeichnissen aus den installierten Mssql-Konto- und gruppenverwaltungsdetails ändern?**

   Wir unterstützen nicht den Besitz der SQL Server-Verzeichnisse und Dateien von der standardmäßigen Installation ändern. Der Mssql-Konto- und gruppenverwaltungsdetails speziell für SQL Server verwendet wird, und hat keinen Zugriff für die interaktive Anmeldung.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
