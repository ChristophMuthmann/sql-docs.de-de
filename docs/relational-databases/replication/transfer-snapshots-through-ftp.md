---
title: "&#220;bertragen von Momentaufnahmen &#252;ber FTP | Microsoft Docs"
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
  - "Momentaufnahmen [SQL Server-Replikation], FTP-Momentaufnahmen"
  - "FTP-Momentaufnahmen [SQL Server-Replikation]"
  - "Momentaufnahmereplikation [SQL Server], FTP"
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# &#220;bertragen von Momentaufnahmen &#252;ber FTP
  Standardmäßig werden Momentaufnahmen in Ordnern gespeichert, die als im UNC-Format (Universal Naming Convention) angegebene Dateifreigaben definiert sind. Bei der Replikation haben Sie ebenfalls die Möglichkeit, FTP-Freigaben (FTP, File Transfer Protocol) anstelle der UNC-Freigaben anzugeben. Dazu müssen Sie einen FTP-Server und anschließend eine Veröffentlichung sowie mindestens ein Abonnement über FTP konfigurieren. Informationen dazu, wie ein FTP-Server konfiguriert wird, finden Sie in der Internetinformationsdienste (IIS)-Dokumentation. Wenn Sie FTP-Informationen für eine Veröffentlichung angeben, verwenden die Abonnements dieser Veröffentlichung standardmäßig FTP. FTP wird nur zur Websynchronisierung verwendet, wenn der Computer, auf dem IIS (Internet Information Services, Internetinformationsdienste) ausgeführt wird, vom Verteiler durch eine Firewall getrennt ist. In diesem Fall kann die Momentaufnahme über FTP vom Verteiler an den Computer, auf dem IIS ausgeführt wird, gesendet werden. (Zur Übertragung der Momentaufnahme an den Abonnenten wird immer HTTPS verwendet.)  
  
> [!IMPORTANT]  
>  Es wird empfohlen, vorzugsweise die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Authentifizierung und eine UNC-Freigabe statt einer FTP-Freigabe zu verwenden, da FTP-Kennwörter gespeichert werden müssen, und das Kennwort vom Abonnenten oder von dem Computer, auf dem IIS bei der Websynchronisierung ausgeführt wird, als unverschlüsselter Text an den FTP-Server gesendet wird. Außerdem ist es bei der Übertragung über FTP nicht möglich, sicherzustellen, dass ein Abonnent einer gefilterten Mergeveröffentlichung ausschließlich auf die Momentaufnahmen seiner Datenpartition zugreifen kann, da ein einziges Konto den Zugriff auf die gesamte Momentaufnahme-Freigabe kontrolliert.  
  
 Informationen zum Übermitteln einer Momentaufnahme über FTP finden Sie unter [Deliver a Snapshot Through FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
## Siehe auch  
 [Websynchronisierung für die Mergereplikation](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Momentaufnahmeoptionen](../../relational-databases/replication/snapshot-options.md)  
  
  