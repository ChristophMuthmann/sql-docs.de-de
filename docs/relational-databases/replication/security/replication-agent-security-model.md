---
title: "Sicherheitsmodell des Replikations-Agents | Microsoft Docs"
ms.custom: ""
ms.date: "10/07/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahme-Agent, Sicherheit"
  - "Agents [SQL Server-Replikation], Sicherheit"
  - "Verteilungs-Agent, Sicherheit"
  - "Anmeldungen [SQL Server-Replikation], Berechtigungen für Agents"
  - "Sicherheit [SQL Server-Replikation], Agent-Sicherheitsmodell"
  - "Protokolllese-Agent, Sicherheit"
  - "Warteschlangenlese-Agent, Sicherheit"
  - "Merge-Agent, Sicherheit"
  - "Replikation [SQL Server], Agents und Profile"
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
caps.latest.revision: 72
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 72
---
# Sicherheitsmodell des Replikations-Agents
  Das Sicherheitsmodell des Replikations-Agents ermöglicht die präzise Steuerung der Konten, unter denen Replikations-Agents ausgeführt werden und Verbindungen herstellen. Für jeden Agent kann ein gesondertes Konto angegeben werden. Weitere Informationen zur Vorgehensweise beim Angeben von Konten finden Sie unter [Verwalten von Anmeldenamen und Kennwörtern bei der Replikation](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
> [!IMPORTANT]  
>  Wenn ein Mitglied der festen Serverrolle **sysadmin** die Replikation konfiguriert, kann es die Replikations-Agents so konfigurieren, dass sie die Identität des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentkontos annehmen. Dies geschieht, indem für den Replikations-Agent kein Anmeldename oder Kennwort angegeben wird. Dieser Ansatz ist jedoch nicht empfehlenswert. Sie sollten besser als bewährte Methode in Bezug auf die Sicherheit für jeden Agent ein Konto mit den im Abschnitt zu den für Agents erforderlichen Berechtigungen beschriebenen minimalen Privilegien angeben.  
  
 Replikations-Agents werden wie alle ausführbaren Dateien im Kontext eines Windows-Kontos ausgeführt. Die Agents stellen mithilfe dieses Kontos Verbindungen über die integrierte Sicherheit von Windows her. Unter welchem Konto der Agent ausgeführt wird, ist davon abhängig, wie er gestartet wird:  
  
-   Starten des Agents aus einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentauftrag heraus (Standardeinstellung): Wenn ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentauftrag zum Starten eines Replikations-Agents verwendet wird, wird dieser Agent im Kontext eines Kontos ausgeführt, das Sie während der Replikationskonfiguration angeben. Weitere Informationen zum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent und der Replikation finden Sie im Abschnitt "Agentsicherheit mit SQL Server-Agent" weiter unten in diesem Thema. Weitere Informationen zu den Berechtigungen, die erforderlich sind für das Konto, unter dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent ausgeführt wird, finden Sie unter [SQL Server-Agent konfigurieren](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Starten des Agents von einer MS-DOS Befehlszeile, entweder direkt oder über ein Skript: Der Agent wird im Kontext des Benutzerkontos ausgeführt, der den Agent in der Befehlszeile ausführt.  
  
-   Starten des Agents aus einer Anwendung, von der Replikationsverwaltungsobjekte (RMO) oder ein ActiveX-Steuerelement verwendet werden: Der Agent wird im Kontext der Anwendung ausgeführt, die RMO bzw. das ActiveX-Steuerelement aufruft.  
  
    > [!NOTE]  
    >  ActiveX-Steuerelemente sind als veraltet markiert.  
  
 Es empfiehlt sich, Verbindungen im Kontext der integrierten Sicherheit von Windows herzustellen. Aus Gründen der Abwärtskompatibilität kann auch die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Sicherheit verwendet werden. Weitere Informationen zu bewährten Methoden finden Sie unter [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## Für Agents erforderliche Berechtigungen  
 Die Konten, unter denen Agents ausgeführt werden und über die sie Verbindungen herstellen, erfordern verschiedene Berechtigungen. Eine Beschreibung zu diesen Berechtigungen finden Sie in der folgenden Tabelle. Es empfiehlt sich, jeden Agent unter einem gesonderten Windows-Konto auszuführen. Außerdem sollten den einzelnen Konten lediglich die erforderlichen Berechtigungen erteilt werden. Weitere Informationen über die veröffentlichungszugriffsliste (PAL), die für eine Reihe von Agents relevant ist, finden Sie unter [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
> [!NOTE]  
>  Durch die Benutzerkontensteuerung (User Account Control, UAC) in einigen Windows-Betriebssystemen kann der Administratorzugriff auf die Momentaufnahmefreigabe verhindert werden. Sie müssen daher den vom Momentaufnahme-Agent, Verteilungs-Agent und Merge-Agent verwendeten Windows-Konten explizit Berechtigungen für die Momentaufnahmefreigabe erteilen. Dies ist auch dann erforderlich, wenn die Windows-Konten Mitglieder der Administratorengruppe sind. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
|Agent|Berechtigungen|  
|-----------|-----------------|  
|Momentaufnahme-Agent|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Verteiler herstellt. Für dieses Konto ist Folgendes erforderlich:<br /><br /> – Zumindest Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.<br /><br /> – Es muss über Lese-, Schreib- und Änderungsberechtigungen für die Momentaufnahmefreigabe verfügen.<br /><br /> <br /><br /> Beachten Sie, dass das Konto, das verwendet wird *Verbinden* mit dem Verleger muss mindestens Mitglied der **Db_owner** festen Datenbankrolle in der Publikationsdatenbank.|  
|Protokolllese-Agent|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Verteiler herstellt. Dieses Konto muss zumindest Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.<br /><br /> Das Konto, das verwendet wird, für die Verbindung mit dem Verleger muss mindestens Mitglied der **Db_owner** festen Datenbankrolle in der Publikationsdatenbank.<br /><br /> Bei der Auswahl der **Sync_type** Optionen *nur replikationsunterstützung*, *Initialisieren mit Sicherung*, oder *LSN initialisieren*, muss der Protokolllese-Agent nach der Ausführung ausgeführt **Sp_addsubscription**, sodass die festgelegten Skripts in die Verteilungsdatenbank geschrieben werden. Der Protokolllese-Agent muss unter einem Konto ausgeführt werden, das Mitglied der festen Serverrolle **sysadmin** ist. Wenn die **Sync_type** Option auf festgelegt ist *automatische*, keine besondere Log Reader Agent-Aktionen erforderlich sind.|  
|Verteilungs-Agent für Pushabonnements|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Verteiler herstellt. Für dieses Konto ist Folgendes erforderlich:<br /><br /> -Mindestens Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.<br /><br /> – Es muss Mitglied der PAL sein.<br /><br /> – Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.<br /><br /> – Es muss über die Leseberechtigung für das Installationsverzeichnis des OLE DB-Anbieters für den Abonnenten verfügen, wenn das Abonnement für einen Nicht-SQL Server-Abonnenten vorgesehen ist.<br /><br /> -Wenn Sie LOB-Daten zu replizieren, muss der Verteilungsagent auf die Replikation über Schreibberechtigungen verfügen **C:\Program Files\Microsoft SQL Server\XX\COMfolder** wobei XX die InstanceID darstellt.<br /><br /> <br /><br /> Beachten Sie, dass das Konto, das verwendet wird *Verbinden* an den Abonnenten müssen mindestens Mitglied der **Db_owner** festen Datenbankrollen in der Abonnementdatenbank oder über entsprechende Berechtigungen verfügen, wenn das Abonnement für eine nicht - SQL Server-Abonnent ist.<br /><br /> Beachten Sie, dass bei Verwendung `-subscriptionstreams >= 2` auf der Verteilungsagent, Sie müssen außerdem gewähren, der **View Server State** Berechtigung auf dem Abonnenten, um Deadlocks zu erkennen.|  
|Verteilungs-Agent für Pullabonnements|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Abonnenten herstellt. Dieses Konto muss zumindest Mitglied der **Db_owner** festen Datenbankrolle in der Abonnementdatenbank. Für das zum Herstellen der Verbindung mit dem Verteiler verwendete Konto ist Folgendes erforderlich:<br /><br /> – Es muss Mitglied der PAL sein.<br /><br /> – Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.<br /><br /> -Wenn Sie LOB-Daten zu replizieren, muss der Verteilungsagent auf die Replikation über Schreibberechtigungen verfügen **C:\Program Files\Microsoft SQL Server\XX\COMfolder** wobei XX die InstanceID darstellt.<br /><br /> <br /><br /> Beachten Sie, dass bei Verwendung `-subscriptionstreams >= 2` auf der Verteilungsagent, Sie müssen außerdem gewähren, der **View Server State** Berechtigung auf dem Abonnenten, um Deadlocks zu erkennen.|  
|Merge-Agent für Pushabonnements|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Verleger und dem Verteiler herstellt. Für dieses Konto ist Folgendes erforderlich:<br /><br /> -Mindestens Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.<br /><br /> – Es muss Mitglied der PAL sein.<br /><br /> – Die Anmeldung muss mit einem Benutzer in der Veröffentlichungsdatenbank verknüpft sein.<br /><br /> – Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.<br /><br /> <br /><br /> Beachten Sie, dass das Konto zu *Verbinden* an den Abonnenten müssen mindestens Mitglied der **Db_owner** festen Datenbankrolle in der Abonnementdatenbank.|  
|Merge-Agent für Pullabonnements|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Abonnenten herstellt. Dieses Konto muss zumindest Mitglied der **Db_owner** festen Datenbankrolle in der Abonnementdatenbank. Für das zum Herstellen der Verbindung mit dem Verleger und Verteiler verwendete Konto ist Folgendes erforderlich:<br /><br /> – Es muss Mitglied der PAL sein.<br /><br /> – Die Anmeldung muss mit einem Benutzer in der Veröffentlichungsdatenbank verknüpft sein.<br /><br /> – Die Anmeldung muss mit einem Benutzer in der Verteilungsdatenbank verknüpft sein. Der Benutzer kann der **Guest** -Benutzer sein.<br /><br /> – Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.|  
|Warteschlangenlese-Agent|Das Windows-Konto, unter dem der Agent ausgeführt wird, wird verwendet, wenn er Verbindungen mit dem Verteiler herstellt. Dieses Konto muss zumindest Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.<br /><br /> Das Konto, das verwendet wird, für die Verbindung mit dem Verleger muss mindestens Mitglied der **Db_owner** festen Datenbankrolle in der Publikationsdatenbank.<br /><br /> Die Verbindung mit dem Abonnenten verwendete Konto muss mindestens Mitglied der **Db_owner** festen Datenbankrolle in der Abonnementdatenbank.|  
  
## Agentsicherheit mit SQL Server-Agent  
 Wenn Sie die Replikation mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Prozeduren oder RMO konfigurieren, wird standardmäßig ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentauftrag für jeden Agent erstellt. Die Agents werden dann im Kontext eines Auftragsschritts ausgeführt, unabhängig davon, ob sie kontinuierlich, nach einem Zeitplan oder bei Bedarf ausgeführt werden. Diese Aufträge können im Ordner **Aufträge** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]angezeigt werden. Die Auftragsnamen sind in der folgenden Tabelle aufgeführt.  
  
|Agent|Auftragsname|  
|-----------|--------------|  
|Momentaufnahme-Agent|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Integer>**|  
|Momentaufnahme-Agent für eine Mergeveröffentlichungspartition|**Dyn_ \< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< GUID>**|  
|Protokolllese-Agent|**\< Publisher>-\< PublicationDatabase>-\< Integer>**|  
|Merge-Agent für Pullabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< SubscriptionDatabase>-\< Integer>**|  
|Merge-Agent für Pushabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>**|  
|Verteilungs-Agent für Pushabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>***|  
|Verteilungs-Agent für Pullabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< SubscriptionDatabase>-\< GUID>***\*|  
|Verteilungs-Agent für Pushabonnements für Nicht-SQL Server-Abonnenten|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>**|  
|Warteschlangenlese-Agent|**[\< Verteiler>]. \< ganze Zahl>**|  
  
 \*Bei Pushabonnements für Oracle-Veröffentlichungen lautet der Auftragsname ist **\< Publisher>-\< Publisher**> anstelle von **\< Publisher>-\< PublicationDatabase>**.  
  
 \*\*Bei Pullabonnements für Oracle-Veröffentlichungen lautet der Auftragsname ist **\< Publisher>-\< DistributionDatabase**> anstelle von **\< Publisher>-\< PublicationDatabase>**.  
  
 Wenn Sie die Replikation konfigurieren, geben Sie Konten an, unter denen die Agents ausgeführt werden sollen. Sämtliche Auftragsschritte werden jedoch im Sicherheitskontext eines *Proxys*ausgeführt, somit führt die Replikation folgende Zuordnungen für die von Ihnen angegebenen Agentkonten intern aus:  
  
-   Das Konto wird zunächst mithilfe des [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](../../../t-sql/statements/create-credential-transact-sql.md) -Anweisung einer Anmeldeinformation zugeordnet. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Proxys werden Anmeldeinformationen zum Speichern von Informationen zu Windows-Benutzerkonten verwendet.  
  
-   Die [Sp_add_proxy](../../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md) gespeicherte Prozedur wird aufgerufen, und die Anmeldeinformationen werden verwendet, um einen Proxy erstellen...  
  
> [!NOTE]  
>  Diese Informationen werden bereitgestellt, damit Sie besser verstehen, was für die Ausführung von Agents im angemessenen Sicherheitskontext erforderlich ist. Sie müssen in der Regel nicht direkt mit den Anmeldeinformationen oder Proxys interagieren, die erstellt wurden.  
  
## Siehe auch  
 [Bewährte Methoden für die Replikationssicherheit](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz & #40; Replikation & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  