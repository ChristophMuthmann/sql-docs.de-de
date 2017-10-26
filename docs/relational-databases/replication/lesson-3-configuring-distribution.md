---
title: 'Lektion 3: Konfigurieren der Verteilung | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e582c5fb7853c69a083755a944bd3922d0d4c5af
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-3-configuring-distribution"></a>Lektion 3: Konfigurieren der Verteilung
In dieser Lektion konfigurieren Sie die Verteilung auf dem Verleger und legen die erforderlichen Berechtigungen für die Verteilungs- und Veröffentlichungsdatenbanken fest. Wenn der Verteiler bereits konfiguriert wurde, müssen die Veröffentlichung und die Verteilung erst deaktiviert werden, bevor Sie mit dieser Lektion beginnen. Führen Sie diese Lektion nicht aus, wenn Sie eine vorhandene Replikationstopologie beibehalten müssen.  
  
Das Konfigurieren eines Verlegers mit einem Remoteverteiler wird in diesem Lernprogramm nicht behandelt.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Konfigurieren der Verteilung auf dem Verleger  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Replikation**, und klicken Sie anschließend auf **Verteilung konfigurieren**.  
  
    > [!NOTE]  
    > Wenn Sie **localhost[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anstelle des tatsächlichen Servernamens verwendet haben, um eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen, werden Sie in einer Warnmeldung darauf hingewiesen, dass**  nicht in der Lage ist, eine Verbindung mit dem Server **"localhost"** herzustellen. Klicken Sie im Warnungsdialogfeld auf **OK**. Ändern Sie im Dialogfeld **Verbindung mit Server herstellen** die Angabe für **Servername** von **localhost** in den Namen des Servers. Klicken Sie auf **Verbinden**.  
  
    Der Verteilungskonfigurations-Assistent wird gestartet.  
  
3.  Wählen Sie auf der Seite **Verteiler** die Option „‚ServerName‘ will act as its own Distributor; SQL Server will create a distribution database and log**“ (‚ServerName‘ als seinen eigenen Verteiler verwenden; SQL Server erstellt eine Verteilungsdatenbank und ein Protokoll**), und klicken Sie anschließend auf **Weiter**.  
  
4.  Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht ausgeführt wird, wählen Sie auf der Seite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agent-Start** die Option **Ja**, den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent zum automatischen Starten konfigurieren. Klicken Sie auf **Weiter**.  
  
5.  Geben Sie im Textfeld **Momentaufnahmeordner** die Zeichenfolge **\\\\**\<*Machine_Name>***\repldata** ein, wobei \<*Machine_Name>* der Name des Verlegers ist, und klicken Sie anschließend auf **Weiter**.  
  
6.  Übernehmen Sie die Standardwerte auf den restlichen Seiten des Assistenten.  
  
7.  Klicken Sie auf **Fertig stellen** , um die Verteilung zu aktivieren.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Festlegen der Datenbankberechtigungen auf dem Verleger  
  
1.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Knoten **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung**aus.  
  
2.  Klicken Sie auf der Seite **Allgemein** auf **Suchen**, geben Sie im Feld **Geben Sie die zu verwendenden Objektnamen ein** die Zeichenfolge \<*Machine_Name>***\repl_snapshot** ein, wobei \<*Machine_Name>* der Name des lokalen Verlegerservers ist. Klicken Sie auf **Namen überprüfen**, und klicken Sie anschließend auf **OK**.  
  
3.  Wählen Sie auf der Seite **Benutzerzuordnung** in der Liste **Benutzer, die dieser Anmeldung zugeordnet sind** sowohl die **Verteilungs** - als auch die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank aus.  
  
    Wählen Sie in der Liste **Mitgliedschaft in Datenbankrolle** die Rolle **db_owner** für die Anmeldung bei beiden Datenbanken aus.  
  
4.  Klicken Sie auf **OK** , um die Anmeldung zu erstellen.  
  
5.  Wiederholen Sie die Schritte 1 bis 4, um eine Anmeldung für das lokale Konto repl_logreader zu erstellen. Diese Anmeldung muss auch Benutzern zugeordnet werden, die Mitglied der festen Datenbankrolle **db_owner** in den Datenbanken **distribution** und **AdventureWorks** sind.  
  
6.  Wiederholen Sie die Schritte 1 bis 4, um eine Anmeldung für das lokale Konto repl_distribution zu erstellen. Diese Anmeldung muss einem Benutzer zugeordnet werden, der Mitglied der festen Datenbankrolle **db_owner** in der Datenbank **distribution** ist.  
  
7.  Wiederholen Sie die Schritte 1 bis 4, um eine Anmeldung für das lokale Konto repl_merge zu erstellen. Diese Anmeldung muss Benutzerzuordnungen in den Datenbanken **distribution** und **AdventureWorks** haben.  
  
## <a name="see-also"></a>Siehe auch  
[Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)  
[Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)  
  
  
  

