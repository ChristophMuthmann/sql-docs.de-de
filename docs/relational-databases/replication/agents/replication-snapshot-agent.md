---
title: "Replikationsmomentaufnahme-Agent | Microsoft Docs"
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
  - "Momentaufnahme-Agent, ausführbare Dateien"
  - "Agents [SQL Server-Replikation], Momentaufnahme-Agent"
  - "Eingabeaufforderung [SQL Server-Replikation]"
  - "Momentaufnahme-Agent, Parameterreferenz"
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Replikationsmomentaufnahme-Agent
  Der Replikationsmomentaufnahme-Agent ist eine ausführbare Datei, die Momentaufnahmedateien vorbereitet, die das Schema und die Daten von veröffentlichten Tabellen und Datenbankobjekten enthalten, die Dateien im Momentaufnahmeordner speichert und Synchronisierungsaufträge in der Verteilungsdatenbank aufzeichnet.  
  
> [!NOTE]  
>  Parameter können in beliebiger Reihenfolge angegeben werden.  
  
## Syntax  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## Argumente  
 **-?**  
 Druckt alle verfügbaren Parameter.  
  
 **-Publisher**  *Servername*[**\\***Instance_name*]    
 Der Name des Verlegers. Geben Sie Server_name für die Standardinstanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server. Geben Sie *Servername***\\***Instance_name* für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server.  
  
 **-Veröffentlichung** *Veröffentlichung*  
 Der Name der Veröffentlichung. Dieser Parameter ist nur gültig, wenn die Veröffentlichung so festgelegt ist, dass sie immer eine Momentaufnahme für neue oder neu initialisierte Abonnements zur Verfügung hat.  
  
 **-70Subscribers**  
 Muss verwendet werden, wenn alle Abonnenten ausführen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Version 7.0.  
  
 **-BcpBatchSize** *Bcp*_ *Batch*\_ *Größe*  
 Die Anzahl von Zeilen, die in einem Massenkopiervorgang gesendet werden sollen. Bei Ausführung eines **bcp in** -Vorgangs entspricht die Batchgröße der Anzahl von Zeilen, die als eine Transaktion an den Server gesendet werden sollen, und ebenso der Anzahl von Zeilen, die gesendet werden müssen, bevor der Verteilungs-Agent eine **bcp** -Statusmeldung protokolliert. Beim Durchführen einer **Bcp out** Vorgang, eine feste Batchgröße von 1000 verwendet wird. Durch den Wert 0 wird angezeigt, dass keine Meldungsprotokollierung ausgeführt wird.  
  
 **-DefinitionFile** *PfadUndNameDerDefinitionsdatei*  
 Der Pfad der Agentdefinitionsdatei. Eine Agentdefinitionsdatei enthält Befehlszeilenargumente für den Agent. Der Inhalt der Datei wird als ausführbare Datei analysiert. Verwenden Sie doppelte Anführungszeichen ("), um Argumentwerte anzugeben, die beliebige Zeichen enthalten.  
  
 **-Verteiler** *Servername*[**\\***Instance_name*]  
 Der Name des Verteilers. Geben Sie *Servername* für die Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server. Geben Sie *Servername***\\***Instance_name* für eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf diesem Server.  
  
 **Von DistributorDeadlockPriority -** [**-1**|**0**|**1**]  
 Die Priorität der Momentaufnahme-Agent-Verbindung mit dem Verteiler, wenn ein Deadlock auftritt. Dieser Parameter wird angegeben, um Deadlocks zu beheben, die möglicherweise während der Momentaufnahmegenerierung zwischen dem Momentaufnahme-Agent und Benutzeranwendungen auftreten.  
  
|Wert von DistributorDeadlockPriority|Beschreibung|  
|---------------------------------------|-----------------|  
|**-1**|Bei Auftreten eines Deadlocks auf dem Verteiler haben andere Anwendungen als der Momentaufnahme-Agent Priorität.|  
|**0** (Standard)|Es wird keine Priorität zugewiesen.|  
|**1**|Bei Auftreten eines Deadlocks auf dem Verteiler hat der Momentaufnahme-Agent Priorität.|  
  
 **--DistributorLogin** *Distributor_login*  
 Der Anmeldename, der verwendet wird, um mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung eine Verbindung mit dem Verteiler herzustellen.  
  
 **-DistributorPassword** *Distributor_password*  
 Das Kennwort, das verwendet wird, um mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung eine Verbindung mit dem Verteiler herzustellen. .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Gibt den Sicherheitsmodus des Verteilers an. Der Wert **0** gibt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierungsmodus (Standard) und den Wert **1** Windows-Authentifizierungsmodus.  
  
 **-DynamicFilterHostName** *Dynamic_filter_host_name*  
 Wird verwendet, um einen Wert für [HOST_NAME & #40; Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md) in Filtern, wenn eine dynamische Momentaufnahme wird erstellt. Beispielsweise, wenn die Teilmengenfilterklausel `rep_id = HOST_NAME()` für einen Artikel angegeben ist, und legen Sie die **DynamicFilterHostName** -Eigenschaft auf "fbjones"festlegen, bevor Sie den Merge-Agent nur Zeilen mit "FBJones" in der **Rep_id** Spalte repliziert wird.  
  
 **-DynamicFilterLogin** *Dynamic_filter_login*  
 Wird verwendet, um einen Wert für [SUSER_SNAME & #40; Transact-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)in Filtern, wenn eine dynamische Momentaufnahme wird erstellt. Beispielsweise, wenn die Teilmengenfilterklausel `user_id = SUSER_SNAME()` für einen Artikel angegeben ist und legen Sie die **DynamicFilterLogin** -Eigenschaft auf "Rsmith" vor dem Aufruf der **Ausführen** Methode der **SQLSnapshot** -Objekt nur Zeilen, in denen "Rsmith" in der **User_id** Spalte wird in der Momentaufnahme enthalten sein.  
  
 **-DynamicSnapshotLocation** *Dynamic_snapshot_location*  
 Der Speicherort, an dem die dynamische Momentaufnahme generiert werden soll.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Die Ebene der SSL-Verschlüsselung (Secure Sockets Layer), die vom Momentaufnahme-Agent beim Herstellen von Verbindungen verwendet wird.  
  
|Wert von EncryptionLevel|Beschreibung|  
|---------------------------|-----------------|  
|**0**|Gibt an, dass SSL nicht verwendet wird.|  
|**1**|Gibt an, dass SSL verwendet wird, der Agent jedoch nicht überprüft, ob das SSL-Serverzertifikat von einem vertrauenswürdigen Aussteller signiert wurde.|  
|**2**|Gibt an, dass SSL verwendet und das Zertifikat überprüft wird.|  
  
 Weitere Informationen finden Sie unter [Sicherheitsübersicht & #40; Replikation und #41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-FieldDelimiter** *Field_delimiter*  
 Das Zeichen oder die Zeichenfolge, das bzw. die das Ende eines Felds in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datendatei für das Massenkopieren markiert. Die Standardeinstellung ist \n\<x$3>\n.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 Gibt den Umfang des Verlaufs an, der während eines Momentaufnahmevorgangs protokolliert wird. Sie können die negativen Auswirkungen der Verlaufsprotokollierung auf die Leistung minimieren, indem Sie den Wert **1**auswählen.  
  
|Wert von <legacyBold>HistoryVerboseLevel</legacyBold>|Beschreibung|  
|-------------------------------|-----------------|  
|**0**|Statusmeldungen werden entweder an der Konsole ausgegeben oder in eine Ausgabedatei geschrieben. Verlaufsdatensätze werden nicht in der Verteilungsdatenbank protokolliert.|  
|**1**|Aktualisieren Sie immer eine vorherige Verlaufsmeldung mit dem gleichen Status (Start, Status, Erfolg usw.). Wenn kein vorheriger Datensatz mit dem gleichen Status vorhanden ist, fügen Sie einen neuen Datensatz ein.|  
|**2** (Standard)|Fügen Sie neue Verlaufsdatensätze ein, es sei denn, der Datensatz bezieht sich z. B. auf Leerlaufmeldungen oder Meldungen zu Aufträgen mit langer Ausführungszeit. In diesen Fällen aktualisieren Sie die vorherigen Datensätze.|  
|**3**|Fügen Sie immer neue Datensätze ein, es sei denn, ein Datensatz bezieht sich auf Leerlaufmeldungen.|  
  
 **HRBcpBlocks -** *Number_of_blocks*  
 Die Anzahl der **Bcp** Datenblöcke, die zwischen den Writer und Reader Threads in der Warteschlange befinden. Der Standardwert lautet "50". **HRBcpBlocks** wird nur mit Oracle-Veröffentlichungen verwendet.  
  
> [!NOTE]  
>  Dieser Parameter wird zum Optimieren der Leistung von **Bcp** von einem Oracle-Verleger.  
  
 -**HRBcpBlockSize***Block_size*  
 Ist die Größe in Kilobyte (KB) der einzelnen **Bcp** Datenblock. Der Standardwert ist 64 KB. **HRBcpBlocks** wird nur mit Oracle-Veröffentlichungen verwendet.  
  
> [!NOTE]  
>  Dieser Parameter wird zum Optimieren der Leistung von **Bcp** von einem Oracle-Verleger.  
  
 **-HRBcpDynamicBlocks**  
 Ist, und zwar unabhängig davon, ob die Größe der einzelnen **Bcp** Datenblocks dynamisch wachsen kann. **HRBcpBlocks** wird nur mit Oracle-Veröffentlichungen verwendet.  
  
> [!NOTE]  
>  Dieser Parameter wird zum Optimieren der Leistung von **Bcp** von einem Oracle-Verleger.  
  
 **-KeepAliveMessageInterval** *Keep_alive_interval*  
 Ist die Zeitdauer in Sekunden, die der Snapshot-Agent vor, dass auf Back-End-Nachricht "wartet auf die [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) Tabelle. Der Standardwert beträgt 300 Sekunden.  
  
 **-LoginTimeOut** *Login_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Anmeldung eintritt. Der Standardwert ist **15** Sekunden.  
  
 **-MaxBcpThreads** *Number_of_threads*  
 Gibt die Anzahl von Massenkopiervorgängen an, die parallel ausgeführt werden können. Die maximale Anzahl von Threads und gleichzeitig vorhandenen ODBC-Verbindungen entspricht entweder **MaxBcpThreads** oder der Anzahl von Massenkopieranforderungen, die in der Verteilungsdatenbank in der Synchronisierungstransaktion enthalten sind. Dabei gilt der jeweils kleinere Wert. **MaxBcpThreads** müssen einen Wert größer als **0** und ist keine hartcodierte Obergrenze. Der Standardwert lautet **1**.  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 Wird verwendet, wenn irrelevante Löschvorgänge an den Abonnenten gesendet werden. Bei irrelevanten Löschvorgängen handelt es sich um DELETE-Befehle, die für Zeilen, die nicht zur Partition des Abonnenten gehören, an den Abonnenten gesendet werden. Irrelevante Löschvorgänge beeinträchtigen weder die Datenintegrität noch die Konvergenz, allerdings können sie zu unnötigem Netzwerkverkehr führen. Der Standardwert von **MaxNetworkOptimization** ist **0**. Festlegen von **MaxNetworkOptimization** auf **1** Minimieren dadurch das Risiko irrelevanter Löschvorgänge Reduzierung des Netzwerkverkehrs und eine netzwerkoptimierung. Wenn dieser Parameter auf **1** können auch die Speicherung von Metadaten zu erhöhen und die Leistung auf dem Verleger zu beeinträchtigen, wenn Sie mehrere Ebenen von joinfiltern und komplexe Teilmengenfilter vorhanden sind. Sie sollten sorgfältig bewerten Sie die Replikationstopologie und **MaxNetworkOptimization** auf **1** nur, wenn der Netzwerkverkehr durch irrelevante Löschvorgänge inakzeptabel hoch ist.  
  
> [!NOTE]  
>  Wenn dieser Parameter auf **1** eignet sich nur, wenn die synchronisierungsoptimierungsoption der Mergeveröffentlichung festgelegt ist **true** (die **@keep_partition_changes** Parameter [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-Ausgabe** *Output_path_and_file_name*  
 Der Pfad der Agentausgabedatei. Wenn kein Dateiname angegeben ist, wird die Ausgabe an die Konsole gesendet. Wenn eine Datei mit dem angegebenen Namen vorhanden ist, wird die Ausgabe an diese Datei angefügt.  
  
 **' - OutputVerboseLevel '** [ **0**| **1**| **2**]  
 Gibt an, ob die Ausgabe ausführlich sein soll.  
  
|Wert von OutputVerboseLevel|Beschreibung|  
|------------------------------|-----------------|  
|**0**|Nur Fehlermeldungen werden gedruckt.|  
|**1** (Standard)|Alle Statusberichtsmeldungen werden gedruckt (Standard).|  
|**2**|Alle Fehlermeldungen und Statusberichtsmeldungen werden gedruckt, was zum Debuggen nützlich ist.|  
  
 **-PacketSize** *Paketgröße*  
 Die vom Momentaufnahme-Agent beim Herstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendete Paketgröße (in Bytes). Der Standardwert ist 8192 Bytes.  
  
> [!NOTE]  
>  Sie sollten die Paketgröße nur dann ändern, wenn Sie sicher sind, dass die Leistung dadurch verbessert werden kann. Für die meisten Anwendungen empfiehlt sich die Standardpaketgröße.  
  
 **-ProfileName** *Profile_name*  
 Gibt ein Agentprofil an, das für Agentparameter verwendet werden soll. Wenn **ProfileName** den Wert NULL aufweist, wird das Agentprofil deaktiviert. Wenn **ProfileName** nicht angegeben ist, wird das Standardprofil für den Agenttyp verwendet. Weitere Informationen finden Sie unter [Replikations-Agentprofile](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherDB** *Verlegerdatenbank*  
 Der Name der Veröffentlichungsdatenbank. *Dieser Parameter wird nicht für Oracle-Verleger unterstützt*.  
  
 **Von PublisherDeadlockPriority -** [**-1**|**0**|**1**]  
 Die Priorität der Momentaufnahme-Agent-Verbindung mit dem Verleger, wenn ein Deadlock auftritt. Dieser Parameter wird angegeben, um Deadlocks zu beheben, die möglicherweise während der Momentaufnahmegenerierung zwischen dem Momentaufnahme-Agent und Benutzeranwendungen auftreten.  
  
|Wert von PublisherDeadlockPriority|Beschreibung|  
|-------------------------------------|-----------------|  
|**-1**|Bei Auftreten eines Deadlocks auf dem Verleger haben andere Anwendungen als der Momentaufnahme-Agent Priorität.|  
|**0** (Standard)|Es wird keine Priorität zugewiesen.|  
|**1**|Bei Auftreten eines Deadlocks auf dem Verleger hat der Momentaufnahme-Agent Priorität.|  
  
 **PublisherFailoverPartner -** *Servername*[**\\***Instance_name*]  
 Gibt die Failoverpartnerinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an, die an einer Datenbank-Spiegelungssitzung mit der Veröffentlichungsdatenbank teilnimmt. Weitere Informationen finden Sie unter [Datenbankspiegelung und Replikation & #40; SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **--PublisherLogin** *Publisher_login*  
 Der Anmeldename, der verwendet wird, um mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung eine Verbindung mit dem Verleger herzustellen.  
  
 **-PublisherPassword**  *Publisher_password*  
 Das Kennwort, das verwendet wird, um mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung eine Verbindung mit dem Verleger herzustellen. .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Gibt den Sicherheitsmodus des Verlegers an. Der Wert **0** gibt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung (Standard) und einem Wert von **1** Windows-Authentifizierungsmodus.  
  
 **QueryTimeOut -** *Query_time_out_seconds*  
 Die Anzahl von Sekunden, nach denen ein Timeout bei der Abfrage eintritt. Die Standardeinstellung ist 1800 Sekunden.  
  
 **ReplicationType -** [ **1**| **2**]  
 Gibt den Typ der Replikation an. Der Wert **1** gibt Transaktionsreplikation und der Wert **2** Mergereplikation.  
  
 **RowDelimiter -** *Row_delimiter*  
 Das Zeichen oder die Zeichenfolge, das bzw. die das Ende einer Zeile in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datendatei für das Massenkopieren markiert. Die Standardeinstellung ist \n\<,@g>\n.  
  
 **StartQueueTimeout -** *Start_queue_timeout_seconds*  
 Ist die maximale Anzahl von Sekunden, die der Snapshot-Agent wartet, wird die Anzahl von gleichzeitigen dynamischen Snapshotprozesse an das Limit der **@max_concurrent_dynamic_snapshots** -Eigenschaft des [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Wenn der Momentaufnahme-Agent nach Verstreichen der maximalen Anzahl von Sekunden immer noch wartet, wird der Agent beendet. Der Wert 0 bedeutet, dass der Agent unbegrenzt wartet, der Vorgang jedoch abgebrochen werden kann.  
  
 \- **UsePerArticleContentsView** *Use_per_article_contents_view*  
 Dieser Parameter wurde als veraltet markiert und wird lediglich aus Gründen der Abwärtskompatibilität unterstützt.  
  
## Hinweise  
  
> [!IMPORTANT]  
>  Wenn Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Agent so installiert haben, dass er unter einem lokalen Systemkonto und nicht unter einem Domänenbenutzerkonto (Standard) ausgeführt wird, kann der Dienst nur auf den lokalen Computer zugreifen. Wenn der Momentaufnahme-Agent, der unter dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Agent ausgeführt wird, so konfiguriert ist, dass beim Anmelden bei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] der Windows-Authentifizierungsmodus verwendet wird, schlägt der Momentaufnahme-Agent fehl. Die Standardeinstellung ist die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung.  
  
 Führen Sie zum Starten der Snapshot-Agent **snapshot.exe** von der Befehlszeile aus. Informationen hierzu finden Sie im [Abschnitt zu den ausführbaren Dateien von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  