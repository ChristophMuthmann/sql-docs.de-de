---
title: Remoteserver | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1c662eb0ba6ba239f53b8983864f3d861d21e092
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="remote-servers"></a>Remoteserver
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Remoteserver werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur aus Gründen der Abwärtskompatibilität unterstützt. Neue Anwendungen sollten stattdessen Verbindungsserver verwenden. Weitere Informationen finden Sie unter [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).  
  
 Durch die Konfiguration eines Remoteservers kann ein Client, der eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt hat, eine gespeicherte Prozedur in einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen, ohne eine separate Verbindung einrichten zu müssen. Der mit dem Client verbundene Server nimmt in diesem Fall die Clientanforderung an und sendet die Anforderung im Auftrag des Clients an den Remoteserver. Der Remoteserver verarbeitet die Anforderung und gibt die Ergebnisse an den ursprünglichen Server zurück. Dieser Server übergibt seinerseits die Ergebnisse an den Client. Wenn Sie eine Remoteserverkonfiguration einrichten, sollten Sie auch Sicherheitsaspekte berücksichtigen.  
  
 Wenn Sie eine Serverkonfiguration einrichten möchten, um gespeicherte Prozeduren auf einem anderen Server auszuführen, jedoch keine Remoteserverkonfigurationen vorhanden sind, sollten Sie Verbindungsserver statt Remoteserver verwenden. Sowohl gespeicherte Prozeduren als auch verteilte Abfragen sind mit Verbindungsservern möglich. Auf Remoteservern können hingegen nur gespeicherte Prozeduren ausgeführt werden.  
  
## <a name="remote-server-details"></a>Einzelheiten zu Remoteservern  
 Remoteserver werden paarweise eingerichtet. Wenn Sie ein Remoteserverpaar einrichten möchten, sollten Sie beide Server so konfigurieren, dass sie sich gegenseitig als Remoteserver erkennen.  
  
 In den meisten Fällen ist es nicht erforderlich, Konfigurationsoptionen für Remoteserver festzulegen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] legt die Standardeinstellungen auf den lokalen und Remotecomputern für Remoteserververbindungen fest.  
  
 Damit der Zugriff auf Remoteserver funktioniert, muss die Konfigurationsoption **Remotezugriff** auf den lokalen und den Remotecomputern auf 1 festgelegt werden. (Dies ist die Standardeinstellung.)  **Remotezugriff** steuert Anmeldungen von Remoteservern. Diese Konfigurationsoption können Sie entweder mit der gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** stored procedure or [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn Sie die Option in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]festlegen möchten, verwenden Sie auf der Seite **Verbindungen** die Option **Remoteverbindungen mit diesem Server zulassen**. Um auf die Seite **Verbindungen** zu gelangen, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Servernamen, und klicken Sie auf **Eigenschaften**. Klicken Sie auf der Seite **Servereigenschaften** auf die Seite **Verbindungen** .  
  
 Sie können eine Remoteserverkonfiguration von einem lokalen Server aus deaktivieren, um den Zugriff auf diesen lokalen Server durch Benutzer des diesem zugeordneten Remoteservers zu verhindern.  
  
## <a name="security-for-remote-servers"></a>Sicherheit für Remoteserver  
 Um Remoteprozeduraufrufe (Remote Procedure Calls, RPCs) für einen Remoteserver zu ermöglichen, müssen Sie auf dem Remoteserver sowie gegebenenfalls auf dem lokalen Server, auf dem eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird, Anmeldungszuordnungen einrichten. RPC ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]standardmäßig deaktiviert. Durch diese Konfiguration wird die Angriffsfläche des Servers verkleinert und dadurch die Sicherheit des Servers verbessert. RPC muss aktiviert werden, bevor Sie diese Funktion verwenden können. Weitere Informationen finden Sie unter [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
### <a name="setting-up-the-remote-server"></a>Einrichten des Remoteservers  
 Auf dem Remoteserver müssen Anmeldungszuordnungen eingerichtet werden. Der Remoteserver ordnet über diese Zuordnungen die von einem bestimmten Server eingehende Anmeldung für eine RPC-Verbindung einer lokalen Anmeldung zu. Zuordnungen von Remoteanmeldungen können mithilfe der gespeicherten Prozedur **sp_addremotelogin** auf dem Remoteserver eingerichtet werden.  
  
> [!NOTE]  
>  Die **trusted** -Option von  **sp_remoteoption** wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht unterstützt.  
  
### <a name="setting-up-the-local-server"></a>Einrichten des lokalen Servers  
 Für die lokale Anmeldung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung müssen Sie keine Anmeldungszuordnung auf dem lokalen Server einrichten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet den Anmeldenamen und das Kennwort der lokalen Anmeldung, um die Verbindung mit dem Remoteserver herzustellen. Bei Windows-authentifizierten Anmeldungen richten Sie eine lokale Anmeldungszuordnung auf einem lokalen Server ein, über die definiert wird, welche Anmeldung und welches Kennwort von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verwendet werden, wenn eine RPC-Verbindung mit einem Remoteserver hergestellt wird.  
  
 Bei durch die Windows-Authentifizierung erstellten Anmeldungen müssen Sie eine Anmeldungs- und Kennwortzuordnung über die gespeicherte Prozedur **sp_addlinkedservlogin** erstellen. Diese mithilfe von **sp_addremotelogin**erstellte Anmeldung und dieses Kennwort müssen mit der eingehenden Anmeldung bzw. dem eingehenden Kennwort übereinstimmen.  
  
> [!NOTE]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
### <a name="remote-server-security-example"></a>Beispiel für die Sicherheit von Remoteservern  
 Betrachten Sie diese beiden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationen: **serverSend** und **serverReceive**. **serverReceive** ist so konfiguriert, dass eine eingehende Anmeldung von **serverSend**namens **Sales_Mary**einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -authentifizierten Anmeldung bei **serverReceive**namens **Alice**zugeordnet wird. Eine weitere eingehende Anmeldung von **serverSend** namens **Joe** wird einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-authentifizierten Anmeldung auf **serverReceive**** namens **Joe** zugeordnet.  
  
 Der folgende Transact-SQL-Beispielcode konfiguriert `serverSend` so, dass Remoteprozeduraufrufe auf `serverReceive`ausgeführt werden können.  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 Auf `serverSend`wird eine lokale Anmeldungszuordnung zwischen der Windows-authentifizierten Anmeldung `Sales\Mary` und einer Anmeldung `Sales_Mary`erstellt. Für `Joe`ist keine lokale Anmeldungszuordnung erforderlich, da standardmäßig dieselbe Anmeldung und dasselbe Kennwort verwendet werden und `serverReceive` über eine Zuordnung für `Joe`verfügt.  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>Anzeigen der Eigenschaften von lokalen Servern oder Remoteservern  
 Sie können die erweiterte gespeicherte Prozedur **xp_msver** verwenden, um Serverattribute von lokalen oder Remoteservern zu überprüfen. Diese Attribute enthalten die Versionsnummer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Typ und Anzahl von Prozessoren des Computers, sowie die Version des Betriebssystems. Sie können vom lokalen Server Datenbanken, Dateien, Anmeldungen und Tools eines Remoteserver anzeigen. Weitere Informationen finden Sie unter [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [Konfigurieren der Serverkonfigurationsoption Remotezugriff](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
