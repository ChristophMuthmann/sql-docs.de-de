---
title: Implementieren der SQL Server-Agent-Sicherheit | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 12098ac39d1ede9f304797dc93396c64cfbea6bd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="implement-sql-server-agent-security"></a>Implementieren der SQL Server-Agent-Sicherheit
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent ermöglicht es dem Datenbankadministrator, jeden Auftragsschritt in einem Sicherheitskontext auszuführen, dem lediglich die Berechtigungen erteilt wurden, die zum Durchführen dieses Auftragsschritts erforderlich sind, wie von einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Proxy festgelegt. Um Berechtigungen für einen bestimmten Auftragsschritt festzulegen, erstellen Sie einen Proxy mit den erforderlichen Berechtigungen und weisen dann diesen Proxy dem Auftragsschritt zu. Ein Proxy kann für mehrere Auftragsschritte angegeben werden. Für Auftragsschritte, für die dieselben Berechtigungen erforderlich sind, verwenden Sie denselben Proxy.  
  
Im folgenden Abschnitt wird erläutert, welche Datenbankrolle Sie Benutzern erteilen müssen, damit sie Aufträge mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents erstellen oder ausführen können.  
  
## <a name="granting-access-to-sql-server-agent"></a>Erteilen des Zugriffs auf den SQL Server-Agent  
Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zu verwenden, müssen die Benutzer Mitglied mindestens einer der folgenden festen Datenbankrollen sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Diese Rollen werden in der **msdb** -Datenbank gespeichert. Standardmäßig ist kein Benutzer Mitglied dieser Datenbankrollen. Die Mitgliedschaft in diesen Rollen muss explizit erteilt werden. Benutzer, die Mitglieder der festen Serverrolle **sysadmin** sind, haben vollen Zugriff auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent und müssen nicht Mitglied dieser festen Datenbankrollen sein, um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwenden zu können. Wenn ein Benutzer nicht Mitglied einer dieser Datenbankrollen oder der **sysadmin** -Rolle ist, steht ihm der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten nicht zur Verfügung, wenn er mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Verbindung mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]herstellt.  
  
Die Mitglieder dieser Datenbankrollen können Aufträge anzeigen und ausführen, deren Besitzer sie sind, und Auftragsschritte erstellen, die als bereits vorhandenes Proxykonto ausgeführt werden. Weitere Informationen zu den einzelnen Berechtigungen, die jeder dieser festen Rollen zugeordnet sind, finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Die Mitglieder der festen Serverrolle **sysadmin** haben die Berechtigung zum Erstellen, Ändern und Löschen von Proxykonten. Die Mitglieder der **sysadmin** -Rolle haben die Berechtigung zum Erstellen von Auftragsschritten, die keinen Proxy angeben, sondern stattdessen als das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto ausgeführt werden, bei dem es sich um das Konto handelt, das zum Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents verwendet wird.  
  
## <a name="guidelines"></a>Richtlinien  
Befolgen Sie diese Richtlinien, um die Sicherheit Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Implementierung zu verbessern:  
  
-   Erstellen Sie dedizierte Benutzerkonten speziell für Proxys, und verwenden Sie diese Proxybenutzerkonten nur zum Ausführen von Auftragsschritten.  
  
-   Erteilen Sie die erforderlichen Berechtigungen lediglich den Proxybenutzerkonten. Erteilen Sie lediglich die Berechtigungen, die zum Ausführen der Auftragsschritte erforderlich sind, die einem bestimmten Proxykonto zugewiesen sind.  
  
-   Führen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst nicht unter einem Microsoft Windows-Konto aus, das Mitglied der Windows-Gruppe **Administratoren** ist.  
  
-   Proxys sind nur so sicher wie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Anmeldeinformationenspeicher.  
  
-   Wenn Benutzerschreibvorgänge in das NT-Ereignisprotokoll schreiben können, können sie Warnungen über den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent auslösen.  
  
-   Geben Sie das NT-Adminkonto nicht als Dienst- oder Proxykonto an.  
  
-   Hinweis: [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent können gegenseitig auf ihre Ressourcen zugreifen. Die beiden Dienste verwenden einen einzelnen Prozessraum, und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent fungiert mit der Rolle "sysadmin" auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Dienst.  
  
-   Wenn für ein TSX ein MSX eingetragen wird, erhält die MSX-Rolle "sysadmins" die vollständige Kontrolle über die TSX-Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   ACE ist eine Erweiterung und kann sich nicht selbst aufrufen. ACE wird von der "Chainer ScenarioEngine.exe" (auch als bekannt als "Microsoft.SqlServer.Chainer.Setup.exe") oder einem anderen Hostprozess aufgerufen.  
  
-   ACE hängt von den folgenden Konfigurations-DLL-Elementen ab, die sich im Besitz von SSDP befinden, da diese DLL-APIs von ACE aufgerufen werden:  
  
    -   **SCO** – Microsoft.SqlServer.Configuration.Sco.dll, einschließlich neuer SCO-Überprüfungen für virtuelle Konten  
  
    -   **Cluster** – Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC** – Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **Erweiterung** – Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwenden vordefinierter Rollen](http://msdn.microsoft.com/en-us/6b46db51-7c30-467d-a251-50f50647fe21)  
[sp_addrolemember (Transact-SQL)](http://msdn.microsoft.com/en-us/a583c087-bdb3-46d2-b9e5-3921b3e6d10b)  
[sp_droprolemember (Transact-SQL)](http://msdn.microsoft.com/en-us/c2f19ab1-e742-4d56-ba8e-8ffd40cf4925)  
[Sicherheit und Schutz (Datenbankmodul)](http://msdn.microsoft.com/en-us/dfb39d16-722a-4734-94bb-98e61e014ee7)  
  
