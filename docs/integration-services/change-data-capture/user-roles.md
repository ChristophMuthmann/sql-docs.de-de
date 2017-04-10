---
title: "Benutzerrollen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Benutzerrollen
  In diesem Abschnitt werden die Benutzerrollen für den Change Data Capture Service für Oracle von Attunity beschrieben. Die beschriebenen Rollen sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankrollen, Windows-Rollen und Oracle-Datenbankrollen.  
  
## Windows-Benutzerrollen  
 Im Folgenden werden die vom Oracle CDC Service verwendeten Windows-Benutzerrollen beschrieben.  
  
### Computeradministrator: Oracle CDC Service  
 Der Computeradministrator ist ein Windows-Benutzer, der für das Erstellen und Verwalten des CDC Service auf dem Computer zuständig ist. Dieser Benutzer muss der Gruppe der lokalen Computeradministratoren angehören.  
  
 Zu den vom Oracle CDC Service-Computeradministrator ausgeführten Tasks gehört Folgendes:  
  
-   Installieren der CDC Service for Oracle-Software  
  
-   Erstellen eines Oracle CDC-Windows-Diensts  
  
-   Herstellen der CDC Service-Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zielinstanz (Verbindungszeichenfolge und Anmeldeinformationen)  
  
-   Sicherstellen, dass das CDC Service-Masterkennwort als Schutz für die Oracle-Log Mining-Anmeldeinformationen verwendet wird  
  
-   Löschen eines CDC Service-Windows-Diensts  
  
-   Deinstallieren der CDC Service for Oracle-Software  
  
-   Verwalten der CDC Service for Oracle-Software (z. B. Installation von Updates)  
  
-   Starten und Beenden eines CDC Service-Windows-Diensts  
  
 Beim Verwenden von Konfigurationen mit hoher Verfügbarkeit, z. B. Microsoft-Failovercluster, muss der Computeradministrator über zusätzliche Zuständigkeiten und Berechtigungen verfügen, z. B.:  
  
-   Installation und Wartung der CDC Service for Oracle-Software auf allen Clusterknoten.  
  
-   Definition von generischen Clusterdienstressourcen für den CDC Service-Windows-Dienst auf den verschiedenen Clusterknoten.  
  
-   Arbeit als Computeradministrator, der auf dem Computer, auf dem der CDC Service for Oracle installiert ist, als Administrator autorisiert ist. Diese Person installiert den CDC Service for Oracle und verwendet die CDC Service Configuration Console, um einen CDC Service for Oracle auf einem lokalen Computer zu konfigurieren.  
  
### Dienstkonto: Oracle CDC Service  
 Dieses Oracle CDC Service-Windows-Dienstkonto ist ein Windows-Konto, das zum Ausführen des Oracle CDC Service (das Dienstkonto) verwendet wird.  
  
 Die einzige Berechtigung für das Dienstkonto, die erforderlich ist, ist die Möglichkeit der Verwendung des Oracle-Clients und des systemeigenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Anbieters. Dieses Konto benötigt keinen Zugriff auf Dateien, es sei denn, dies ist für bestimmte Anbieter erforderlich (wenn z.B. die Verbindungszeichenfolge des Oracle-Clients auf Oracle-Datenbankinstanzen in der Datei **tnsnames.ora** verweist, muss das Dienstkonto für diese Datei über Lesezugriff verfügen).  
  
 Beim Erstellen eines Oracle CDC Service unter Windows Vista oder Windows Server 2008 ist das Standarddienstkonto das Konto NETZWERKDIENST.  
  
 Unter Windows 7 und Windows Server 2008 R2 und höher ist das Standarddienstkonto NT-Dienst\\<Dienstname>.  
  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem anderen Computer ausgeführt wird oder eine gruppierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz ist und der Dienst per Windows-Authentifizierung eine Verbindung zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ziel herstellen muss, sollte das Dienstkonto ein Domänenkonto sein.  
  
## SQL Server-Benutzerrollen  
 Im Folgenden werden die vom Oracle CDC Service verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzerrollen beschrieben.  
  
