# [About SQL Server on Linux (Informationen zu SQL Server unter Linux)](sql-server-linux-overview.md)

# Übersicht
## [Versionsanmerkungen](sql-server-linux-release-notes.md)
## [What's new in this release? (Neuerungen in dieser Version)](sql-server-linux-whats-new.md)
## [New and recently updated articles (Neue und kürzlich aktualisierte Artikel)](new-updated-linux.md)
## [Editionen und unterstützte Funktionen](sql-server-linux-editions-and-components-2017.md)

# Schnellstarts
## [Install & Connect - Red Hat (Installieren und Verbinden – Red Hat)](quickstart-install-connect-red-hat.md)
## [Install & Connect - SUSE (Installieren und Verbinden – SUSE)](quickstart-install-connect-suse.md)
## [Install & Connect - Ubuntu ((Installieren und Verbinden – Ubuntu)](quickstart-install-connect-ubuntu.md)
## [Run & Connect - Docker (Ausführen und Verbinden – Docker)](quickstart-install-connect-docker.md)
## [Provision a SQL VM in Azure (Bereitstellen einer SQL-VM in Azure)](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

# Lernprogramme
## [1_Migration von Windows](sql-server-linux-migrate-restore-database.md)
## [2_Migration von Oracle](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)
## [3_Migration zu Docker](tutorial-restore-backup-in-sql-server-container.md)
## [4_Erstellen eines Auftrags](sql-server-linux-run-sql-server-agent-job.md)
## [5_AD-Authentifizierung einrichten](sql-server-linux-active-directory-authentication.md)
## [6_Erstellen einer Failoverclusterinstanz](sql-server-linux-shared-disk-cluster-configure.md)
### [iSCSI](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
### [NFS](sql-server-linux-shared-disk-cluster-configure-nfs.md)
### [SMB](sql-server-linux-shared-disk-cluster-configure-smb.md)

# Konzepte
## Install
### [Installieren von SQL Server](sql-server-linux-setup.md)
### [Install SQL Server tools (Installieren von SQL Server-Tools)](sql-server-linux-setup-tools.md)
### [Install SQL Server Agent (Installieren des SQL Server-Agents)](sql-server-linux-setup-sql-agent.md)
### [Install SQL Server Full-Text Search (Installieren der SQL Server-Volltextsuche)](sql-server-linux-setup-full-text-search.md)
### [Install SQL Server Integration Services (Installieren von SQL Server Integration Services)](sql-server-linux-setup-ssis.md)
### [Registrieren des GA-Repositorys](sql-server-linux-change-repo.md)

## Konfigurieren
### [Configure with mssql-conf (Konfigurieren mit mssql-conf)](sql-server-linux-configure-mssql-conf.md)
### [Environment variables (Umgebungsvariablen)](sql-server-linux-configure-environment-variables.md)
### [Konfigurieren von Docker-Containern](sql-server-linux-configure-docker.md)
### [Customer Feedback (Kundenfeedback)](sql-server-linux-customer-feedback.md)

## [Entwickeln](sql-server-linux-develop-overview.md)
### [Connectivity libraries (Verbindungsbibliotheken)](sql-server-linux-develop-connectivity-libraries.md)
### [Use Visual Studio Code (Verwenden von Visual Studio Code)](sql-server-linux-develop-use-vscode.md)
### [Verwenden von SSMS](sql-server-linux-develop-use-ssms.md)
### [Use SSDT (Verwenden von SSDT)](sql-server-linux-develop-use-ssdt.md)

## [Verwalten](sql-server-linux-management-overview.md)
### [Use SSMS to manage (Verwenden von SSMS zum Verwalten)](sql-server-linux-manage-ssms.md)
### [Use PowerShell to manage (Verwenden von PowerShell zum Verwalten)](sql-server-linux-manage-powershell.md)
### [Use log shipping (Verwenden von Protokollversand)](sql-server-linux-use-log-shipping.md)
### [Use DB Mail and email alerts (Verwenden von DB-Mails und E-Mail-Warnungen)](sql-server-linux-db-mail-sql-agent.md)

