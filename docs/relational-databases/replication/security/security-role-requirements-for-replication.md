---
title: "Sicherheitsrollenanforderungen f&#252;r die Replikation | Microsoft Docs"
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
  - "Sicherheit [SQL Server-Replikation], Rollen"
  - "Rollen [SQL Server], Replikation"
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Sicherheitsrollenanforderungen f&#252;r die Replikation
  Die Replikation schränkt auf der Basis der Rollen, die dem Benutzernamen des jeweiligen Benutzers zugeordnet sind, die Aktionen ein, die dieser Benutzer ausführen kann. Replikation verfügt über bestimmte Berechtigungen erteilt der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle und den Benutzernamen in der veröffentlichungszugriffsliste (PAL).  
  
## Sicherheitsrollenanforderungen für die Einrichtung der Replikation  
 Die folgende Tabelle gibt einen Überblick darüber, welche Authentifizierungsanforderungen für allgemeine Aufgaben bei der Einrichtung der Replikation erfüllt sein müssen:  
  
|Einrichtungsaufgabe|Erforderliche Mitgliedschaft|  
|----------------|----------------------------|  
|Aktivieren eines Verteilers, Verlegers bzw. Abonnenten|**sysadmin** -Serverrolle auf dem Verleger|  
|Aktivieren einer Datenbank für die Replikation|**sysadmin** -Serverrolle auf dem Verleger|  
|Erstellen einer Veröffentlichung|**Db_owner** -Datenbankrolle in der Publikationsdatenbank auf dem Verleger oder **Sysadmin** -Serverrolle auf dem Verleger.|  
|Anzeigen von Veröffentlichungseigenschaften|Mitglied der VERÖFFENTLICHUNGSZUGRIFFSLISTE auf dem Verleger **Db_owner** -Datenbankrolle in der Publikationsdatenbank auf dem Verleger oder **Sysadmin** -Serverrolle auf dem Verleger.|  
|Erstellen eines Abonnements|**Db_owner** -Datenbankrolle in der Publikationsdatenbank auf dem Verleger oder **Sysadmin** -Serverrolle auf dem Verleger.<br /><br /> **Db_owner** -Datenbankrolle in der Abonnementdatenbank auf dem Abonnenten oder **Sysadmin** -Serverrolle auf dem Abonnenten.|  
|Konfigurieren von Agentprofilen|**sysadmin** -Serverrolle auf dem Verteiler|  
  
## Sicherheitsrollenanforderungen für die Replikationswartung  
 Die folgende Tabelle gibt einen Überblick darüber, welche Authentifizierungsanforderungen für allgemeine Aufgaben bei der Wartung der Replikation erfüllt sein müssen:  
  
|Wartungsaufgabe|Erforderliche Mitgliedschaft|  
|----------------------|----------------------------|  
|Ändern oder Löschen eines Verteilers, Verlegers bzw. Abonnenten|**sysadmin** -Serverrolle auf dem entsprechenden Server|  
|Ändern oder Löschen einer Veröffentlichung|**Db_owner** -Datenbankrolle in der Publikationsdatenbank auf dem Verleger oder **Sysadmin** -Serverrolle auf dem Verleger.|  
|Ändern oder Löschen eines Abonnements auf dem Verleger|**Db_owner** -Datenbankrolle in der Publikationsdatenbank auf dem Verleger oder **Sysadmin** -Serverrolle auf dem Verleger.|  
|Ändern oder Löschen eines Abonnements auf dem Abonnenten|**Db_owner** -Datenbankrolle in der Abonnementdatenbank auf dem Abonnenten oder **Sysadmin** -Serverrolle auf dem Abonnenten.|  
|Markieren eines Abonnements für die Neuinitialisierung|Pushabonnement: **Db_owner** -Datenbankrolle in der Publikationsdatenbank auf dem Verleger oder **Sysadmin** -Serverrolle auf dem Verleger.<br /><br /> Pullabonnement: **Db_owner** -Datenbankrolle in der Abonnementdatenbank auf dem Abonnenten oder **Sysadmin** -Serverrolle auf dem Abonnenten.|  
|Anzeigen der Replikationsaktivität, der Fehler und des Verlaufs mithilfe des Replikationsmonitors. Ein Benutzer kann Agentprofile, Zeitpläne usw. nicht ändern, wenn er nicht Mitglied der **sysadmin** -Serverrolle ist.|**replmonitor** -Datenbankrolle in der Verteilungsdatenbank auf dem Verteiler bzw. **sysadmin** -Serverrolle auf dem Verteiler|  
|Warten von Replikations-Agents|**Db_owner** -Datenbankrolle in der entsprechenden Datenbank oder **Sysadmin** -Serverrolle auf dem entsprechenden Server.<br /><br /> Wenn der Agent von einem Benutzer in der **sysadmin** -Rolle erstellt wurde und für den Agent kein Proxykonto angegeben wurde, wird der Agent im Kontext des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Kontos ausgeführt. In diesem Fall kann ein Benutzer in der **Db_owner** Rolle den dem Agent zugeordneten Auftrag kann nicht geändert werden.|  
|Starten oder Beenden eines Replikations-Agents|Besitzer des Agentauftrags bzw. der **sysadmin** -Serverrolle auf dem entsprechenden Server.|  
  
## Siehe auch  
 [Bewährte Methoden für die Replikationssicherheit](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz & #40; Replikation & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  