### Oracle CDC Service-Administrator  
 Der CDC-Dienstadministrator ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer mit vollständiger Kontrolle über die Oracle CDC Service-Artefakte auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz. Der CDC-Dienstadministrator verwendet die Oracle CDC Designer Console, um Oracle CDC-Instanzen zu entwerfen.  
  
 Dem CDC Service-Administrator sollten die festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Serverrollen **public** und **dbcreator**gewährt werden.  
  
 Zu den vom CDC Service-Administrator ausgeführten Tasks gehört Folgendes:  
  
-   Vorbereiten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz auf das Hosten von Oracle CDC-Instanzen (bei denen es sich um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken handelt) In diesem Task wird auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz eine spezielle Datenbank mit dem Namen MSXDBCDC erstellt.  
  
-   Erstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank für die Oracle CDC-Instanz Dieser Task beinhaltet das Aktivieren der neu erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank für CDC, wofür ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemadministrator (**sysadmin**) erforderlich ist.  
  
-   Entwerfen einer Oracle CDC-Instanz Dieser Task beinhaltet das Bereitstellen von Informationen zur Oracle-Quelldatenbank und zu aufgezeichneten Tabellen, wofür ein Oracle-Datenbankadministrator erforderlich ist.  
  
-   Pflegen der Oracle CDC-Instanz, z. B. Hinzufügen/Entfernen von Aufzeichnungsinstanzen und Aktualisieren der Konfiguration  
  
-   Aktivieren oder Deaktivieren einer Oracle CDC-Instanz  
  
-   Überwachen des Status einer Oracle CDC-Instanz  
  
-   Behandeln von Problemen, die sich auf die Oracle CDC-Instanz auswirken  
  
 Der CDC Service-Administrator ist, zumindest am Anfang, in der festen Datenbankrolle **db_owner** für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC-Datenbank der Oracle CDC-Instanz zugeordnet. So erhält der CDC Service-Administrator Zugriff auf die in der CDC-Datenbank gespeicherten Änderungsdaten. Nach der Erstellung kann die Rolle **db_owner** der CDC-Datenbank einem anderen Benutzer zugewiesen werden, der alle oben aufgeführten Tasks ausführen kann (mit Ausnahme der Vorbereitung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz und der Erstellung einer weiteren Oracle CDC-Instanz).  
  
 Der CDC Service-Administrator muss dabei nicht das Masterkennwort kennen, das bei der Erstellung des Oracle CDC-Windows-Diensts angegeben wurde.  
  
### Systemadministrator  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemadministrator ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer, dem die feste Serverrolle **sysadmin** für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gewährt werden sollte, die den Oracle CDC-Diensten zugeordnet ist.  
  
 Es ist nur ein Oracle CDC-spezifischer Task vorhanden, der über den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministrator ausgeführt wird. Dieser Task ist das Aktivieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank für eine Oracle CDC-Instanz für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Dieser Task wird beim Erstellen einer neuen Oracle CDC-Instanz mit der Oracle CDC Designer Console ausgeführt.  
  
### Oracle CDC Service-Benutzer  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC Service-Benutzer ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung, die vom Oracle CDC Service verwendet wird, um die Arbeitsschritte mit der MSXDBCDC-Datenbank und mit allen von diesem Dienst behandelten Oracle CDC-Instanzen (CDC-Datenbanken) durchzuführen.  
  
 Dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC Service-Benutzer sollte Folgendes gewährt werden:  
  
-   Mitglied der festen Datenbankrollen **db_dlladmin**, **db_datareader** und **db_datawriter** für alle CDC-Datenbanken, die vom Server behandelt werden.  
  
-   Mitglied der festen Datenbankrollen **db_datareader** und **db_datawriter** für die MSXDBCDC-Datenbank.  
  
 Da der Oracle CDC Service für die Verwendung aller CDC-Datenbanken und der MSXDBCDC-Datenbank eine einzelne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung verwendet, sollte diese Anmeldung in all diesen Datenbanken zugeordnet werden.  
  
### Oracle CDC Change Consumer  
 Der Oracle CDC Change Consumer ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer, der Änderungen nutzt, die in den CDC-Tabellen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC-Instanzdatenbank gespeichert sind.  
  
 Dieser Benutzer bestimmt die Benutzerrolle, die für den Zugriff auf die einzelnen CDC-Tabellen über die CDC-Funktionen erforderlich ist, die von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC-Infrastruktur generiert werden. Wenn beim Angeben einer Aufzeichnungsinstanz keine Benutzerrolle angegeben wird, ist der Zugriff auf die Änderungen auf das Mitglied der festen Datenbankrolle **db_owner** der CDC-Datenbank beschränkt.  
  
