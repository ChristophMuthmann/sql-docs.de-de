---
title: "Ausf&#252;hren von Skripts vor und nach dem Anwenden der Momentaufnahme | Microsoft Docs"
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
  - "Momentaufnahmen [SQL Server-Replikation], Skripts"
  - "Skripts [SQL Server-Replikation], Momentaufnahmen"
  - "Momentaufnahmereplikation [SQL Server], Skripts"
  - "Skripts [SQL Server-Replikation]"
ms.assetid: 9a6872c2-9bed-477f-9d2f-332d640edcf2
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Ausf&#252;hren von Skripts vor und nach dem Anwenden der Momentaufnahme
  Sie können angeben, ob Skripts auf dem Abonnenten vor oder nach dem Anwenden der Momentaufnahme ausgeführt werden. Skripts können für verschiedene Zecke verwendet werden, z. B. zum Erstellen von Anmeldungen und Schemas (Objektbesitzer) auf den einzelnen Abonnenten.  
  
 Sie geben einen Dateispeicherort für jedes Skript an, und der Momentaufnahme-Agent kopiert jeweils bei der Verarbeitung der Momentaufnahme die Skriptdateien in den aktuellen Momentaufnahmeordner. Der Verteilungs-Agent oder der Merge-Agent führt das Vor-Momentaufnahme-Skript vor allen Skripts für replizierte Objekte aus, wenn eine Momentaufnahme angewendet wird. Der Verteilungs-Agent oder der Merge-Agent führt das Nach-Momentaufnahme-Skript nach der Momentaufnahme aus, nachdem alle anderen Skripts für replizierte Objekte und Daten angewendet wurden. Nachdem die Momentaufnahmeanwendung abgeschlossen ist und Skriptdateien erfolgreich ausgeführt wurden, werden die Skriptdateien aus dem Arbeitsverzeichnis auf dem Abonnenten entfernt.  
  
 Das Skript wird ausgeführt, indem das Hilfsprogramm **sqlcmd** gestartet wird. Führen Sie das Skript vor der Bereitstellung mithilfe von **sqlcmd** aus, um sicherzustellen, dass es erwartungsgemäß ausgeführt wird. Der Inhalt von Skripts, die vor und nach dem Anwenden der Momentaufnahme ausgeführt werden, muss wiederholbar sein. Wenn Sie z. B. eine Tabelle im Skript erstellen, müssen Sie zuerst ihr Vorhandensein überprüfen und daraufhin die entsprechende Aktion vornehmen. Das Skript muss wiederholbar sein, denn beim erneuten Initialisieren eines Abonnements, für das das Skript bereits angewendet wurde, wird das Skript erneut angewendet, wenn die neue Momentaufnahme während der erneuten Initialisierung angewendet wird.  
  
 Falls Sie die Momentaufnahmedatei komprimieren (indem sie in das CAB-Dateiformat von [!INCLUDE[msCoName](../../includes/msconame-md.md)] kopiert wird), werden die Skripts ebenfalls komprimiert und in der CAB-Datei platziert. Nachdem die komprimierte Momentaufnahmedatei zum Abonnenten übertragen und in ein Arbeitsverzeichnis auf dem Abonnenten dekomprimiert wurde, werden als Vor-Momentaufnahme-Skripts gekennzeichnete Skripts ausgeführt. Genauso werden alle Nach-Momentaufnahme-Skripts dekomprimiert und auf dem Abonnenten als letzter Schritt der Anwendung der Momentaufnahme ausgeführt.  
  
 **So führen Sie Skripts vor und nach dem Anwenden der Momentaufnahme aus**  
  
-   [! INCLUDE [SsManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [How to: Execute Scripts Before and After a Snapshot is Applied \(SQL Server Management Studio\)](../../relational-databases/replication/execute scripts before and after a snapshot is applied.md)  
  
-   Replikation [!INCLUDE[tsql](../../includes/tsql-md.md)] programming: [Snapshot-Eigenschaften konfigurieren & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## Siehe auch  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Momentaufnahmeoptionen](../../relational-databases/replication/snapshot-options.md)  
  
  