---
title: Lokale Überwachung für Feedbackerfassung zur SQL Server-Nutzung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Local Audit
ms.assetid: a0665916-7789-4f94-9086-879275802cf3
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f69dfadfb4de412794beba72f69b22fdc8a39287
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="local-audit-for-sql-server-usage-feedback-collection"></a>Lokale Überwachung für Feedbackerfassung zur SQL Server-Nutzung

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="introduction"></a>Einführung

Microsoft SQL Server enthält internetfähige Funktionen, die Daten über Ihren Computer oder Ihr Gerät („Standardcomputerinformationen“) erfassen und an Microsoft senden können. Die Komponente „Lokale Überwachung“ der [Feedbackerfassung zur SQL Server-Nutzung](http://support.microsoft.com/kb/3153756) schreibt die vom Dienst erfassten Daten, die die an Microsoft zu sendenden Daten (Protokolle) darstellen, in einen bestimmten Ordner. Der Zweck der lokalen Überwachung besteht darin, dass es Benutzern gestattet wird, alle Daten hinsichtlich Zustimmung, behördlicher Bestimmungen oder aus Datenschutzgründen anzuzeigen, die Microsoft mithilfe dieses Features erfasst.  

Seit SQL Server 2016 CU2 kann die lokale Überwachung auf Instanzebene für SQL Server-Datenbankmodul und Analysis Services (SSAS) konfiguriert werden. In SQL Server 2016 CU4 und SQL Server 2016 SP1 ist die lokale Überwachung auch für SQL Server Integration Services (SSIS) aktiviert. Andere SQL Server-Komponenten, die beim Setup installiert werden, und SQL Server-Tools, die nach dem Setup heruntergeladen oder installiert werden, verfügen für die Feedbackerfassung hinsichtlich der Nutzung nicht über die Funktion zur lokalen Überwachung. 

## <a name="prerequisites"></a>Voraussetzungen 

Nachfolgend sind die erforderlichen Komponenten zum Aktivieren der lokalen Überwachung auf jeder SQL Server-Instanz aufgeführt: 

1. Die Instanz wird auf SQL Server 2016 RTM CU2 oder höher gepatcht. 

1. Benutzer muss ein Systemadministrator oder eine Rolle mit Zugriff zum Hinzufügen und Ändern von Registrierungsschlüsseln, Erstellen von Ordnern, Verwalten der Ordnersicherheit und Beenden/Starten eines Windows-Diensts sein.  

## <a name="pre-configuration-steps-prior-to-turning-on-local-audit"></a>Vorkonfigurationsschritte vor der Aktivierung der lokalen Überwachung 

Bevor Sie die lokale Überwachung aktivieren, muss ein Systemadministrator die folgenden Schritte ausführen:

1. Er muss den SQL Server-Instanznamen und das Anmeldekonto für den SQL Server CEIP-Telemetriedienst kennen. 

1. Er muss einen neuen Ordner für die Dateien der lokalen Überwachung konfigurieren.

1. Er muss dem Anmeldekonto für den SQL Server CEIP-Telemetriedienst die entsprechenden Berechtigungen erteilen.

1. Er muss eine Registrierungsschlüsseleinstellung erstellen, um das Zielverzeichnis für die lokale Überwachung zu konfigurieren. 

    Er muss für das Datenbankmodul und für Integration Services den Schlüssel unter *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANZNAME\>\\CPE* erstellen. 
    
    Er muss für Analysis Services den Schlüssel unter *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANZNAME\>\\CPE* erstellen.

### <a name="get-the-sql-server-ceip-service-logon-account"></a>Abrufen des Anmeldekontos für den SQL Server CEIP-Dienst

Führen Sie die folgenden Schritte aus, um das Anmeldekonto für den SQL Server CEIP-Telemetriedienst abzurufen:
 
1. Starten Sie **Dienste** , klicken Sie auf die **Windows**  -Schaltfläche, und geben Sie *services.msc*ein. 

2. Navigieren Sie zu dem entsprechenden Dienst. Suchen Sie z. B. für das Datenbankmodul nach **SQL Server CEIP-Dienst \<Instanzname\>**erstellen. Suchen Sie für Analysis Services nach **SQL Server Analysis Services CEIP \<Instanzname\>**. Suchen Sie für Integration Services **SQL Server Integration Services-CEIP-Dienst 13**.

3. Klicken Sie mit der rechten Maustaste auf den Dienst, und wählen Sie **Eigenschaften**aus. 

4. Klicken Sie auf die Registerkarte **Anmelden** . Das Anmeldekonto wird in **Dieses Konto**aufgelistet. 

### <a name="configure-a-new-folder-for-the-local-audit-files"></a>Er muss einen neuen Ordner für die Dateien der lokalen Überwachung konfigurieren.    

Erstellen Sie einen neuen Ordner (Verzeichnis für die lokale Überwachung), in das die lokale Überwachung die Protokolle schreiben wird. Der vollständige Pfad zum Verzeichnis der lokalen Überwachung für eine Standardinstanz des Datenbankmoduls wäre beispielsweise: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*. 
 
> Hinweis: Konfigurieren Sie den Verzeichnispfad für die lokale Überwachung außerhalb des SQL Server-Installationspfads, um zu vermeiden, dass die Überwachungsfunktionen und das Patchen zu potenziellen Problemen mit SQL Server führen.

  ||Entwurfsentscheidung|Empfehlung|  
  |------|-----------------|----------|  
  |![Kontrollkästchen](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Kontrollkästchen")|Speicherplatzverfügbarkeit |Planen Sie für mittlere Arbeitsauslastungen mit ungefähr 10 Datenbanken ca. 2 MB an Speicherplatz pro Tag und Instanz ein.|  
|![Kontrollkästchen](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Kontrollkästchen")|Separate Verzeichnisse | Erstellen sie für jede Instanz ein Verzeichnis. Verwenden Sie z. B. *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* für eine SQL Server-Instanz namens `MSSQLSERVER`. Dies vereinfacht die Dateiverwaltung.
|![Kontrollkästchen](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Kontrollkästchen")|Separate Ordner |Verwenden Sie für jeden Dienst einen bestimmten Ordner. Verwenden Sie z. B. für einen angegebenen Instanznamen einen Ordner für das Datenbankmodul. Wenn eine Instanz von SSAS denselben Instanznamen verwendet, erstellen Sie einen separaten Ordner für SSAS. Wenn sowohl Instanzen für Datenbankmodul und Analysis Services für denselben Ordner konfiguriert sind, führt dies dazu, dass die lokale Überwachung für beide Instanzen in dieselbe Protokolldatei schreibt.| 
|![Kontrollkästchen](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Kontrollkästchen")|Erteilen von Berechtigungen für das Anmeldekonto für den SQL Server CEIP-Telemetriedienst|Aktivieren des Zugriffs für **Ordnerinhalt auflisten**, **Lesen** und **Schreiben** für das Anmeldekonto für den SQL Server CEIP-Telemetriedienst|


### <a name="grant-permissions-to-the-sql-server-ciep-telemetry-service-logon-account"></a>Erteilen von Berechtigungen für das Anmeldekonto für den SQL Server CEIP-Telemetriedienst
  
1. Navigieren Sie in **Datei-Explorer**zum Speicherort, in dem sich der neue Ordner befindet.  

1. Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie **Eigenschaften**aus. 

1. Klicken Sie auf der Registerkarte **Sicherheit**auf **Bearbeiten** und dann auf „Berechtigung verwalten“.

1. Klicken Sie auf **Hinzufügen** und geben Sie die Anmeldeinformationen für den SQL Server CEIP-Telemetriedienst ein, z. B. `NT Service\SQLTELEMETRY`.   

1. Klicken Sie auf **Namen überprüfen** , um den bereitgestellten Namen zu überprüfen, und klicken Sie dann auf **OK**. 

1. Wählen Sie im Dialogfeld **Berechtigung** das Anmeldekonto für den SQL Server CEIP-Telemetriedienst aus, und klicken Sie auf **Ordnerinhalt auflisten**, **Lesen** und **Schreiben**.  

1. Klicken Sie auf **OK** , um die Berechtigungsänderungen sofort anzuwenden. 
  
### <a name="create-a-registry-key-setting-to-configure-local-audit-target-directory"></a>Er muss eine Registrierungsschlüsseleinstellung erstellen, um das Zielverzeichnis für die lokale Überwachung zu konfigurieren.

1. Starten Sie „regedit“.  

1. Navigieren Sie zu dem entsprechenden CPE-Pfad. 

    Verwenden Sie für das Datenbankmodul und Integration Services *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANZNAME\>\\CPE*. 
    
    Verwenden Sie für Analysis Services *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANZNAME\>\\CPE*.

1. Klicken Sie im mit der rechten Maustaste auf den CPE-Pfad, und wählen Sie dann **Neu**aus. Klicken Sie auf **Zeichenfolgenwert**.

1. Benennen Sie den neuen Registrierungsschlüssel `UserRequestedLocalAuditDirectory`. 
 
## <a name="turning-local-audit-on-or-off"></a>Aktivieren oder Deaktivieren der lokalen Überwachung

Nachdem Sie die Schritte zur Vorkonfiguration abgeschlossen haben, können Sie die lokale Überwachung aktivieren. Verwenden Sie dazu ein Systemadministratorkonto oder eine ähnliche Rolle mit Zugriff zum Ändern von Registrierungsschlüsseln, um die lokale Überwachung mithilfe der folgenden Schritte zu aktivieren oder zu deaktivieren. 

1. Starten Sie **regedit**.  

1. Navigieren Sie zu dem entsprechenden CPE-Pfad. 

    Verwenden Sie für das Datenbankmodul und Integration Services *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANZNAME\>\\CPE*. 
    
    Verwenden Sie für Analysis Services *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANZNAME\>\\CPE*.

1. Klicken Sie mit der rechten Maustaste auf **UserRequestedLocalAuditDirectory** , und klicken Sie dann auf *Ändern*. 

1. Geben Sie den Pfad für die lokale Überwachung ein, um diese zu aktivieren. Beispiel: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*.
 
    Leeren Sie den Wert in **UserRequestedLocalAuditDirectory**, um die lokale Überwachung zu deaktivieren.

1. Schließen Sie **regedit**. 

SQL Server CEIP sollte die Einstellung für die lokale Überwachung sofort erkennen, wenn der Dienst bereits ausgeführt wird. Um den SQL Server CEIP-Dienst zu starten, kann ein Systemadministrator oder eine Person mit Zugriff zum Starten oder Beenden von Windows-Diensten die folgenden Schritte ausführen: 

1. Starten Sie „Dienste“, indem Sie auf die Windows-Schaltfläche klicken und „Dienste“ eingeben. 

1. Navigieren Sie zu dem entsprechenden Dienst. 

    Für das Datenbankmodul verwenden Sie **SQL Server CEIP-Dienst (\<INSTANZNAME\>)**. 
    
    Für Analysis Services verwenden Sie **SQL Server Analysis Services CEIP (\<INSTANZNAME\>)**. 

1. Klicken Sie mit der rechten Maustaste auf den Dienst, und wählen Sie „Neu starten“ aus. 

1. Vergewissern Sie sich, dass der Dienst den Status **Wird ausgeführt**aufweist. 

Die lokale Überwachung generiert eine Protokolldatei pro Tag. Die Protokolldateien erhalten Dateinamen im Format `<YYYY-MM-DD>.json`. Beispiel: *2016-07-12.json*. Wenn für den Tag im ausgewählten Verzeichnis eine Datei vorhanden ist, werden die Einträge von der lokalen Überwachung an die Datei angehängt. Andernfalls wird für den Tag eine neue Datei erstellt. 

> Hinweis: Nach der Aktivierung der lokalen Überwachung kann es bis zu fünf Minuten dauern, bis die Protokolldatei zum ersten Mal geschrieben wird. 

## <a name="maintenance"></a>Verwaltung 

1. Um die Nutzung von Speicherplatz beim Schreiben von Dateien durch die lokale Überwachung einzuschränken, richten Sie eine Richtlinie oder einen regulären Auftrag ein, um das Verzeichnis für die lokale Überwachung zu bereinigen, damit ältere, überflüssige Dateien entfernt werden.  

2. Schützen Sie das Verzeichnis der lokalen Überwachung, sodass nur entsprechende Personen darauf zugreifen können. Beachten Sie, dass die Protokolldateien Informationen enthalten, die in [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756)erläutert werden. Der entsprechende Zugriff auf diese Datei sollte die meisten Personen in Ihrem Unternehmen daran hindern, die Datei zu lesen.  

## <a name="data-dictionary-of-local-audit-output-data-structure"></a>Datenwörterbuch für die Ausgabedatenstruktur der lokalen Überwachung 

- Die Protokolldateien der lokalen Überwachung besitzen das JSON-Format, enthalten einen Satz von Objekten (Zeilen), die Datenpunkte darstellen, die zu **emitTime**an Microsoft gesendet werden.  

- Jede Zeile entspricht einem bestimmten Schema, das durch **schemaVersion**identifiziert wird.   

- Jede Zeile stellt eine Ausgabe einer SQLCEIP-Dienstsitzung dar, die als **sessionID**identifiziert wird.  

- Zeilen werden in Folge ausgegeben und durch **sequence**identifiziert. 

- Jede Datenpunktzeile enthält die Ausgabe für ein **queryIdentifier** , wobei es sich um eine T-SQL-Abfrage, eine XE-Sitzung oder eine handeln kann, die mit einer Art von Ablaufverfolgung verknüpft ist, die als **traceName**identifiziert wird.   

- **queryIdentifiers** werden zusammen mit **querySetVersion**gruppiert und erhalten eine Versionsangabe. 

- **data** enthält die Ausgabe der entsprechenden Abfrageausführung, die **queryTimeInTicks**benötigt hat. 

- Für**queryIdentifiers** für T-SQL-Abfragen ist die T-SQL-Abfragedefinition in der Abfrage gespeichert. 


| Logische Informationshierarchie für die lokale Überwachung | Verbundene Spalten |
| ------ | -------|
| Header | emitTime, schemaVersion 
| Computer | hostname, domainHash, sqmID, operatingSystem 
| Instanz | instanceName, correlationID, clientVersion 
| Session | sessionID, traceName 
| Dataseteigenschaften | sequence, querySetVersion, queryIdentifier, query, queryTimeInTicks 
| data |  data 

### <a name="namevalue-pairs-definition-and-examples"></a>Definition und Beispiele für Name-Wert-Paare 

Die nachfolgend aufgeführten Spalten stellen die Reihenfolge für die Dateiausgabe der lokalen Überwachung dar. Unidirektionaler Hash mit SHA-256 dient zum anonymisieren von Werten für eine Reihe der nachfolgenden Spalten.  

| Name | Description | Beispielwerte
|-------|--------| ----------|
|hostname | Anonymisierter Computername, auf dem SQL Server installiert ist| de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11 
|domainHash| Anonymisierter Domänenhash des Computers, der die SQL Server-Instanz hostet | de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11 
|sqmId |Bezeichner für den Computer, auf dem SQL Server installiert ist | 02AF58F5-753A-429C-96CD-3900E90DB990 
|INSTANCENAME| Anonymisierter SQL Server-Instanzname| e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855 
|schemaVersion| Schemaversion von SQLCEIP |  3 
|emitTime |Ausgabezeit für Datenpunkt in UTC | 2016-09-08T17:20:22.1124269Z 
|sessionID | Sitzungsbezeichner für SQLCEIP-Dienst | 89decf9a-ad11-485c-94a7-fefb3a02ed86 
| correlationId | Platzhalter für einen zusätzlichen Bezeichner | 0 
|sequence | Sequenznummer der Datenpunkte, die innerhalb der Sitzung gesendet wurden | 15 
| clientVersion | SQL Server-Instanzversion | 13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223) 
| operatingSystem | Betriebssystemversion, auf der die SQL Server-Instanz installiert ist | Microsoft Windows Server 2012 R2 Datacenter 
| querySetVersion | Version einer Gruppe von Abfragedefinitionen | 1.0.0.0 
|traceName | Ablaufverfolgungskategorien: (SQLServerXeQueries, SQLServerPeriodicQueries, SQLServerOneSettingsException) | SQLServerPeriodicQueries 
|queryIdentifier | Ein Bezeichner der Abfrage | SQLServerProperties.002 
|data   | Die Ausgabe der für queryIdentifier erfassten Informationen als Ausgabe einer T-SQL-Abfrage, XE-Sitzung oder der Anwendung |   [{"Collation": "SQL_Latin1_General_CP1_CI_AS","SqlFTinstalled": "0" "SqlIntSec": "1","IsSingleUser": "0","SqlFilestreamMode": "0","SqlPbInstalled": "0","SqlPbNodeRole": "","SqlVersionMajor": "13","SqlVersionMinor": "0","SqlVersionBuild": "2161","ProductBuildType": "","ProductLevel": "RTM","ProductUpdateLevel": "CU2","ProductUpdateReference": "KB3182270","ProductRevision": "3","SQLEditionId": "-1534726760","IsClustered": "0","IsHadrEnabled": "0","SqlAdvAInstalled": "0","PacketReceived": "1210","Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-Bit) unter Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"}],
|Abfrage| Die auf queryIdentifier bezogene T-SQL-Abfragedefinition, die Daten erzeugt, falls zutreffend.        Diese Komponente wird nicht vom SQL Server CEIP-Dienst hochgeladen. Sie ist in der lokalen Überwachung nur als Referenz für Kunden enthalten.| SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version
|queryTimeInTicks | Die Dauer zum Ausführen der Abfrage mit der folgenden Ablaufverfolgungskategorie: (SQLServerXeQueries, SQLServerPeriodicQueries) |  0 
 
### <a name="trace-categories"></a>Ablaufverfolgungskategorien 
Derzeit werden die folgenden Ablaufverfolgungskategorien erfasst: 

- **SQLServerXeQueries**: Enthält Datenpunkte, die über die Sitzung für erweiterte Ereignisse erfasst wurden. 

- **SQLServerPeriodicQueries**: Enthält Datenpunkte, die über regelmäßige Abfragen erfasst werden, die in einer SQL Server-Instanz ausgeführt werden. 

- **SQLServerPerDBPeriodicQueries**: Enthält Datenpunkte, die über regelmäßige Abfragen erfasst werden, die in einer SQL Server-Instanz für bis zu 30 Datenbanken ausgeführt werden. 

- **SQLServerOneSettingsException**: Enthält Ausnahmenachrichten hinsichtlich der Aktualisierung von Schema- und/oder Abfragesätzen. 

- **DigitalProductID**: Enthält Datenpunkte zum Aggregieren anonymisierter (SHA-256) digitaler Produkt-IDs mit Hash von SQL Server-Instanzen. 

### <a name="local-audit-file-examples"></a>Dateibeispiele für die lokale Überwachung



Es folgt ein Auszug aus einer JSON-Dateiausgabe der lokalen Überwachung.

```JSON
{
    "hostName": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "domainHash": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "sqmId": "02AF58F5-753A-429C-96CD-3900E90DB990",
    "instanceName": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
    "schemaVersion": "3",
    "emitTime": "2016-09-08T17:20:22.1124269Z",
    "sessionId": "89decf9a-ad11-485c-94a7-fefb3a02ed86",
    "correlationId": 0,
    "sequence": 15,
    "clientVersion": "13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223)",
    "operatingSystem": "Microsoft Windows Server 2012 R2 Datacenter",
    "querySetVersion": "1.0.0.0",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "SQLServerProperties.002",
    "data": [
      {
        "Collation": "SQL_Latin1_General_CP1_CI_AS",
        "SqlFTinstalled": "0",
        "SqlIntSec": "1",
        "IsSingleUser": "0",
        "SqlFilestreamMode": "0",
        "SqlPbInstalled": "0",
        "SqlPbNodeRole": "",
        "SqlVersionMajor": "13",
        "SqlVersionMinor": "0",
        "SqlVersionBuild": "2161",
        "ProductBuildType": "",
        "ProductLevel": "RTM",
        "ProductUpdateLevel": "CU2",
        "ProductUpdateReference": "KB3182270",
        "ProductRevision": "3",
        "SQLEditionId": "-1534726760",
        "IsClustered": "0",
        "IsHadrEnabled": "0",
        "SqlAdvAInstalled": "0",
        "PacketReceived": "1210",
        "Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"
      }
    ],
    "query": "SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version",
    "queryTimeInTicks": 0
  } ,
  {
    "hostName": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "domainHash": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "sqmId": "02AF58F5-753A-429C-96CD-3900E90DB990",
    "instanceName": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
    "schemaVersion": "3",
    "emitTime": "2016-09-08T17:20:24.9819144Z",
    "sessionId": "89decf9a-ad11-485c-94a7-fefb3a02ed86",
    "correlationId": 0,
    "sequence": 61,
    "clientVersion": "13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223)",
    "operatingSystem": "Microsoft Windows Server 2012 R2 Datacenter",
    "querySetVersion": "1.0.0.0",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "ExternalScriptStats.001",
    "data": [
      {
        "counter_name": "Total Executions                                                                                                                ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Parallel Executions                                                                                                             ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Streaming Executions                                                                                                            ",
        "cntr_value": "0"
      },
      {
        "counter_name": "SQL CC Executions                                                                                                               ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Implied Auth. Logins                                                                                                            ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Total Execution Time (ms)                                                                                                       ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Execution Errors                                                                                                                ",
        "cntr_value": "0"
      }
    ],  
    "query": "select counter_name, cntr_value from sys.dm_os_performance_counters where object_name like \u0027%External Scripts%\u0027",
    "queryTimeInTicks": 155834
  } 
```
## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

**Wie lesen DBAs die Protokolldateien der lokalen Überwachung?**
Diese Protokolldateien werden im JSON-Format geschrieben. Jede Zeile ist ein JSON-Objekt, das eine Telemetriekomponente darstellt, die zu Microsoft hochgeladen wird. Die Feldnamen sollten selbsterklärend sein. 

**Was geschieht, wenn der DBA die Feedbackerfassung hinsichtlich der Nutzung deaktiviert?**
Es wird keine Datei für die lokale Überwachung geschrieben. 

**Was geschieht, wenn keine Verbindung mit dem Internet besteht bzw. der Computer sich hinter der Firewall befindet?**
Das Feedback zur Nutzung von SQL Server 2016 wird nicht an Microsoft gesendet. Es wird weiterhin versucht, die Protokolle der lokalen Überwachung zu schreiben, wenn dies ordnungsgemäß konfiguriert wurde.

**Wie deaktivieren DBAs die lokale Überwachung?**
Entfernen Sie den Registrierungsschlüsseleintrag „UserRequestedLocalAuditDirectory“.

**Wer kann die Protokolldateien der lokalen Überwachung lesen?**
Jeder in Ihrem Unternehmen mit Zugriff auf das Verzeichnis für die lokale Überwachung.

**Wie verwalten DBAs die Protokolldateien, die in das vorgesehene Verzeichnis geschrieben werden?**
Das Bereinigen der Dateien im Verzeichnis muss von den Datenbankadministratoren selbst verwaltet werden, damit die Verwendung von zu viel Speicherplatz vermieden wird.

**Gibt es einen Client oder ein Tool, mit dem diese JSON-Ausgabe gelesen werden kann?**
Die Ausgabe kann mit Editor, Visual Studio oder einem beliebigen JSON-Reader gelesen werden.
Alternativ können Sie die JSON-Datei lesen und die Daten in einer Instanz von SQL Server 2016 analysieren, wie unten dargestellt. Weitere Informationen zum Lesen von JSON-Datei in SQL Server finden Sie unter [Importieren von JSON-Dateien in SQL Server mithilfe von OPENROWSET (BULK) und OPENJSON (Transact-SQL)](http://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/10/07/bulk-importing-json-files-into-sql-server/).

```Transact-SQL
DECLARE @JSONFile AS VARCHAR(MAX)

-- Read the JSON file into variable 
SELECT @JSONFile = BulkColumn 
FROM OPENROWSET (BULK 'C:\SQLCEIPAudit\MSSQLSERVER\2016-09-08.json', SINGLE_CLOB) MyFile 

-- Check if the JSON file has been read properly and if it's in a JSON format
SELECT 
    @JSONFile LocalAuditOutput, 
    ISJSON(@JSONFile) IsFileInJSONFormat

-- Get the query identifier, query and the data (output of the query)   
SELECT 
    sequence,
    queryIdentifier,
    query,
    data
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON)
-- Get specific details about the output of "DatabaseProperties.001" query  
SELECT 
    QueryIdentifier,
    DatabaseID,
    CompatibilityLevel,
    IsQueryStoreOn
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON) 
    CROSS APPLY OPENJSON(data) 
        WITH (   DatabaseID varchar(128) '$.database_id'
                ,CompatibilityLevel varchar(128) '$.compatibility_level'
                ,IsQueryStoreOn varchar(128) '$.QS'
             )
WHERE queryIdentifier = 'DatabaseProperties.001'
```

## <a name="see-also"></a>Weitere Informationen finden Sie unter
[Lokale Überwachung für Feedbackerfassung zur SSMS-Nutzung](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-telemetry-ssms)