## Oracle-Benutzerrollen  
 Im Folgenden werden die vom Oracle CDC Service verwendeten Oracle-Benutzerrollen beschrieben.  
  
### Datenbankadministrator (DBA)  
 Der Oracle-Datenbankadministrator (DBA) ist ein Oracle-Datenbankbenutzer. Vom Oracle-Datenbankadministrator ausgeführte Tasks sind z. B.:  
  
-   Einrichten der Oracle-Quelldatenbank für die Arbeit im ARCHIVELOG-Modus  
  
-   Einrichten eines Log Mining-Benutzers mit den erforderlichen Berechtigungen  
  
-   Festlegen der ergänzenden Protokollierung für aufgezeichnete Tabellen  
  
-   Unterstützen der Wiederherstellung archivierter Transaktionsprotokolldateien, die nicht mehr verfügbar sind, um die Verarbeitung zu ermöglichen  
  
 Der Oracle-Datenbankadministrator kann Oracle SQL-Skripts abrufen, die ausgeführt werden müssen, damit diese vor dem Ausführen ausgewertet werden können. Der Oracle-Datenbankadministrator kann Oracle SQL-Skripts auch direkt über die Oracle CDC Designer Console ausführen.  
  
 Wenn der Oracle-Datenbankadministrator sich für die Verwendung der Oracle CDC Designer Console entscheidet, werden die Anmeldeinformationen des Administrators nicht beibehalten, mit Ausnahme des Kontexts (Dialogfeld), in dem sie verwendet wurden.  
  
 Der Oracle-Datenbankadministrator arbeitet in Abstimmung mit dem Oracle CDC Service-Administrator an der Konfiguration der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC-Instanzen.  
  
### Log Mining-Benutzer  
 Der Oracle Log Miner-Benutzer ist ein spezieller Oracle-Datenbankbenutzer, dem die erforderlichen Berechtigungen für den Zugriff auf und die Verarbeitung von Oracle-Transaktionsprotokollen gewährt werden.  
  
 Die Anmeldeinformationen für diesen Benutzer werden mithilfe der Verschlüsselung per asymmetrischem Schlüssel in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC-Instanzdatenbank gespeichert. Der Zugriff ist nur für den Oracle CDC Service möglich, nicht für den Besitzer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC-Instanzdatenbank.  
  
 In der folgenden Liste sind die erforderlichen Berechtigungen beschrieben, die dem Log Mining-Benutzer gewährt werden sollten:  
  
-   SELECT on \<beliebige-aufgezeichnete-tabelle>  
  
-   SELECT ANY TRANSACTION  
  
-   EXECUTE on DBMS_LOGMNR  
  
-   SELECT on V$LOGMNR_CONTENTS  
  
-   SELECT on V$ARCHIVED_LOG  
  
-   SELECT on V$LOG  
  
-   SELECT on V$LOGFILE  
  
-   SELECT on V$DATABASE  
  
-   SELECT on V$THREAD  
  
-   SELECT on ALL_INDEXES  
  
-   SELECT on ALL_OBJECTS  
  
-   SELECT on DBA_OBJECTS  
  
-   SELECT on ALL_TABLES  
  
 Wenn einem V$xxx einige dieser Berechtigungen nicht gewährt werden können, sollten sie V $xxx gewährt werden.  
  
### Schemabenutzer  
 Der Oracle-Schemabenutzer ist ein Oracle-Benutzer mit Lesezugriff auf das Schema der aufzuzeichnenden Oracle-Tabellen. Dieser Benutzer wird beim Verwenden der Oracle CDC Designer Console benötigt, um die Liste der Oracle-Schemas, aufzuzeichnende Tabellen und ihre Spalten, Indizes und Schlüssel abzurufen.  
  
 Die Anmeldeinformationen für diesen Benutzer werden nicht gespeichert. Sie werden von der CDC Designer Console jeweils angefordert, wenn sie benötigt werden, und dann für die restlichen Benutzeroberflächen-Sitzungen beibehalten.  
  
  