---
title: Konfigurieren von Momentaufnahmeeigenschaften (Replikationsprogrammierung mit Transact-SQL) | Microsoft Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 696e717afbf46a23987d1cd611e5b57d5c935c4e
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Konfigurieren von Momentaufnahmeeigenschaften (Replikationsprogrammierung mit Transact-SQL)
  Momentaufnahmeeigenschaften können mithilfe gespeicherter Replikationsprozeduren programmgesteuert definiert und geändert werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>So konfigurieren Sie Momentaufnahmeeigenschaften beim Erstellen einer Momentaufnahme oder einer Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)aus. Geben Sie einen Veröffentlichungsnamen für **@publication**, den Wert **snapshot** oder **continuous** für **@repl_freq**und einen oder mehrere der folgenden Momentaufnahmeparameter ein:  
  
    -   **@alt_snapshot_folder** &ndash; Geben Sie einen Pfad an, wenn von diesem Speicherort, anstatt vom Standardmomentaufnahmeordner oder zusätzlich zu diesem, auf die Momentaufnahme für diese Veröffentlichung zugegriffen wird.  
  
    -   **@compress_snapshot** &ndash; Geben Sie den Wert **true** an, wenn die Momentaufnahmedateien im alternativen Momentaufnahmeordner im [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB-Dateiformat komprimiert sind.  
  
    -   **@pre_snapshot_script** &ndash; Geben Sie den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, bevor die Anfangsmomentaufnahme angewendet wird.  
  
    -   **@post_snapshot_script** &ndash; Geben Sie den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, nachdem die Anfangsmomentaufnahme angewendet wurde.  
  
    -   **@snapshot_in_defaultfolder** &ndash; Geben Sie den Wert **false** an, wenn die Momentaufnahme nur in einem anderen als dem Standardverzeichnis verfügbar ist.  
  
     Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>So konfigurieren Sie Momentaufnahmeeigenschaften beim Erstellen einer Momentaufnahme oder einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)aus. Geben Sie einen Veröffentlichungsnamen für **@publication**, den Wert **snapshot** oder **continuous** für **@repl_freq**und einen oder mehrere der folgenden Momentaufnahmeparameter ein:  
  
    -   **@alt_snapshot_folder** &ndash; Geben Sie einen Pfad an, wenn von diesem Speicherort, anstatt vom Standardmomentaufnahmeordner oder zusätzlich zu diesem, auf die Momentaufnahme für diese Veröffentlichung zugegriffen wird.  
  
    -   **@compress_snapshot** &ndash; Geben Sie den Wert **true** an, wenn die Momentaufnahmedateien im alternativen Momentaufnahmeordner im CAB-Dateiformat komprimiert sind.  
  
    -   **@pre_snapshot_script** &ndash; Geben Sie den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, bevor die Anfangsmomentaufnahme angewendet wird.  
  
    -   **@post_snapshot_script** &ndash; Geben Sie den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, nachdem die Anfangsmomentaufnahme angewendet wurde.  
  
    -   **@snapshot_in_defaultfolder** &ndash; Geben Sie den Wert **false** an, wenn die Momentaufnahme nur in einem anderen als dem Standardverzeichnis verfügbar ist.  
  
2.  Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>So ändern Sie die Momentaufnahmeeigenschaften einer bestehenden Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)aus. Geben Sie den Wert **1** für **@force_invalidate_snapshot** und einen der folgenden Werte für **@property**an:  
  
    -   **alt_snapshot_folder** &ndash; Geben Sie außerdem einen neuen Pfad zum alternativen Momentaufnahmeordner für **@value**aus.  
  
    -   **compress_snapshot** &ndash; Geben Sie außerdem entweder **true** oder **false** für **@value** an, um zu definieren, ob die Momentaufnahmedateien im alternativen Momentaufnahmeordner im CAB-Dateiformat komprimiert sind.  
  
    -   **pre_snapshot_script** &ndash; Geben Sie außerdem für **@value** den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, bevor die Anfangsmomentaufnahme angewendet wird.  
  
    -   **post_snapshot_script** &ndash; Geben Sie außerdem für **@value** den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, nachdem die Anfangsmomentaufnahme angewendet wurde.  
  
    -   **snapshot_in_defaultfolder** &ndash; Geben Sie außerdem den Wert **true** oder **false** an, um zu definieren, ob die Momentaufnahme an einem anderen als dem Standardspeicherort verfügbar ist.  
  
2.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)aus. Geben Sie **@publication** und einen oder mehrere der zu ändernden Parameter für die Zeitplanung oder Sicherheitsanmeldeinformationen an.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
3.  Führen Sie den [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) von der Eingabeaufforderung aus, oder starten Sie den Momentaufnahme-Agentauftrag, um eine neue Momentaufnahme zu erzeugen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>So ändern Sie die Momentaufnahmeeigenschaften einer bestehenden Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)aus. Geben Sie den Wert **1** für **@force_invalidate_snapshot** und einen der folgenden Werte für **@property**an:  
  
    -   **alt_snapshot_folder** &ndash; Geben Sie außerdem einen neuen Pfad zum alternativen Momentaufnahmeordner für **@value**aus.  
  
    -   **compress_snapshot** &ndash; Geben Sie außerdem entweder **true** oder **false** für **@value** an, um zu definieren, ob die Momentaufnahmedateien im alternativen Momentaufnahmeordner im CAB-Dateiformat komprimiert sind.  
  
    -   **pre_snapshot_script** &ndash; Geben Sie außerdem für **@value** den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, bevor die Anfangsmomentaufnahme angewendet wird.  
  
    -   **post_snapshot_script** &ndash; Geben Sie außerdem für **@value** den Dateinamen und den vollständigen Pfad einer **.sql** -Datei an, die während der Initialisierung auf dem Abonnenten ausgeführt wird, nachdem die Anfangsmomentaufnahme angewendet wurde.  
  
    -   **snapshot_in_defaultfolder** &ndash; Geben Sie außerdem den Wert **true** oder **false** an, um zu definieren, ob die Momentaufnahme an einem anderen als dem Standardspeicherort verfügbar ist.  
  
2.  Führen Sie den [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) von der Eingabeaufforderung aus, oder starten Sie den Momentaufnahme-Agentauftrag, um eine neue Momentaufnahme zu erzeugen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird eine Veröffentlichung erstellt, die einen alternativen Momentaufnahmeordner und eine komprimierte Momentaufnahme verwendet.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Komprimierte Momentaufnahmen](../../../relational-databases/replication/compressed-snapshots.md)   
 [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Übertragen von Momentaufnahmen über FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  
