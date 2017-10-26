---
title: "Servereigenschaften (Seite „Sicherheit“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bfad12622d6f86101b5a9e8d192922424e5f7171
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="server-properties---security-page"></a>Servereigenschaften (Seite „Sicherheit“)
  Auf dieser Seite können Sie die Optionen für die Serversicherheit anzeigen oder bearbeiten.  
  
## <a name="server-authentication"></a>Serverauthentifizierung  
 **Windows-Authentifizierungsmodus**  
 Verwendet die Windows-Authentifizierung zum Überprüfen von Verbindungsversuchen. Wenn beim Ändern des Sicherheitsmodus kein Kennwort für **sa** festgelegt ist, wird der Benutzer zur Eingabe des Kennworts für **sa** aufgefordert.  
  
> [!IMPORTANT]  
>  Die Windows-Authentifizierung bietet deutlich mehr Sicherheit als die SQL Server-Authentifizierung. Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
 **SQL Server- und Windows-Authentifizierungsmodus**  
 Verwendet aus Gründen der Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]einen gemischten Authentifizierungsmodus zum Überprüfen von Verbindungsversuchen. Wenn beim Ändern des Sicherheitsmodus kein Kennwort für **sa** festgelegt ist, wird der Benutzer zur Eingabe des Kennworts für **sa** aufgefordert.  
  
> [!NOTE]  
>  Das Ändern der Sicherheitskonfiguration erfordert einen Neustart des Diensts. Beim Ändern des SQL Server- und Windows-Authentifizierungsmodus wird das SA-Konto nicht automatisch aktiviert. Zum Verwenden des SA-Kontos führen Sie [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) mit der Option ENABLE aus.  
  
## <a name="login-auditing"></a>Anmeldungsüberwachung  
 **Keine**  
 Schaltet die Anmeldungsüberwachung ab.  
  
 **Nur fehlgeschlagene Anmeldungen**  
 Überwacht nur nicht erfolgreiche Anmeldungen.  
  
 **Nur erfolgreiche Anmeldungen**  
 Überwacht nur erfolgreiche Anmeldungen.  
  
 **Erfolgreiche und fehlgeschlagene Anmeldungen**  
 Überwacht alle Anmeldungsversuche.  
  
> [!NOTE]  
>  Eine Änderung der Überwachungsebene erfordert einen Neustart des Diensts.  
  
## <a name="server-proxy-account"></a>Serverproxykonto  
 **Serverproxykonto aktivieren**  
 Aktiviert ein Konto für die Verwendung durch **xp_cmdshell**. Proxykonten ermöglichen den Identitätswechsel bei Anmeldungen, Serverrollen und Datenbankrollen, wenn ein Betriebssystembefehl ausgeführt wird.  
  
> [!CAUTION]  
>  Die vom Serverproxykonto verwendete Anmeldung sollte nur so viele Privilegien besitzen, wie zur Ausführung der vorgesehenen Arbeit erforderlich sind. Zu großzügige Privilegien für das Proxykonto können von einem Benutzer mit bösartigen Absichten zur Beeinträchtigung der Systemsicherheit ausgenutzt werden.  
  
 **Proxykonto**  
 Geben Sie das verwendete Proxykonto an.  
  
 **Kennwort**  
 Geben Sie das Kennwort für das Proxykonto ein.  
  
## <a name="options"></a>Optionen  
 **C2-Überwachungs-Ablaufverfolgung aktivieren**  
 Überwacht alle Zugriffsversuche auf Anweisungen und Objekte und zeichnet diese in einer Datei im Verzeichnis \MSSQL\Data (bei Standardinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) bzw. \MSSQL$*Instanzname*\Data (bei benannten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) auf. Weitere Informationen finden Sie unter [C2-Überwachungsmodus (Serverkonfigurationsoption)](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md).  
  
 **Datenbankübergreifende Besitzverkettung**  
 Wählen Sie diese Option aus, um es der Datenbank zu ermöglichen, Quelle oder Ziel einer datenbankübergreifenden Besitzverkettung zu sein. Weitere Informationen finden Sie unter [Datenbankübergreifende Besitzverkettung (Serverkonfigurationsoption)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  

