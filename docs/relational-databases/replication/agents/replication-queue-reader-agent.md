---
title: "Warteschlangenlese-Agent der Microsoft SQL Server-Replikation | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agents [SQL Server-Replikation], Warteschlangenlese-Agent"
  - "Eingabeaufforderung [SQL Server-Replikation]"
  - "Warteschlangenlese-Agent, Parameterreferenz"
  - "Warteschlangenlese-Agent, ausführbare Dateien"
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Warteschlangenlese-Agent der Microsoft SQL Server-Replikation
  Der Warteschlangenlese-Agent der Microsoft SQL Server-Replikation ist eine ausführbare Datei, die in einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Warteschlange oder einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] -Nachrichtenwarteschlange gespeicherte Nachrichten liest und diese Nachrichten dann auf den Verleger anwendet. Der Warteschlangenlese-Agent wird bei Momentaufnahme- und Transaktionsveröffentlichungen verwendet, die das verzögerte Update über eine Warteschlange gestatten.  
  
> [!NOTE]  
>  Parameter können in beliebiger Reihenfolge angegeben werden. Wenn keine optionalen Parameter angegeben werden, werden vordefinierte Werte auf Grundlage des Standardagentprofils verwendet.  
  
## Syntax  
  
```  
  
qrdrsvc [-?]  
[-Continuous]  
[-DefinitionFile definition_file]  
[-Distributor server_name[\instance_name]]  
[-DistributionDB distribution_database]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-LoginTimeOut login_time_out_seconds]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PollingInterval polling_interval]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-ProfileName agent_profile_name]  
[-QueryTimeOut query_time_out_seconds]  
[-ResolverState [1|2|3]]  
```  
  
