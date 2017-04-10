---
title: "Replikationsprotokolllese-Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protokolllese-Agent, ausführbare Dateien"
  - "Protokolllese-Agent, Parameterreferenz"
  - "Agents [SQL Server-Replikation], Protokolllese-Agent"
  - "Eingabeaufforderung [SQL Server-Replikation]"
ms.assetid: 5487b645-d99b-454c-8bd2-aff470709a0e
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# Replikationsprotokolllese-Agent
  Der Replikationsprotokolllese-Agent ist eine ausführbare Datei, die das Transaktionsprotokoll jeder für die Transaktionsreplikation konfigurierten Datenbank überwacht und die für die Replikation markierten Transaktionen aus dem Transaktionsprotokoll in die Verteilungsdatenbank kopiert.  
  
> [!NOTE]  
>  Parameter können in beliebiger Reihenfolge angegeben werden. Wenn keine optionalen Parameter angegeben werden, werden vordefinierte Werte auf Grundlage des Standardagentprofils verwendet.  
  
## Syntax  
  
```  
  
logread [-?]   
-Publisher server_name[\instance_name]   
-PublisherDB publisher_database   
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-HistoryVerboseLevel [0|1|2]]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-LogScanThreshold scan_threshold]  
[-MaxCmdsInTran number_of_commands]  
[-MessageInterval message_interval]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2|3|4]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]   
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherSecurityMode [0|1]]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-QueryTimeOut query_time_out_seconds]  
[-ReadBatchSize number_of_transactions]   
[-ReadBatchThreshold read_batch_threshold]  
[-RecoverFromDataErrors]  
```  
  
