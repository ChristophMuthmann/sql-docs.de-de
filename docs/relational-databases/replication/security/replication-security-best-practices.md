---
title: "Bewährte Methoden für die Replikationssicherheit | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 85ab9523752bc1f72c1535cc00e51e50dbac946e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="replication-security-best-practices"></a>Bewährte Methoden für die Replikationssicherheit
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Bei der Replikation werden Daten in verteilten Umgebungen verschoben. Diese reichen von Intranets auf einer einzelnen Domäne bis hin zu Anwendungen, die auf Daten zwischen nicht vertrauenswürdigen Domänen und über das Internet zugreifen. Es ist wichtig, die beste Methode für die Sicherung der Replikationsverbindungen unter diesen verschiedenen Voraussetzungen zu kennen und zu verstehen.  
  
 Folgende Informationen sind für die Replikation in sämtlichen Umgebungen relevant:  
  
-   Verschlüsseln Sie die Verbindungen zwischen Computern in einer Replikationstopologie mithilfe einer Industriestandardmethode, wie beispielsweise Virtual Private Networks (VPN), Secure Sockets Layer (SSL) oder IP Security (IPSEC). Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Informationen zum Verwenden von VPN und SSL für die Replikation von Daten über das Internet finden Sie unter [Securing Replication Over the Internet](../../../relational-databases/replication/security/securing-replication-over-the-internet.md).  
  
     Wenn Sie SSL zum Sichern der Verbindungen zwischen Computern in einer Replikationstopologie verwenden, geben Sie den Wert **1** oder **2** für den Parameter **-EncryptionLevel** der einzelnen Replikations-Agents an (der Wert **2** wird empfohlen). Mit dem Wert **1** wird angegeben, dass eine Verschlüsselung verwendet wird. Der Agent überprüft aber nicht, ob das SSL-Serverzertifikat von einem vertrauenswürdigen Aussteller signiert wurde. Mit dem Wert **2** wird angegeben, dass das Zertifikat überprüft wurde. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Befehlszeilenparametern des Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Ausführbare Konzepte für die Programmierung von Replikations-Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Führen Sie jeden Replikations-Agent unter einem anderen Windows-Konto aus, und verwenden Sie die Windows-Authentifizierung für sämtliche Verbindungen des Replikations-Agents. Weitere Informationen zum Angeben von Konten finden Sie unter [Verwalten von Anmeldenamen und Kennwörtern bei der Replikation](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Erteilen Sie jedem Agent nur die erforderlichen Berechtigungen. Weitere Informationen finden Sie im Abschnitt zu den für die Agents erforderlichen Berechtigungen unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Stellen Sie sicher, dass sich alle Konten für Merge-Agents und Verteilungs-Agents in der Veröffentlichungszugriffsliste (PAL, Publication Access List) befinden. Weitere Informationen finden Sie unter [Schützen des Verteilers](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
-   Befolgen Sie das Prinzip der geringsten Rechte, indem Sie den Konten in der PAL nur die Berechtigungen erteilen, die sie zur Ausführung von Replikationstasks benötigen. Fügen Sie keine Anmeldungen zu festen Serverrollen hinzu, die nicht für die Replikation erforderlich sind.  
  
-   Konfigurieren Sie die Momentaufnahmefreigabe, um den Lesezugriff für alle Merge-Agents und Verteilungs-Agents zuzulassen. Im Fall von Momentaufnahmen für Veröffentlichungen mit parametrisierten Filtern sollten Sie sicherstellen, dass jeder Ordner so konfiguriert wird, dass der Zugriff nur für die geeigneten Merge-Agent-Konten gewährt wird.  
  
-   Konfigurieren sie die Momentaufnahmefreigabe so, dass der Schreibzugriff für den Momentaufnahme-Agent gewährt wird.  
  
-   Falls Sie Pullabonnements verwenden, sollten Sie anstelle eines lokalen Pfads für den Momentaufnahmeordner eine Netzwerkfreigabe verwenden.  
  
 Falls Ihre Replikationstopologie Computer enthält, die sich nicht in derselben Domäne oder in Domänen befinden, zwischen denen keine Vertrauensstellungen bestehen, können Sie die Windows-Authentifizierung oder die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung für die von den Agents hergestellten Verbindungen verwenden. (Weitere Informationen zu Domänen finden Sie in der Windows-Dokumentation.) Es empfiehlt sich, als bewährte Sicherheitsmethode die Windows-Authentifizierung zu verwenden.  
  
-   So verwenden Sie die Windows-Authentifizierung  
  
    -   Fügen Sie ein lokales Windows-Konto (kein Domänenkonto) für jeden Agent an den passenden Knoten hinzu (verwenden Sie an jedem Knoten denselben Namen und dasselbe Kennwort). Beispielsweise wird der Verteilungs-Agent für ein Pushabonnement auf dem Verteiler ausgeführt und stellt Verbindungen mit dem Verteiler und mit dem Abonnenten her. Das Windows-Konto für den Verteilungs-Agent sollte dem Verteiler und dem Abonnenten hinzugefügt werden.  
  
    -   Stellen Sie sicher, dass ein bestimmter Agent (z. B. ein Verteilungs-Agent für ein Abonnement) auf jedem Computer unter demselben Konto ausgeführt wird.  
  
-   So verwenden Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung  
  
    -   Fügen Sie ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konto für jeden Agent an den passenden Knoten hinzu (verwenden Sie an jedem Knoten denselben Namen und dasselbe Kennwort). Beispielsweise wird der Verteilungs-Agent für ein Pushabonnement auf dem Verteiler ausgeführt und stellt Verbindungen mit dem Verteiler und mit dem Abonnenten her. Das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konto für den Verteilungs-Agent sollte dem Verteiler und dem Abonnenten hinzugefügt werden.  
  
    -   Stellen Sie sicher, dass ein bestimmter Agent (z. B. ein Verteilungs-Agent für ein Abonnement) auf jedem Computer unter demselben Konto Verbindungen herstellt.  
  
    -   In Situationen, für die die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung erforderlich ist, ist der Zugriff auf die UNC-Momentaufnahmefreigabe oft nicht verfügbar (der Zugriff kann z. B. durch eine Firewall gesperrt sein). In diesem Fall können Sie die Momentaufnahme über das Dateiübertragungsprotokoll (FTP, File Transfer Protokoll) auf Abonnenten übertragen. Weitere Informationen finden Sie unter [Übertragen von Momentaufnahmen über FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replikation über das Internet](../../../relational-databases/replication/replication-over-the-internet.md)   
 [Sichern des Abonnenten](../../../relational-databases/replication/security/secure-the-subscriber.md)   
 [Schützen des Verteilers](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
