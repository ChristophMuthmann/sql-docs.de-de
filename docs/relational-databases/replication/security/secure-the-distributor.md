---
title: "Sch&#252;tzen des Verteilers | Microsoft Docs"
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
  - "Sicherheit [SQL Server-Replikation], Verteiler"
  - "Verteiler [SQL Server-Replikation], Sicherheit"
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Sch&#252;tzen des Verteilers
  Die folgenden Replikations-Agents stellen eine Verbindung mit dem Verteiler her: Protokolllese-Agent, Momentaufnahme-Agent, Warteschlangenlese-Agent und Merge-Agent. Es ist wichtig, dass jeder dieser Agents einen geeigneten Anmeldenamen besitzt, dass grundsätzlich nur die minimal erforderlichen Rechte erteilt werden und dass die Speicherung aller Kennwörter geschützt ist:  
  
-   Informationen zum Verwalten von Benutzernamen und Kennwörtern finden Sie unter [Verwalten von Anmeldenamen und Kennwörtern bei der Replikation](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Weitere Informationen zu den für die jeweiligen Agents erforderlichen Berechtigungen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Neben der Verwaltung von Benutzernamen und Kennwörter entsprechend ein, es ist wichtig zu verstehen, die Rolle des der **Repl_distributor** -remoteserverlink und der **Distributor_admin** Konto.  
  
## Schützen der Verbindung vom Verleger zum Verteiler  
 Zur Unterstützung der Kommunikation, die erforderlich, wenn administrative gespeicherte Prozeduren auf dem Verleger und Updateinformationen auf dem Verteiler ausgeführt, die remote-Server automatisch die Replikation konfiguriert **Repl_distributor**. Die **Repl_distributor** remoteservereintrag wird für die Kommunikation mit der Verteilungsdatenbank, unabhängig davon, ob die Verteilungsdatenbank in der Verlegerinstanz (ein lokaler Verteiler) enthalten ist, oder befindet sich in einer verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Instanz (ein Remoteverteiler).  
  
 Ist die Verteilungsdatenbank in einer lokalen Instanz enthalten, wird ein zufälliges Kennwort generiert und automatisch konfiguriert. Die Verteilungsdatenbank auf einer Remoteinstanz befindet, konfiguriert der Administrator ein gemeinsames Kennwort beim Einrichten des Verlegers und Verteilers; Dieses Kennwort dient dann zur Authentifizierung des Datenverkehrs, der durchläuft die **Repl_distributor** Link.  
  
 Der Verteiler verwendet die **Repl_distributor** Remoteserver-Eintrag, um sicherzustellen, dass der aufrufende Server als Verleger auf dem Verteiler konfiguriert ist, überprüft er das vom Verleger angegebene Kennwort und überprüft, ob die gespeicherte Prozedur eine Replikation ist gespeicherte Prozedur während der Ausführung.  
  
 Das Kennwort für konfiguriert die **Repl_distributor** remoteservereintrag während des Setups zugeordnet ist eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldung **Distributor_admin**, die hinzugefügt wird die **Sysadmin** festen Serverrolle auf dem Verteiler. Die **Distributor_admin** Anmeldung wird von gespeicherten Replikationsprozeduren verwendet, wenn die Verbindung zum Verteiler.  
  
> [!NOTE]  
>  Ändern Sie das Kennwort für die nicht die **Distributor_admin** manuell. Verwenden Sie immer die **Sp_changedistributor_password** gespeicherte Prozedur oder die **Verteilereigenschaften** oder **Replikationskennwörter aktualisieren** Dialogfeldern in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], da das Kennwort werden dann für lokale Veröffentlichungen automatisch geändert.  
  
## Sicherheit des Momentaufnahmeordners  
 Stellen Sie sicher, dass der Momentaufnahmefreigabe Lesezugriff auf das Konto gewährt wurde, unter dem der Merge-Agent (bei der Mergereplikation) oder der Verteilungs-Agent (bei der Momentaufnahme- oder Transaktionsreplikation) ausgeführt wird. Stellen Sie außerdem sicher, dass dem Konto, unter dem der Momentaufnahme-Agent ausgeführt wird, Schreibzugriff gewährt wurde. Weitere Informationen zum momentaufnahmeordner finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## Siehe auch  
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz & #40; Replikation & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  