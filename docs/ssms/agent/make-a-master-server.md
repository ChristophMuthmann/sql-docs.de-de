---
title: Einrichten eines Masterservers | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 99f55a30de01a0f9848b8f1c1f4f75e3d3c3fe3c
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="make-a-master-server"></a>Einrichten eines Masterservers
In diesem Thema wird beschrieben, wie Sie mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] einen [!INCLUDE[tsql](../../includes/tsql_md.md)]-Masterserver einrichten.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **Einrichten eines Masterservers mit:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Sicherheit  
Verteilte Aufträge mit Schritten, die einem Proxy zugeordnet sind, werden im Kontext des Proxykontos auf dem Zielserver ausgeführt. Stellen Sie sicher, dass die folgenden Bedingungen erfüllt sind, da andernfalls einem Proxy zugeordnete Auftragsschritte nicht vom Masterserver auf den Zielserver heruntergeladen werden:  
  
-   Der Registrierungsunterschlüssel des Masterservers **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) wird auf 1 (true) festgelegt. Dieser Unterschlüssel ist standardmäßig auf 0 (false) festgelegt.  
  
-   Auf dem Zielserver ist ein Proxykonto vorhanden, das den gleichen Namen wie das Proxykonto des Masterservers hat, unter dem der Auftragsschritt ausgeführt wird.  
  
Falls bei Auftragsschritten, die Proxykonten verwenden, beim Herunterladen vom Masterserver auf den Zielserver ein Fehler auftritt, können Sie die **error_message** -Spalte in der **sysdownloadlist** -Tabelle der **msdb** -Datenbank auf die folgenden Fehlermeldungen überprüfen:  
  
-   "Für den Auftragsschritt ist ein Proxykonto erforderlich, das Proxyabgleichen ist auf dem Zielserver aber deaktiviert."  
  
    Um diesen Fehler zu beheben, legen Sie den Registrierungsunterschlüssel **AllowDownloadedJobsToMatchProxyName** auf 1 fest.  
  
-   "Proxy nicht gefunden."  
  
    Um diesen Fehler zu beheben, stellen Sie sicher, dass auf dem Zielserver ein Proxykonto vorhanden ist, das den gleichen Namen wie das Proxykonto des Masterservers hat, unter dem der Auftragsschritt ausgeführt wird.  
  
#### <a name="Permissions"></a>Berechtigungen  
Berechtigungen zur Ausführung dieser Prozedur erhalten standardmäßig Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-make-a-master-server"></a>So richten Sie einen Masterserver ein  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, zeigen Sie auf **Multiserveradministration**, und klicken Sie dann auf **Als Masterserver einrichten**. Der **Masterserver-Assistent** führt Sie durch die Schritte zum Einrichten eines Masterservers und Hinzufügen eines Zielservers.  
  
3.  Konfigurieren Sie auf der Seite **Masterserveroperator** einen Operator, damit der Masterserver Benachrichtigungen per E-Mail oder mittels Pager an Operatoren sendet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent muss zum Senden von E-Mails konfiguriert werden. Um Operatoren die Benachrichtigungen mithilfe von **NET SEND**zu senden, muss auf dem Server mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent der Messenger-Dienst ausgeführt werden.  
  
    **E-Mail-Adresse**  
    Legt die E-Mail-Adresse des Operators fest.  
  
    **Pageradresse**  
    Legt die Pager-E-Mail-Adresse des Operators fest.  
  
    **NET SEND-Adresse**  
    Legt die **NET SEND** -Adresse des Operators fest.  
  
4.  Wählen Sie auf der Seite **Zielserver** Zielserver für den Masterserver aus.  
  
    **Registrierte Server**  
    Listet die in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] registrierten Server auf, die noch nicht als Zielserver festgelegt wurden.  
  
    **Zielserver**  
    Listet die Server auf, die Zielserver sind.  
  
    **>**  
    Verschiebt den ausgewählten Server in die Liste mit den Zielservern.  
  
    **>>**  
    Verschiebt alle Server auf die Zielserverliste.  
  
    **<**  
    Entfernt den ausgewählten Server aus der Liste mit den Zielservern.  
  
    **<<**  
    Entfernt alle Server von der Zielserverliste.  
  
    **Verbindung hinzufügen**  
    Fügt der Zielserverliste einen Server hinzu, ohne diesen zu registrieren.  
  
    **Verbindung**  
    Ändert die Verbindungseigenschaften der ausgewählten Server.  
  
5.  Geben Sie auf der Seite **Masterserver-Anmeldeinformationen** an, ob für den Zielserver ein neuer Anmeldename erstellt werden soll, und weisen Sie ihm ggf. Rechte für den Masterserver zu.  
  
    **Bei Bedarf eine neue Anmeldung erstellen und ihr Rechte für MSX zuweisen**  
    Erstellt eine neue Anmeldung auf dem Zielserver, sofern die angegebene Anmeldung noch nicht vorhanden ist.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>So richten Sie einen Masterserver ein  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde_md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im folgenden Beispiel wird der aktuelle Server auf dem Masterserver "AdventureWorks1" eingetragen. Der Speicherort für den aktuellen Server ist "Building 21, Room 309, Rack 5".  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
Weitere Informationen finden Sie unter [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f).  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen einer Multiserverumgebung](../../ssms/agent/create-a-multiserver-environment.md)  
[Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  

