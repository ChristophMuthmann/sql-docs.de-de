---
title: "Konfigurieren von Momentaufnahmeeigenschaften (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], Eigenschaften"
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Konfigurieren von Momentaufnahmeeigenschaften (Replikationsprogrammierung mit Transact-SQL)
  Momentaufnahmeeigenschaften können mithilfe gespeicherter Replikationsprozeduren programmgesteuert definiert und geändert werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab.  
  
### So konfigurieren Sie Momentaufnahmeeigenschaften beim Erstellen einer Momentaufnahme oder einer Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger [Sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Geben Sie einen Veröffentlichungsnamen für **@publication**, entweder den Wert **Snapshot** oder **fortlaufenden** für **@repl_freq**, und mindestens eines der folgenden momentaufnahmeparameter:  
  
    -   **@alt_snapshot_folder** -Geben Sie einen Pfad ein, wenn von diesem Speicherort anstelle von oder zusätzlich zu den Standardordner für Momentaufnahme der Momentaufnahme für diese Veröffentlichung zugegriffen wird.  
  
    -   **@compress_snapshot** -Geben Sie den Wert **true** Wenn die momentaufnahmedateien im alternativen momentaufnahmeordner im komprimiert sind die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB-Dateiformat.  
  
    -   **@pre_snapshot_script** -Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung bevor die anfangsmomentaufnahme angewendet wird.  
  
    -   **@post_snapshot_script** -Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung nachdem die anfangsmomentaufnahme angewendet wird.  
  
    -   **@snapshot_in_defaultfolder** -Geben Sie den Wert **false** wenn die Momentaufnahme nur in einem nicht standardmäßigen Speicherort verfügbar ist.  
  
     Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### So konfigurieren Sie Momentaufnahmeeigenschaften beim Erstellen einer Momentaufnahme oder einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [Sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Geben Sie einen Veröffentlichungsnamen für **@publication**, entweder den Wert **Snapshot** oder **fortlaufenden** für **@repl_freq**, und mindestens eines der folgenden momentaufnahmeparameter:  
  
    -   **@alt_snapshot_folder** -Geben Sie einen Pfad ein, wenn von diesem Speicherort anstelle von oder zusätzlich zu den Standardordner für Momentaufnahme der Momentaufnahme für diese Veröffentlichung zugegriffen wird.  
  
    -   **@compress_snapshot** -Geben Sie den Wert **true** Wenn die momentaufnahmedateien im alternativen momentaufnahmeordner im CAB-Dateiformat komprimiert sind.  
  
    -   **@pre_snapshot_script** -Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung bevor die anfangsmomentaufnahme angewendet wird.  
  
    -   **@post_snapshot_script** -Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung nachdem die anfangsmomentaufnahme angewendet wird.  
  
    -   **@snapshot_in_defaultfolder** -Geben Sie den Wert **false** wenn die Momentaufnahme nur in einem nicht standardmäßigen Speicherort verfügbar ist.  
  
2.  Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### So ändern Sie die Momentaufnahmeeigenschaften einer bestehenden Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Geben Sie den Wert **1** für **@force_invalidate_snapshot** und einen der folgenden Werte für **@property**:  
  
    -   **Alt_snapshot_folder** -Geben Sie auch einen neuen Pfad zum alternativen momentaufnahmeordner für **@value**.  
  
    -   **Compress_snapshot** -Geben Sie auch den Wert entweder **true** oder **false** für **@value** an, ob die momentaufnahmedateien im alternativen momentaufnahmeordner im CAB-Dateiformat komprimiert sind.  
  
    -   **Pre_snapshot_script** – auch für **@value** Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung bevor die anfangsmomentaufnahme angewendet wird.  
  
    -   **Post_snapshot_script** – auch für **@value** Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung nachdem die anfangsmomentaufnahme angewendet wird.  
  
    -   **Snapshot_in_defaultfolder** -Geben Sie auch den Wert entweder **true** oder **false** an, ob die Momentaufnahme nur in einem nicht standardmäßigen Speicherort verfügbar ist.  
  
2.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md). Geben Sie **@publication** und einen oder mehrere der zu ändernden Parameter für die Zeitplanung oder Sicherheitsanmeldeinformationen an.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
3.  Führen Sie den [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) von der Eingabeaufforderung aus, oder starten Sie den Momentaufnahme-Agentauftrag, um eine neue Momentaufnahme zu erzeugen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
### So ändern Sie die Momentaufnahmeeigenschaften einer bestehenden Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Geben Sie den Wert **1** für **@force_invalidate_snapshot** und einen der folgenden Werte für **@property**:  
  
    -   **Alt_snapshot_folder** -Geben Sie auch einen neuen Pfad zum alternativen momentaufnahmeordner für **@value**.  
  
    -   **Compress_snapshot** -Geben Sie auch den Wert entweder **true** oder **false** für **@value** an, ob die momentaufnahmedateien im alternativen momentaufnahmeordner im CAB-Dateiformat komprimiert sind.  
  
    -   **Pre_snapshot_script** – auch für **@value** Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung bevor die anfangsmomentaufnahme angewendet wird.  
  
    -   **Post_snapshot_script** – auch für **@value** Geben Sie den Dateinamen und den vollständigen Pfad einer **SQL** -Datei, die ausgeführt wird, auf dem Abonnenten während der Initialisierung nachdem die anfangsmomentaufnahme angewendet wird.  
  
    -   **Snapshot_in_defaultfolder** -Geben Sie auch den Wert entweder **true** oder **false** an, ob die Momentaufnahme nur in einem nicht standardmäßigen Speicherort verfügbar ist.  
  
2.  Führen Sie den [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) von der Eingabeaufforderung aus, oder starten Sie den Momentaufnahme-Agentauftrag, um eine neue Momentaufnahme zu erzeugen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## Beispiel  
 In diesem Beispiel wird eine Veröffentlichung erstellt, die einen alternativen Momentaufnahmeordner und eine komprimierte Momentaufnahme verwendet.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Komprimierte Momentaufnahmen](../../../relational-databases/replication/compressed-snapshots.md)   
 [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Übertragen von Momentaufnahmen über FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  