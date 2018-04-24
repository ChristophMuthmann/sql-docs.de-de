---
title: Warteschlangenlese-Agent der Microsoft SQL Server-Replikation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], Queue Reader Agent
- command prompt [SQL Server replication]
- Queue Reader Agent, parameter reference
- Queue Reader Agent, executables
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b71480a6229a5c1834c77b8d555017091835b76
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="replication-queue-reader-agent"></a>Warteschlangenlese-Agent der Microsoft SQL Server-Replikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Warteschlangenlese-Agent der Microsoft SQL Server-Replikation ist eine ausführbare Datei, die in einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Warteschlange oder einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] -Nachrichtenwarteschlange gespeicherte Nachrichten liest und diese Nachrichten dann auf den Verleger anwendet. Der Warteschlangenlese-Agent wird bei Momentaufnahme- und Transaktionsveröffentlichungen verwendet, die das verzögerte Update über eine Warteschlange gestatten.  
  
> [!NOTE]  
>  Parameter können in beliebiger Reihenfolge angegeben werden. Wenn keine optionalen Parameter angegeben werden, werden vordefinierte Werte auf Grundlage des Standardagentprofils verwendet.  
  
## <a name="syntax"></a>Syntax  
  
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
  
## <a name="arguments"></a>Argumente  
 **-?**  
 Zeigt Informationen zur Verwendung an.  
  
 **-Continuous**  
 Gibt an, ob der Agent fortlaufend versucht, Transaktionen in der Warteschlange zu verarbeiten. Wenn dieses Argument angegeben ist, setzt der Agent die Ausführung auch dann fort, wenn in der Warteschlange keine ausstehenden Transaktionen von einem der Abonnenten vorhanden sind.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 Der Pfad der Agentdefinitionsdatei. Eine Agentdefinitionsdatei enthält Befehlszeilenargumente für den Agent. Der Inhalt der Datei wird als ausführbare Datei analysiert. Verwenden Sie doppelte Anführungszeichen ("), um Argumentwerte anzugeben, die beliebige Zeichen enthalten.  
  
 **-Distributor** *Servername*[**\\***Instanzname*]  
 Der Name des Verteilers. Geben Sie *server_name* für die Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server an. Geben Sie *server_name*\\*instance_name* für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server an. Wenn kein Name angegeben wird, wird als Standardwert der Name der Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf dem lokalen Computer verwendet.  
  
 **-DistributionDB** *distribution_database*  
 Die Verteilungsdatenbank.  
  
 **-DistributorLogin** *distributor_login*  
 Der Anmeldename des Verteilers.  
  
 **-DistributorPassword** *distributor_password*  
 Das Verteilerkennwort.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Gibt den Sicherheitsmodus des Verteilers an. Der Wert **0** steht für den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierungsmodus (Standard), der Wert **1** für den Windows-Authentifizierungsmodus.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Die Ebene der SSL-Verschlüsselung (Secure Sockets Layer), die vom Warteschlangenlese-Agent beim Herstellen von Verbindungen verwendet wird.  
  
|Wert von EncryptionLevel|Description|  
|---------------------------|-----------------|  
|**0**|Gibt an, dass SSL nicht verwendet wird.|  
|**1**|Gibt an, dass SSL verwendet wird, der Agent jedoch nicht überprüft, ob das SSL-Serverzertifikat von einem vertrauenswürdigen Aussteller signiert wurde.|  
|**2**|Gibt an, dass SSL verwendet und das Zertifikat überprüft wird.|  
  
 Weitere Informationen finden Sie unter [Sicherheitsübersicht &#40;Replikation&#41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 Gibt den Umfang des Verlaufs an, der während eines Vorgangs des Warteschlangenlese-Agents protokolliert wird. Sie können die negativen Auswirkungen der Verlaufsprotokollierung auf die Leistung minimieren, indem Sie den Wert **1**auswählen.  
  
|Wert von <legacyBold>HistoryVerboseLevel</legacyBold>|Description|  
|-------------------------------|-----------------|  
|**0**|Keine Verlaufsprotokollierung (nicht empfohlen).|  
|**1**|Standard. Aktualisieren Sie immer eine vorherige Verlaufsmeldung mit dem gleichen Status (Start, Status, Erfolg usw.). Wenn kein vorheriger Datensatz mit dem gleichen Status vorhanden ist, fügen Sie einen neuen Datensatz ein.|  
|**2**|Fügen Sie neue Verlaufsdatensätze ein, einschließlich Leerlaufmeldungen oder Meldungen zu Aufträgen mit langer Ausführungszeit.|  
|**3**|Fügen Sie neue Verlaufsdatensätze ein, die weitere Details enthalten, die möglicherweise für die Problembehandlung nützlich sind.|  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Anmeldung eintritt. Der Standardwert ist 15 Sekunden.  
  
 **-Output** *output_path_and_file_name*  
 Der Pfad der Agentausgabedatei. Wenn kein Dateiname angegeben ist, wird die Ausgabe an die Konsole gesendet. Wenn eine Datei mit dem angegebenen Namen vorhanden ist, wird die Ausgabe an diese Datei angefügt.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Gibt an, ob die Ausgabe ausführlich sein soll. Wenn die Meldungsstufe **0**beträgt, werden nur Fehlermeldungen gedruckt. Wenn die Meldungsstufe **1**beträgt, werden alle Statusberichtsmeldungen gedruckt. Wenn die Meldungsstufe **2** (Standard) beträgt, werden alle Fehlermeldungen und Statusberichtsmeldungen gedruckt, was beim Debuggen nützlich ist.  
  
 **-PollingInterval** *polling_interval*  
 Ist nur relevant, um Abonnements zu aktualisieren, die auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] basierende Warteschlangen verwenden. Gibt an, wie oft die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Warteschlange nach anstehenden Transaktionen abgefragt wird (in Sekunden). Der Wert kann zwischen 0 und 240 Sekunden liegen. Die Standardeinstellung ist 5 Sekunden.  
  
 **-PublisherFailoverPartner** *Servername*[**\\***Instanzname*]  
 Gibt die Failoverpartnerinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an, die an einer Datenbank-Spiegelungssitzung mit der Veröffentlichungsdatenbank teilnimmt. Weitere Informationen finden Sie unter [Database Mirroring and Replication &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-ProfileName** *agent_profile_name*  
 Der Name eines Agentprofils, das zum Bereitstellen von Standardwerten an den Agent verwendet wird. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Abfrage eintritt. Die Standardeinstellung ist 1800 Sekunden.  
  
 **-ResolverState** [ **1**| **2**| **3**]  
 Gibt an, wie Konflikte bei verzögertem Update über eine Warteschlange gelöst werden. Der Wert **1** gibt an, dass der Verleger den Konflikt gewinnt und für die aktuelle Transaktion in der Warteschlage, bei der der Konflikt aufgetreten ist, auf dem Verleger und dem ursprünglichen Updateabonnenten ein Rollback ausgeführt wird. Die Verarbeitung der folgenden Transaktionen in der Warteschlange wird fortgesetzt. Der Wert **2** gibt an, dass der Abonnent den Konflikt gewinnt und durch die Transaktion in der Warteschlange die Werte auf dem Verleger überschrieben werden. Der Wert **3** gibt an, dass jeder Konflikt zu einer erneuten Initialisierung des Abonnenten führt. Der Verleger gewinnt den Konflikt, die Verarbeitung der folgenden Transaktionen in der Warteschlange wird beendet, und das Abonnement wird erneut initialisiert. Die Standardeinstellung für Transaktionsveröffentlichungen lautet **1** , für Momentaufnahmeveröffentlichungen **3** .  
  
## <a name="remarks"></a>Remarks  
 Führen Sie zum Starten des Warteschlangenlese-Agents von der Eingabeaufforderung **qrdrsvc.exe** aus. Informationen hierzu finden Sie im [Abschnitt zu den ausführbaren Dateien von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
