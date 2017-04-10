---
title: "Oracle CDC Service | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Oracle CDC Service
  Der Oracle CDC Service ist ein Windows-Dienst, der das Programm xdbcdcsvc.exe ausführt. Der Oracle CDC Service kann so konfiguriert werden, dass er mehrere Windows-Dienste auf demselben Computer ausführt, wobei jeder Dienst einen anderen Windows-Dienstnamen aufweist. Die Erstellung mehrerer Oracle CDC-Windows-Dienste auf einem Computer wird häufig angewendet, um eine bessere Trennung der einzelnen Dienste zu erzielen oder um zu ermöglichen, dass jeder Dienst mit einer anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz arbeitet.  
  
 Ein Oracle CDC Service wird mithilfe der Oracle CDC Service Configuration Console erstellt oder mit der in das Programm xdbcdcsvc.exe integrierten Befehlszeilenschnittstelle definiert. In beiden Fällen wird jeder erstellte Oracle CDC Service einer einzelnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zugeordnet (die gruppiert oder per **Always On**-Setup gespiegelt sein kann), und die Verbindungsinformationen (Verbindungszeichenfolge und Anmeldeinformationen für den Zugriff) sind Teil der Dienstkonfiguration.  
  
 Wenn ein Oracle CDC Service gestartet wird, versucht er, die folgenden Schritte auszuführen: Herstellen einer Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, der er zugeordnet ist, Abrufen der Liste der Oracle CDC-Instanzen, die er behandeln muss, und Durchführen einer ersten Überprüfung der Umgebung. Fehler während des Dienststarts und alle Informationen zum Starten und Beenden werden immer in das Windows-Anwendungsereignisprotokoll geschrieben. Wenn eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt wird, werden alle Fehler und Informationsmeldungen in die Tabelle **dbo.xdbcdc_trace** der MSXDBCDC-Datenbank für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz geschrieben. Bei einer der Überprüfungen, die während des Startvorgangs durchgeführt werden, wird sichergestellt, dass momentan kein anderer Oracle CDC Service mit dem gleichen Namen aktiv ist. Wenn für einen Dienst mit dem gleichen Namen momentan eine Verbindung von einem anderen Computer besteht, begibt sich der Oracle CDC Service in eine Warteschleife und wartet, bis der andere Dienst die Verbindung getrennt hat, bevor die Oracle CDC-Aufgaben ausgeführt werden.  
  
 Wenn der Oracle CDC Service alle Startüberprüfungen besteht, überprüft er die Tabelle **dbo.xdbcdc_databases** in der MSXDBCDC-Datenbank auf aktivierte Oracle CDC-Instanzen. Für jede aktivierte Oracle CDC-Instanz startet der Dienst einen Unterprozess zur Behandlung dieser Oracle CDC-Instanz.  
  
 Beim Starten einer Oracle CDC-Instanz greift diese auf die SQL Server CDC-Datenbank mit dem gleichen Namen wie die CDC-Instanz zu und ruft ihren Status aus der vorherigen Ausführung ab. Außerdem wird überprüft, ob alles ordnungsgemäß ausgeführt wird. Anschließend wird die Verarbeitung der Änderungen fortgesetzt. Das Lesen der Oracle-Transaktionsprotokolle und das Schreiben von Änderungen in die CDC-Datenbank wird durchgeführt.  
  
 Der Oracle CDC Service überprüft die Tabelle **dbo.xdbcdc_tables** in der MSXDBCDC-Datenbank in regelmäßigen Abständen, um zu ermitteln, ob an einer der Oracle CDC-Instanzkonfigurationen Konfigurationsänderungen vorgenommen wurden. Wenn eine Änderung gefunden wird, informiert der Oracle CDC Service die Oracle CDC-Instanz darüber, dass diese ihre Konfiguration auf Änderungen überprüfen sollte. Die meisten Konfigurationsänderungen, z. B. das Hinzufügen und Entfernen von Aufzeichnungsinstanzen, können angewendet werden, während die Oracle CDC-Instanz aktiviert ist. Bei den übrigen Änderungen muss die Oracle CDC-Instanz neu gestartet werden.  
  
 Beim Verwenden der Oracle CDC Designer Console werden Änderungen automatisch erkannt. Beim direkten Aktualisieren der Oracle CDC-Konfiguration mit SQL sollte die folgende Prozedur aufgerufen werden, damit der Oracle CDC Service die Konfigurationsänderung beachtet:  
  