## [Migrieren](sql-server-linux-migrate-overview.md)
### [Export and import a BACPAC from Windows (Exportieren und Importieren einer BACPAC-Datei von Windows)](sql-server-linux-migrate-ssms.md)
### [Migrate with SQL Server Migration Assistant (Migrieren mit SQL Server Migration Assistant)](sql-server-linux-migrate-ssma.md)
### [Bulk copy with bcp (Massenkopieren mit bcp)](sql-server-linux-migrate-bcp.md)

## [Extrahieren, Transformieren, Laden](sql-server-linux-migrate-ssis.md)
### [Einschränkungen und bekannte Probleme](sql-server-linux-ssis-known-issues.md)
### [Konfigurieren von SSIS](sql-server-linux-configure-ssis.md)
### [Zeitliches Planen von SSIS-Paketen](sql-server-linux-schedule-ssis-packages.md)

## [Configure Business Continuity (Konfigurieren des Geschäftskontinuität)](sql-server-linux-business-continuity-dr.md)
### [Backup and Restore (Sichern und Wiederherstellen)](sql-server-linux-backup-and-restore-database.md)
#### [Virtual Device Interface - Linux (Virtuelle Geräteschnittstelle – Linux)](sql-server-linux-backup-vdi-specification.md)
### [Failover Cluster Instance (Failoverclusterinstanz)](sql-server-linux-shared-disk-cluster-concepts.md)
#### [Red Hat Enterprise Linux]()
##### [Configure (HA add-on) (Konfigurieren (HA-Add-on))](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)
##### [Operate (HA add-on) (Ausführen (HA-Add-on))](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
#### [SUSE Linux Enterprise Server]()
##### [Configure (HA add-on) (Konfigurieren (HA-Add-on))](sql-server-linux-shared-disk-cluster-sles-configure.md)
### [Availability Groups (Verfügbarkeitsgruppen)](sql-server-linux-availability-group-overview.md)
#### [Create for high availability (Erstellen für Hochverfügbarkeit)](sql-server-linux-availability-group-ha.md)
##### [Configure AG (Konfigurieren von AG)](sql-server-linux-availability-group-configure-ha.md)
##### [Configure on RHEL (Konfigurieren unter RHEL)](sql-server-linux-availability-group-cluster-rhel.md)
##### [Configure on SUSE (Konfigurieren unter SUSE)](sql-server-linux-availability-group-cluster-sles.md)
##### [Configure on Ubuntu (Konfigurieren unter Ubuntu)](sql-server-linux-availability-group-cluster-ubuntu.md)
##### [Operate (Ausführen)](sql-server-linux-availability-group-failover-ha.md)
#### [Create for read scale-out only (Nur für die schreibgeschützte horizontale Skalierung erstellen)]()
##### [Configure AG (Konfigurieren von AG)](sql-server-linux-availability-group-configure-rs.md)

## [Sicherheit](sql-server-linux-security-overview.md)
### [Get started with security features (Erste Schritte mit den Sicherheitsfeatures)](sql-server-linux-security-get-started.md)
### [Encrypting Connections (Verschlüsseln von Verbindungen)](sql-server-linux-encrypted-connections.md)

## Leistung
### [Bewährte Methoden](sql-server-linux-performance-best-practices.md)
### [Erste Schritte mit Leistungsfeatures](sql-server-linux-performance-get-started.md)

# Beispiele
## Unbeaufsichtigtes Installieren
### [Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
### [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)
### [Ubuntu](sample-unattended-install-ubuntu.md)

# Ressourcen
## [Problembehandlung](sql-server-linux-troubleshooting-guide.md)
## [SQL Server Documentation (SQL Server-Dokumentation)](../sql-server/sql-server-technical-documentation.md)
## Partner
### [Überwachung](../sql-server/partner-monitor-sql-server.md)
### [Hochverfügbarkeit und Notfallwiederherstellung](../sql-server/partner-hadr-sql-server.md)
### [Verwaltung](../sql-server/partner-management-sql-server.md)
### [Entwicklung](../sql-server/partner-dev-sql-server.md)
## [DBA Stack Exchange (DBA-Stapelaustausch)](https://dba.stackexchange.com/questions/tagged/sql-server)
## [Stack Overflow (Stapelüberlauf)](http://stackoverflow.com/questions/tagged/sql-server)
## [MSDN-Foren](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
## [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)
## [Reddit](https://www.reddit.com/r/SQLServer)
