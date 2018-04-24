---
title: Ausführbare Konzepte für die Programmierung von Replikations-Agents | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3376ec6d28da96321c7e598beab1f414b621961
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="replication-agent-executables-concepts"></a>Ausführbare Konzepte für die Programmierung von Replikations-Agents
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Replikations-Agents können wie folgt programmgesteuert kontrolliert werden:  
  
-   Mit den verwalteten Schnittstellen für die Agent-Programmierung im <xref:Microsoft.SqlServer.Replication> Namespace  
  
-   Durch Aufrufen von ausführbaren Dateien von Agents mit einem angegebenen Satz von Parametern von der Eingabeaufforderung aus  
  
 Das direkte Aufrufen von Replikations-Agents von der Eingabeaufforderung aus ermöglicht den programmgesteuerten Zugriff auf Agents vom Befehlszeilenskript in Batchdateien. Wenn ein Agent von der Eingabeaufforderung aus aufgerufen wird, wird er unter dem [!INCLUDE[msCoName](../../../includes/msconame-md.md)]-Windows-Sicherheitskonto des Benutzers ausgeführt, der den Agent aufgerufen oder die Batchdatei gestartet hat.  
  
 Instanzen der folgenden Replikations-Agents können mit ausführbaren Dateien ausgeführt werden.  
  
-   [Replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 Beim Aufrufen von Replikations-Agents können Sie Leistungsprofile verwenden, um einen definierten Satz von Parametern automatisch an die ausführbare Datei des Agents zu übergeben. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele zeigen, wie Replikations-Agents von der Eingabeaufforderung aus aufgerufen werden. Replikations-Agents können auch mit Replikationsverwaltungsobjekten (Replication Management Objects, RMO) aufgerufen werden. Weitere Informationen finden Sie unter [Synchronisieren von Abonnements](../../../relational-databases/replication/synchronize-subscriptions-replication.md).  
  
> [!NOTE]  
>  Zeilenumbrüche wurden in diesen Beispielen hinzugefügt, um die Lesbarkeit zu verbessern. In einer Batchdatei müssen Befehle in einer einzelnen Zeile stehen.  
  
### <a name="running-the-snapshot-agent"></a>Ausführen des Momentaufnahme-Agents  
 Mit dieser Beispielbatchdatei wird der Momentaufnahme-Agent von der Befehlsaufforderung aus aufgerufen, um eine Momentaufnahme für die **AdvWorksSalesOrdersMerge**-Veröffentlichung zu generieren. (Die unten angegebenen Skripts verwenden den Pfad zu den [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)]-Dateien (Version 130). Sie sollten die Skripts auf die Dateien für Ihre jeweilige Version von [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] einstellen.)  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>Ausführen des Verteilungs-Agents  
 Mit dieser Beispielbatchdatei wird der Verteilungs-Agent von der Eingabeaufforderung aus aufgerufen, um Änderungen der **AdvWorksProductTran**-Veröffentlichung kontinuierlich an einen Pushabonnenten zu replizieren.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>Ausführen des Merge-Agents  
 Mit dieser Beispielbatchdatei wird der Merge-Agent von der Eingabeaufforderung aus aufgerufen, um ein Pullabonnement für die **AdvWorksSalesOrdersMerge**-Veröffentlichung zu synchronisieren.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