```  
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 Der Oracle CDC-Instanzprozess aktualisiert seinen Status in der Systemtabelle **cdc.xdbcdc_state** und schreibt Fehlerinformationen in die Tabelle **cdc.xdbcdc_trace**. Die Tabelle **xdbcdc_state** ist nützlich für die Überwachung des Status der Oracle CDC-Instanz. Sie liefert den aktuellen Status und bietet verschiedene Leistungsindikatoren (z.B. die Anzahl der aus Oracle gelesenen Änderungen, die Anzahl der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geschriebenen Änderungen, die Anzahl der geschriebenen Transaktionen mit Commit und die aktuelle Anzahl der umgehend ausgeführten Transaktionen) und eine Anzeige der Latenzzeit.  
  
 Die Oracle CDC-Instanzkonfiguration wird in der Tabelle **cdc.xdbcdc_config** gespeichert. Dies ist die Tabelle, die von der Oracle CDC Designer Console verwendet wird. Da sich die gesamte Konfiguration einer Oracle CDC-Instanz auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz und in CDC-Datenbanken befindet, ist es möglich, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bereitstellungsskripts für eine Oracle CDC-Instanz zu erstellen. Dies wird mithilfe der CDC Service Configuration Console und Oracle CDC Designer Console erreicht.  
  
## Überlegungen zur Sicherheit  
 Im Folgenden werden die Sicherheitsanforderungen beschrieben, die für die Verwendung des CDC Service for Oracle erforderlich sind.  
  
### Schutz der Oracle-Quelldaten  
 Der Oracle CDC Service erfordert keinen Zugriff auf Oracle-Quelldaten und wird geschützt, indem sichergestellt wird, dass über die Log Mining-Anmeldeinformationen keine SELECT-Berechtigung für Oracle-Kundentabellen gewährt wird.  
  
### Schutz der Oracle-Quelländerungsdaten  
 Der Oracle CDC Service wird mit Log Mining-Anmeldeinformationen bereitgestellt, mit denen der Dienst Änderungen aufzeichnen kann, die an einer beliebigen Tabelle in der Oracle-Datenbank vorgenommen werden. Änderungsdaten verfügen nicht über die präzisen Zugriffsberechtigungen von normalen Tabellen. Daher werden die integrierten Oracle-Datenzugriffssteuerelemente beim Zugreifen auf Änderungsdaten umgangen.  
  
 Aufgezeichnete Oracle-Quelltabellen weisen leere Spiegeltabellen mit dem gleichen Schema und Tabellennamen in der CDC-Datenbank auf. Die aufgezeichneten Daten werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aufzeichnungsinstanzen gespeichert und bieten den gleichen Schutz wie bei Änderungen, die aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank aufgezeichnet wurden. Für den Zugriff auf die mit einer Änderungsinstanz verbundenen Änderungsdaten muss dem Benutzer die Zugriffsberechtigung für alle aufgezeichneten Spalten der zugeordneten Spiegeltabelle erteilt werden. Wenn bei Erstellung der Aufzeichnungsinstanz eine Gatingrolle angegeben wird, muss der Aufrufer außerdem Mitglied der angegebenen Gatingrolle sein. Andere allgemeine Change Data Capture-Funktionen für den Zugriff auf Metadaten stehen für alle Datenbankbenutzer mit der Rolle public zur Verfügung. Der Zugriff auf die zurückgegebenen Metadaten wird jedoch in der Regel auch hier durch die Zugriffsberechtigungen auf die zugrunde liegenden Quelltabellen und die Mitgliedschaft in definierten Gatingrollen beschränkt.  
  
 Dies bedeutet, dass Benutzer mit der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** (standardmäßig) Vollzugriff auf die aufgezeichneten Daten haben und dass der weiter gehende Zugriff entweder mithilfe von Gatingrollen oder durch das Gewähren des SELECT-Zugriffs auf die aufgezeichneten Spalten gewährt werden kann.  
  
### Schutz der Oracle-Log Mining-Anmeldeinformationen (Quelldaten)  
 Die in der CDC-Datenbank (in der Tabelle cdc.xdbcdc_config) gespeicherte Oracle CDC-Dienstkonfiguration schließt den Log Mining-Benutzernamen und das dazugehörige Kennwort ein.  
  
 Das Log Mining-Kennwort wird mithilfe eines asymmetrischen Schlüssels mit dem festen Namen `xdbcdc_asym_key` gespeichert, der mit dem folgenden Befehl automatisch erstellt wird:  
  
```  
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 Wenn ein anderer Algorithmus verwendet wird, kann dieser Schlüssel verworfen und ein neuer Schlüssel mit dem gleichen Namen und dem gleichen Verschlüsselungskennwort erstellt werden.  
  
 Das asymmetrische Schlüsselkennwort ist das Masterkennwort, das in der Registrierung unter dem Pfad **HKLM\Software\Microsoft\XDBCDCSVC\\<Dienstname>** gespeichert wird. Auf diesen Schlüssel können nur lokale Administratoren und das Oracle CDC-Windows-Dienst-Konto zugreifen. Der Schlüssel enthält einen verschlüsselten binären Wert **AsymmetricKeyPassword** , unter dem das Kennwort für den asymmetrischen Schlüssel gespeichert wird. Der Zugriff auf diesen Registrierungsschlüssel ist erforderlich, um auf die Oracle-Log Mining-Anmeldeinformationen zugreifen zu können.  
  
 Zum Verwenden der ENCRYPTION BY PASSWORD-Klausel muss das Kennwort die Anforderungen der Windows-Kennwortrichtlinien des Computers erfüllen, auf dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz ausgeführt wird. Wählen Sie dazu das Kennwort für den asymmetrischen Schlüssel gemäß dieser Richtlinie aus.  
  
 Wenn das Kennwort für den asymmetrischen Schlüssel verloren geht, müssen die Log Mining-Anmeldeinformationen für jede Oracle CDC-Instanz im Oracle CDC Service Designer erneut angegeben werden.  
  
 Der asymmetrische Schlüssel wird in der CDC-Datenbank automatisch erstellt, wenn der CDC-Dienst eine CDC-Datenbank der Oracle-Instanz erkennt, die nicht über diesen asymmetrischen Schlüssel verfügt, oder wenn der Schlüssel vorhanden ist, aber das Kennwort nicht übereinstimmt.  
  
### Windows-Dienstkonto für Oracle CDC Service  
 Das mit dem Oracle CDC-Windows-Dienst verwendete Dienstkonto erfordert keine zusätzlichen Berechtigungen. Dieses Konto muss in der Lage sein, sowohl die Oracle Native Client API als auch die SQL Server Native Client ODBC API zu verwenden. Es muss auch in der Lage sein, auf den Dienstkonfigurationsschlüssel in der Registrierung zuzugreifen (die CDC Service Configuration Console richtet die Zugriffssteuerungsliste (ACL) entsprechend ein).  
  
## In diesem Abschnitt  
  
-   [Unterstützung für hohe Verfügbarkeit](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [Für SQL Server-Verbindung erforderliche Berechtigungen für den CDC Service](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [Benutzerrollen](../../integration-services/change-data-capture/user-roles.md)  
  
-   [Arbeiten mit dem Oracle CDC Service](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## Siehe auch  
 [Verwalten eines lokalen CDC Service](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [Verwalten eines Oracle CDC Service](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  