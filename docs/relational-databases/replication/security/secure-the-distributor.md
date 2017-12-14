---
title: "Schützen des Verteilers | Microsoft-Dokumentation"
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
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d4f2511d108c2e461f3ba5ec3e02e43f92ae8d9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="secure-the-distributor"></a>Schützen des Verteilers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die folgenden Replikations-Agents stellen eine Verbindung mit dem Verteiler her: Protokolllese-Agent, Momentaufnahmen-Agent, Warteschlangenlese-Agent, Verteilungs-Agent und Merge-Agent. Es ist wichtig, dass jeder dieser Agents einen geeigneten Anmeldenamen besitzt, dass grundsätzlich nur die minimal erforderlichen Rechte erteilt werden und dass die Speicherung aller Kennwörter geschützt ist:  
  
-   Informationen zum Verwalten von Anmeldungen und Kennwörtern finden Sie unter [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Weitere Informationen zu den für die jeweiligen Agents erforderlichen Berechtigungen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Neben der ordnungsgemäßen Verwaltung von Anmeldenamen und Kennwörtern müssen Sie auch mit der Funktion der **repl_distributor** -Remoteserverlink und der Funktion des **distributor_admin** -Kontos vertraut sein.  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>Schützen der Verbindung vom Verleger zum Verteiler  
 Zur Unterstützung der Kommunikation, die erforderlich ist, wenn administrative gespeicherte Prozeduren auf dem Verleger und Updateinformationen auf dem Verteiler ausgeführt werden, konfiguriert die Replikation den **repl_distributor**-Remoteserver automatisch. Der **repl_distributor** -Remoteservereintrag wird für die Kommunikation mit der Verteilungsdatenbank verwendet, unabhängig davon, ob die Verteilungsdatenbank in der Verlegerinstanz (ein lokaler Verteiler) enthalten ist oder sich in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Remoteinstanz (einem Remoteverteiler) befindet.  
  
 Ist die Verteilungsdatenbank in einer lokalen Instanz enthalten, wird ein zufälliges Kennwort generiert und automatisch konfiguriert. Befindet sich die Verteilungsdatenbank auf einer Remoteinstanz, konfiguriert der Administrator beim Einrichten des Verlegers und Verteilers ein freigegebenes Kennwort. Diese Kennwort dient dann zur Authentifizierung des Datenverkehrs, der den **repl_distributor** -Link durchsucht.  
  
 Der Verteiler verwendet den **repl_distributor** -Remoteservereintrag, um zu überprüfen, ob der aufrufende Server als Verleger auf dem Verteiler konfiguriert ist. Außerdem überprüft er das vom Verleger angegebene Kennwort und ob es sich bei der gespeicherten Prozedur um eine während der Ausführung von der Replikationsverwaltung gespeicherten Prozedur handelt.  
  
 Der beim Setup angegebene **repl_distributor** -Remoteservereintrag wird einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldenamen zugeordnet, **distributor_admin**, der dann der festen Serverrolle **sysadmin** hinzugefügt wird. Die **distributor_admin** -Anmeldung wird von gespeicherten Replikationsprozeduren beim Herstellen der Verbindung zum Verteiler verwendet.  
  
> [!NOTE]  
>  Ändern Sie das Kennwort für **distributor_admin** nicht manuell. Verwenden Sie immer entweder die gespeicherte Prozedur **sp_changedistributor_password** oder die Dialogfelder **Verteilereigenschaften** bzw. **Replikationskennwörter aktualisieren** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], da Kennwortänderungen dann auf lokale Veröffentlichungen automatisch angewendet werden.  
  
## <a name="snapshot-folder-security"></a>Sicherheit des Momentaufnahmeordners  
 Stellen Sie sicher, dass der Momentaufnahmefreigabe Lesezugriff auf das Konto gewährt wurde, unter dem der Merge-Agent (bei der Mergereplikation) oder der Verteilungs-Agent (bei der Momentaufnahme- oder Transaktionsreplikation) ausgeführt wird. Stellen Sie außerdem sicher, dass dem Konto, unter dem der Momentaufnahme-Agent ausgeführt wird, Schreibzugriff gewährt wurde. Weitere Informationen zum Momentaufnahmeordner finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
