---
title: "Momentaufnahmeordner | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replicationutilities.specifysnapshotfolder.f1"
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Momentaufnahmeordner
  Die Seite **Momentaufnahmeordner** wird im Verteilungskonfigurations-Assistenten und im Assistenten für neue Veröffentlichung angezeigt. Der Speicherort Sie angeben, für der Snapshotordner als Standard für alle Verleger, die in diesem Assistenten aktivierten verwendet werden (der standardmäßige momentaufnahmeordner gilt nicht für Verleger, die später mit aktiviert wurden die **Verteilereigenschaften** Dialogfeld). Sie können diese Standardeinstellung für jeden Verleger auf der Seite **Verleger** des Verteilungskonfigurations-Assistenten oder im Dialogfeld **Verteilereigenschaften** überschreiben.  
  
 Der Momentaufnahmeordner ist lediglich ein von Ihnen freigegebenes Verzeichnis. Agents, die aus diesem Ordner lesen bzw. in den Ordner schreiben, benötigen ausreichende Zugriffsberechtigungen. Weitere Informationen zur Absicherung des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md). Testen Sie vor der Implementierung der Replikation, ob die Replikations-Agents eine Verbindung mit dem Momentaufnahmeordner herstellen können. Melden Sie sich unter dem von dem jeweiligen Agenten verwendeten Konto an, und versuchen Sie, auf den Momentaufnahmeordner zuzugreifen.  
  
## Optionen  
 **Momentaufnahmeordner**  
 Geben Sie den Pfad für den Ordner an, in dem Momentaufnahmedateien gespeichert werden sollen.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt die Verwendung einer Netzwerkfreigabe als Speicherort des Momentaufnahmeordners. Lokale Pfade (beginnend mit einem Laufwerksbuchstaben, z. B. C:\\) nicht an die Agents auf anderen Computern zugegriffen werden.  
  
## Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  