## Argumente  
 **-?**  
 Zeigt Informationen zur Verwendung an.  
  
 **-Publisher** *Servername*[**\\***Instance_name*]  
 Der Name des Verlegers. Geben Sie *Servername* für die Standardinstanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server. Geben Sie *Servername***\\***Instance_name* für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server.  
  
 **-PublisherDB** *Verlegerdatenbank*  
 Der Name der Verlegerdatenbank.  
  
 **-Continuous**  
 Gibt an, ob der Agent fortlaufend versucht, replizierte Transaktionen abzurufen. Wenn dieses Argument angegeben ist, ruft der Agent replizierte Transaktionen in festgelegten Abrufintervallen aus der Quelle ab, selbst wenn keine ausstehenden Transaktionen vorhanden sind.  
  
 **-DefinitionFile** *PfadUndNameDerDefinitionsdatei*  
 Der Pfad der Agentdefinitionsdatei. Eine Agentdefinitionsdatei enthält Befehlszeilenargumente für den Agent. Der Inhalt der Datei wird als ausführbare Datei analysiert. Verwenden Sie doppelte Anführungszeichen ("), um Argumentwerte anzugeben, die beliebige Zeichen enthalten.  
  
 **-Verteiler** *Servername*[**\\***Instance_name*]  
 Der Name des Verteilers. Geben Sie *Servername* für die Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server. Geben Sie *Servername***\\***Instance_name* für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server.  
  
 **--DistributorLogin** *Distributor_login*  
 Der Anmeldename des Verteilers.  
  
 **-DistributorPassword** *Distributor_password*  
 Das Verteilerkennwort.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Gibt den Sicherheitsmodus des Verteilers an. Wert **0** gibt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierungsmodus (Standard) und den Wert **1** gibt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Authentifizierungsmodus.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Die Ebene der SSL-Verschlüsselung (Secure Sockets Layer), die vom Protokolllese-Agent beim Herstellen von Verbindungen verwendet wird.  
  
|Wert von EncryptionLevel|Beschreibung|  
|---------------------------|-----------------|  
|**0**|Gibt an, dass SSL nicht verwendet wird.|  
|**1**|Gibt an, dass SSL verwendet wird, der Agent jedoch nicht überprüft, ob das SSL-Serverzertifikat von einem vertrauenswürdigen Aussteller signiert wurde.|  
|**2**|Gibt an, dass SSL verwendet und das Zertifikat überprüft wird.|  
  
 Weitere Informationen finden Sie unter [Sicherheitsübersicht & #40; Replikation und #41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-ExtendedEventConfigFile** *Configuration_path_and_file_name*  
 Gibt den Pfad und den Dateinamen für die erweiterte Ereignis-XML-Konfigurationsdatei an. Die erweiterten Ereignis-Konfigurationsdatei ermöglicht das Konfigurieren von Sitzungen und das Aktivieren der Nachverfolgung für Ereignisse.  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**]  
 Gibt den Umfang des Verlaufs an, der während eines Vorgangs des Protokolllese-Agents protokolliert wird. Sie können die negativen Auswirkungen der Verlaufsprotokollierung auf die Leistung minimieren, indem Sie den Wert **1**auswählen.  
  
|Wert von <legacyBold>HistoryVerboseLevel</legacyBold>|Beschreibung|  
|-------------------------------|-----------------|  
|**0**||  
|**1**|Standard. Aktualisieren Sie immer eine vorherige Verlaufsmeldung mit dem gleichen Status (Start, Status, Erfolg usw.). Wenn kein vorheriger Datensatz mit dem gleichen Status vorhanden ist, fügen Sie einen neuen Datensatz ein.|  
|**2**|Fügen Sie neue Verlaufsdatensätze ein, es sei denn, der Datensatz bezieht sich z. B. auf Leerlaufmeldungen oder Meldungen zu Aufträgen mit langer Ausführungszeit. In diesen Fällen aktualisieren Sie die vorherigen Datensätze.|  
  
 **-KeepAliveMessageInterval** *Keep_alive_message_interval_seconds*  
 Die Anzahl von Sekunden, bevor vom Verlaufsthread geprüft wird, ob bestehende Verbindungen auf eine Antwort vom Server warten. Dieser Wert kann verringert werden, damit der Protokolllese-Agent vom Überprüfungs-Agent nicht als fehlerverdächtig markiert wird, wenn ein lang andauernder Batch ausgeführt wird. Der Standardwert ist 300 Sekunden.  
  
 **-LoginTimeOut** *Login_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Anmeldung eintritt. Der Standardwert ist 15 Sekunden.  
  
 **-LogScanThreshold** *Scan_threshold*  
 Nur interne Verwendung.  
  
 **-MaxCmdsInTran** *Number_of_commands*  
 Gibt die maximale Anzahl von Anweisungen an, die in einer Transaktion zusammengefasst werden, wenn der Protokolllese-Agent Befehle in die Verteilungsdatenbank schreibt. Mithilfe dieses Parameters können der Protokolllese-Agent und der Verteilungs-Agent beim Anwenden auf dem Abonnenten umfangreiche Transaktionen (die aus zahlreichen Befehlen bestehen) auf dem Verleger in mehrere kleinere Transaktionen aufteilen. Durch die Angabe dieses Parameters kommt es auf dem Verteiler möglicherweise zu weniger Konflikten, und die Latenzzeit zwischen Verleger und Abonnent kann reduziert werden. Da die ursprüngliche Transaktion in kleineren Einheiten angewendet wird, kann der Abonnent vor Ende der ursprünglichen Transaktion auf Zeilen einer umfangreichen logischen Verleger-Transaktion zugreifen; dies widerspricht der strikten Unteilbarkeit von Transaktionen. **0**ist der Standardwert, durch den die Transaktionsgrenzen des Verlegers beibehalten werden.  
  
> [!NOTE]  
>  Für Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Veröffentlichungen wird dieser Parameter ignoriert. Weitere Informationen finden Sie im Abschnitt "Konfigurieren des Transaktionssatz-Auftrags" unter [Performance Tuning for Oracle Publishers](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
 **-MessageInterval** *Message_interval*  
 Das für die Verlaufsprotokollierung verwendete Zeitintervall. Wenn nach der Protokollierung des letzten Verlaufsereignisses der Wert von **MessageInterval** erreicht wird, wird erneut ein Verlaufsereignis protokolliert.  
  
 Wenn an der Quelle keine replizierte Transaktion vorhanden ist, sendet der Agent eine entsprechende Meldung an den Verteiler. Mit dieser Option wird angegeben, wie lange der Agent wartet, bevor eine weitere Meldung gesendet wird, dass keine Transaktion vorhanden ist. Agents melden immer, dass keine Transaktion vorhanden ist, wenn sie feststellen, dass an der Quelle keine Transaktionen verfügbar sind, nachdem zuvor replizierte Transaktionen verarbeitet wurden. Der Standardwert ist 60 Sekunden.  
  
 **-Ausgabe** *Output_path_and_file_name*  
 Der Pfad der Agentausgabedatei. Wenn kein Dateiname angegeben ist, wird die Ausgabe an die Konsole gesendet. Wenn eine Datei mit dem angegebenen Namen vorhanden ist, wird die Ausgabe an diese Datei angefügt.  
  
 **' - OutputVerboseLevel '** [ **0**| **1**| **2** | **3** | **4** ]  
 Gibt an, ob die Ausgabe ausführlich sein soll.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Nur Fehlermeldungen werden gedruckt.|  
|**1**|Alle Agent-Statusberichtsmeldungen werden gedruckt.|  
|**2** (Standard)|Alle Fehlermeldungen und Agent-Statusberichtsmeldungen werden gedruckt.|  
|**3**|Die ersten 100 Bytes jedes replizierten Befehls werden gedruckt.|  
|**4**|Alle replizierten Befehle werden gedruckt.|  
  
 Die Werte 2-4 sind beim Debuggen hilfreich.  
  
 **-PacketSize** *Paketgröße*  
 Die Paketgröße in Bytes. Der Standardwert ist 4096 (Bytes).  
  
 **PollingInterval -** *Polling_interval*  
 Gibt an, wie häufig replizierte Transaktionen aus dem Protokoll abgefragt werden (in Sekunden). Die Standardeinstellung ist 5 Sekunden.  
  
 **-ProfileName** *Profile_name*  
 Gibt ein Agentprofil an, das für Agentparameter verwendet werden soll. Wenn **ProfileName** den Wert NULL aufweist, wird das Agentprofil deaktiviert. Wenn **ProfileName** nicht angegeben ist, wird das Standardprofil für den Agenttyp verwendet. Weitere Informationen finden Sie unter [Replikations-Agentprofile](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **PublisherFailoverPartner -** *Servername*[**\\***Instance_name*]  
 Gibt die Failoverpartnerinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an, die an einer Datenbank-Spiegelungssitzung mit der Veröffentlichungsdatenbank teilnimmt. Weitere Informationen finden Sie unter [Datenbankspiegelung und Replikation & #40; SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Gibt den Sicherheitsmodus des Verlegers an. Der Wert **0** gibt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung (Standard) und einem Wert von **1** Windows-Authentifizierungsmodus.  
  
 **--PublisherLogin** *Publisher_login*  
 Der Anmeldename des Verlegers.  
  
 **-PublisherPassword** *Publisher_password*  
 Das Kennwort des Verlegers.  
  
 **QueryTimeOut -** *Query_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Abfrage eintritt. Die Standardeinstellung ist 1800 Sekunden.  
  
 **-ReadBatchSize** *Number_of_transactions*  
 Die maximale Anzahl von Transaktionen, die pro Verarbeitungszyklus aus dem Transaktionsprotokoll der Veröffentlichungsdatenbank ausgelesen werden. Der Standardwert lautet 500. Der Agent setzt das Lesen von Transaktionen in Batches fort, bis alle Transaktionen aus dem Protokoll gelesen wurden. Der Parameter wird von Oracle-Verlegern nicht unterstützt.  
  
 **-ReadBatchThreshold** *Number_of_commands*  
 Die Anzahl von Replikationsbefehlen, die aus dem Transaktionsprotokoll gelesen werden sollen, bevor sie vom Verteilungs-Agent an den Abonnenten ausgegeben werden. Die Standardeinstellung ist 0. Wenn dieser Parameter nicht angegeben wird, liest der Protokolllese-Agent an das Ende des Protokolls bzw. der Zahl **- ReadBatchSize** (Anzahl der Transaktionen).  
  
 **-RecoverFromDataErrors**  
 Gibt an, dass der Protokolllese-Agent weiter ausgeführt wird, wenn in Spaltendaten, die von einem Nicht-SQL Server-Verleger veröffentlicht wurden, Fehler auftreten. Standardmäßig bewirken solche Fehler, dass der Protokolllese-Agent fehlschlägt. Bei Verwendung **- RecoverFromDataErrors**, fehlerhafte Spaltendaten entweder als NULL oder einen entsprechenden Wert ungleich NULL repliziert und Fehlermeldungen werden protokolliert, um die [MSlogreader_history](../../../relational-databases/system-tables/mslogreader-history-transact-sql.md) Tabelle. Der Parameter wird nur von Oracle-Verlegern unterstützt.  
  
## Hinweise  
  
> [!IMPORTANT]  
>  Wenn Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Agent so installiert haben, dass er unter einem lokalen Systemkonto und nicht unter einem Domänenbenutzerkonto (Standard) ausgeführt wird, kann der Dienst nur auf den lokalen Computer zugreifen. Wenn der Protokolllese-Agent, der unter dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent ausgeführt wird, so konfiguriert ist, dass beim Anmelden bei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]der Windows-Authentifizierungsmodus verwendet wird, schlägt der Protokolllese-Agent fehl. Die Standardeinstellung ist die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung. Weitere Informationen zum Ändern von Sicherheitskonten finden Sie unter [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Führen Sie zum Starten des Protokolllese-Agents von der Eingabeaufforderung **logread.exe** aus. Weitere Informationen finden Sie unter [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Hinzugefügt der **- ExtendedEventConfigFile** Parameter.|  
  
## Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  