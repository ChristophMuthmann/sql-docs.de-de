---
title: "Verwalten von Anmeldungen in der Ver&#246;ffentlichungszugriffsliste | Microsoft Docs"
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
  - "Anmeldungen [SQL Server-Replikation], Veröffentlichungszugriffsliste"
  - "Veröffentlichungen [SQL Server-Replikation], Veröffentlichungszugriffslisten"
  - "Veröffentlichungszugriffsliste (PAL)"
  - "PAL (Publication Access List, Veröffentlichungszugriffsliste)"
  - "Anmeldungen [SQL Server-Replikation], verwalten"
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Verwalten von Anmeldungen in der Ver&#246;ffentlichungszugriffsliste
  In diesem Thema wird beschrieben, wie Anmeldungen in der Veröffentlichungszugriffsliste in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]verwaltet werden. Der Zugriff auf eine Veröffentlichung wird von der Veröffentlichungszugriffsliste (Publication Access List, PAL) gesteuert. Anmeldungen und Gruppen können hinzugefügt und aus PAL entfernt werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
-   **So verwalten Sie Anmeldungen in der Veröffentlichungszugriffsliste mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen einem Datenbankbenutzer in der Veröffentlichungsdatenbank die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung zuordnen, bevor Sie die Anmeldung PAL hinzufügen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Sie verwenden die veröffentlichungszugriffsliste (PAL) auf den **Publikationszugriffsliste** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld zum Verwalten der Anmeldenamen. Weitere Informationen dazu, wie Sie dieses Dialogfelds finden Sie unter [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So verwalten Sie Anmeldenamen in der Veröffentlichungszugriffsliste  
  
1.  Auf der **Publikationszugriffsliste** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Verwenden Sie im Dialogfeld die **Hinzufügen**, **Entfernen**, und **Alle entfernen** Schaltflächen hinzufügen und Entfernen von Anmeldungen und Gruppen aus der PAL. Entfernen Sie nicht **Distributor_admin** aus der PAL. Dieses Konto wird für die Replikation verwendet.  
  
    > [!NOTE]  
    >  Wenn ein Remoteverteiler verwendet wird, müssen Konten in der PAL sowohl beim Verleger als auch beim Verteiler verfügbar sein. Das Konto muss entweder ein Domänenkonto oder ein lokales Konto sein, das auf beiden Servern definiert ist. Die den Anmeldenamen zugehörigen Kennwörter müssen übereinstimmen.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So zeigen Sie Gruppen und Anmeldungen an, die zur PAL gehören  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md). Geben Sie für **@publication**den Veröffentlichungsnamen an. Dadurch werden Informationen über die Gruppen und Anmeldungen in der PAL angezeigt.  
  
#### So fügen Sie der PAL Gruppen und Anmeldungen hinzu  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md). Geben Sie den Veröffentlichungsnamen für **@publication**an. Geben Sie den Namen der Anmeldung oder Gruppe, die hinzugefügt wird, für **@login**an.  
  
#### So entfernen Sie Gruppen und Anmeldungen aus der PAL  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md). Geben Sie den Veröffentlichungsnamen für **@publication**an. Geben Sie den Namen der Anmeldung oder Gruppe, die entfernt wird, für **@login**an.  
  
## Siehe auch  
 [Verwalten von Anmeldungen in der Veröffentlichungszugriffsliste](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [Sicherheitsmodell des Replikations-Agents](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Sichern einer Replikationstopologie](../../../relational-databases/replication/security/secure-a-replication-topology.md)   
 [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  