## Argumente  
 **-?**  
 Zeigt Informationen zur Verwendung an.  
  
 **-Continuous**  
 Gibt an, ob der Agent fortlaufend versucht, Transaktionen in der Warteschlange zu verarbeiten. Wenn dieses Argument angegeben ist, setzt der Agent die Ausführung auch dann fort, wenn in der Warteschlange keine ausstehenden Transaktionen von einem der Abonnenten vorhanden sind.  
  
 **-DefinitionFile** *PfadUndNameDerDefinitionsdatei*  
 Der Pfad der Agentdefinitionsdatei. Eine Agentdefinitionsdatei enthält Befehlszeilenargumente für den Agent. Der Inhalt der Datei wird als ausführbare Datei analysiert. Verwenden Sie doppelte Anführungszeichen ("), um Argumentwerte anzugeben, die beliebige Zeichen enthalten.  
  
 **-Verteiler** *Servername*[**\\***Instance_name*]  
 Der Name des Verteilers. Geben Sie *Servername* für die Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server. Geben Sie *Servername*\\*Instance_name* für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server. Wenn kein Name angegeben wird, wird als Standardwert der Name der Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf dem lokalen Computer verwendet.  
  
 **-DistributionDB** *Distribution_database*  
 Die Verteilungsdatenbank.  
  
 **--DistributorLogin** *Distributor_login*  
 Der Anmeldename des Verteilers.  
  
 **-DistributorPassword** *Distributor_password*  
 Das Verteilerkennwort.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Gibt den Sicherheitsmodus des Verteilers an. Der Wert **0** gibt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierungsmodus (Standard) und den Wert **1** Windows-Authentifizierungsmodus.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Die Ebene der SSL-Verschlüsselung (Secure Sockets Layer), die vom Warteschlangenlese-Agent beim Herstellen von Verbindungen verwendet wird.  
  
|Wert von EncryptionLevel|Beschreibung|  
|---------------------------|-----------------|  
|**0**|Gibt an, dass SSL nicht verwendet wird.|  
|**1**|Gibt an, dass SSL verwendet wird, der Agent jedoch nicht überprüft, ob das SSL-Serverzertifikat von einem vertrauenswürdigen Aussteller signiert wurde.|  
|**2**|Gibt an, dass SSL verwendet und das Zertifikat überprüft wird.|  
  
 Weitere Informationen finden Sie unter [Sicherheitsübersicht & #40; Replikation und #41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 Gibt den Umfang des Verlaufs an, der während eines Vorgangs des Warteschlangenlese-Agents protokolliert wird. Sie können die negativen Auswirkungen der Verlaufsprotokollierung auf die Leistung minimieren, indem Sie den Wert **1**auswählen.  
  
|Wert von <legacyBold>HistoryVerboseLevel</legacyBold>|Beschreibung|  
|-------------------------------|-----------------|  
|**0**|Keine Verlaufsprotokollierung (nicht empfohlen).|  
|**1**|Standard. Aktualisieren Sie immer eine vorherige Verlaufsmeldung mit dem gleichen Status (Start, Status, Erfolg usw.). Wenn kein vorheriger Datensatz mit dem gleichen Status vorhanden ist, fügen Sie einen neuen Datensatz ein.|  
|**2**|Fügen Sie neue Verlaufsdatensätze ein, einschließlich Leerlaufmeldungen oder Meldungen zu Aufträgen mit langer Ausführungszeit.|  
|**3**|Fügen Sie neue Verlaufsdatensätze ein, die weitere Details enthalten, die möglicherweise für die Problembehandlung nützlich sind.|  
  
 **-LoginTimeOut** *Login_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Anmeldung eintritt. Der Standardwert ist 15 Sekunden.  
  
 **-Ausgabe** *Output_path_and_file_name*  
 Der Pfad der Agentausgabedatei. Wenn kein Dateiname angegeben ist, wird die Ausgabe an die Konsole gesendet. Wenn eine Datei mit dem angegebenen Namen vorhanden ist, wird die Ausgabe an diese Datei angefügt.  
  
 **' - OutputVerboseLevel '** [ **0**| **1**| **2**]  
 Gibt an, ob die Ausgabe ausführlich sein soll. Wenn die Meldungsstufe **0**beträgt, werden nur Fehlermeldungen gedruckt. Wenn die Meldungsstufe **1**beträgt, werden alle Statusberichtsmeldungen gedruckt. Wenn die Meldungsstufe **2** (Standard), alle Fehlermeldungen und statusberichtsmeldungen werden gedruckt, die beim Debuggen nützlich ist.  
  
 **PollingInterval -** *Polling_interval*  
 Ist nur relevant, um Abonnements zu aktualisieren, die auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] basierende Warteschlangen verwenden. Gibt an, wie oft die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Warteschlange nach anstehenden Transaktionen abgefragt wird (in Sekunden). Der Wert kann zwischen 0 und 240 Sekunden liegen. Die Standardeinstellung ist 5 Sekunden.  
  
 **PublisherFailoverPartner -** *Servername*[**\\***Instance_name*]  
 Gibt die Failoverpartnerinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an, die an einer Datenbank-Spiegelungssitzung mit der Veröffentlichungsdatenbank teilnimmt. Weitere Informationen finden Sie unter [Datenbankspiegelung und Replikation & #40; SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-ProfileName** *Agent_profile_name*  
 Der Name eines Agentprofils, das zum Bereitstellen von Standardwerten an den Agent verwendet wird. Weitere Informationen finden Sie unter [Replikations-Agentprofile](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **QueryTimeOut -** *Query_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Abfrage eintritt. Die Standardeinstellung ist 1800 Sekunden.  
  
 **ResolverState -** [ **1**| **2**| **3**]  
 Gibt an, wie Konflikte bei verzögertem Update über eine Warteschlange gelöst werden. Der Wert **1** gibt an, dass der Verleger den Konflikt gewinnt und für die aktuelle Transaktion in der Warteschlage, bei der der Konflikt aufgetreten ist, auf dem Verleger und dem ursprünglichen Updateabonnenten ein Rollback ausgeführt wird. Die Verarbeitung der folgenden Transaktionen in der Warteschlange wird fortgesetzt. Der Wert **2** gibt an, dass der Abonnent den Konflikt gewinnt und durch die Transaktion in der Warteschlange die Werte auf dem Verleger überschrieben werden. Der Wert **3** Gibt an, dass jeder Konflikt zum erneuten Initialisierung des Abonnenten führt, der Verleger den Konflikt gewinnt, Verarbeitung der nachfolgenden Transaktionen in der Warteschlange beendet wird und das Abonnement erneut initialisiert werden wird. Die Standardeinstellung für Transaktionsveröffentlichungen lautet **1** , für Momentaufnahmeveröffentlichungen **3** .  
  
## Hinweise  
 Führen Sie zum Starten des Warteschlangenlese-Agents von der Eingabeaufforderung **qrdrsvc.exe** aus. Informationen hierzu finden Sie im [Abschnitt zu den ausführbaren Dateien von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  