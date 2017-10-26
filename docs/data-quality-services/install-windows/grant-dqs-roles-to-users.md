---
title: Zuweisen von DQS-Rollen an Benutzer | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: afb445b5-bdbe-4bfe-844f-344766cdc2b2
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 805020ab366ec0e993c8f4be54a4d18a22510911
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-dqs-roles-to-users"></a>Zuweisen von DQS-Rollen an Benutzer
  In diesem Thema wird beschrieben, wie SQL-Anmeldungen auf Grundlage eines Windows-Prinzipals erstellt werden und wie ihnen [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS)-Rollen für die DQS_MAIN-Datenbank gewährt werden.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen die Installation des [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] durch Ausführen der Datei DQSInstaller.exe abgeschlossen haben. Weitere Informationen finden Sie unter [Ausführen von DQSInstaller.exe zum Abschließen der Installation von Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
-   Ihr Windows-Benutzerkonto muss Mitglied der entsprechenden festen Serverrolle (z. B. securityadmin, serveradmin, sysadmin) sein, um eine SQL-Anmeldung zu erstellen und ihr DQS-Rollen zuzuweisen.  
  
### <a name="to-create-sql-login-and-grant-dqs-roles"></a>So erstellen Sie eine SQL-Anmeldung und gewähren DQS-Rollen  
  
1.  Starten Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die SQL Server-Instanz, und erweitern Sie dann **Sicherheit**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Sicherheit** , zeigen Sie auf **Neu**, und wählen Sie dann **Anmeldung**aus.  
  
4.  Geben Sie im Dialogfeld **Anmeldung – Neu** den Namen eines Windows-Benutzers im Feld **Anmeldename** ein, geben Sie für den Authentifizierungstyp **Windows-Authentifizierung**an, und klicken Sie auf **Suchen** , um den Benutzer zu überprüfen.  
  
5.  Klicken Sie nach der Überprüfung des Benutzers auf die Seite **Benutzerzuordnung** im linken Bereich.  
  
6.  Aktivieren Sie im rechten Bereich das Kontrollkästchen unter der Spalte **Zuordnen** für die **DQS_MAIN** -Datenbank, und aktivieren Sie dann das Kontrollkästchen **dqs_administrator**, **dqs_kb_editor**oder **dqs_kb_operator** im Bereich **Mitgliedschaft in Datenbankrolle für: DQS_MAIN** , je nachdem, welche Zugriffsebene für den Benutzer benötigt wird. Weitere Informationen zu den drei DQS-Rollen finden Sie unter [DQS Security](../../data-quality-services/dqs-security.md).  
  
7.  Klicken Sie im Dialogfeld **Anmeldung - Neu** auf **OK** , um die Änderungen zu übernehmen.  
  
    > [!NOTE]  
    >  Wenn Sie einem Benutzer die **dqs_administrator** -Rolle gewähren, übernehmen Sie die Änderungen, und überprüfen Sie dann erneut die Benutzerberechtigungen und ob die beiden anderen Kontrollkästchen für DQS-Rollen (**dq_kb_editor** und **dqs_kb_operator**) auch aktiviert sind.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Melden Sie sich mit dem soeben erstellten Windows-Benutzerkonto, dem Sie die DQS-Rolle gewährt haben, beim [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] an.  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Erstellen eines Anmeldenamens](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  

