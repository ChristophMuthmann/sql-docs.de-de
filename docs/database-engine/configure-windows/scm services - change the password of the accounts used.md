---
title: "&#196;ndern des Kennworts der von SQL Server verwendeten Konten (SQL Server-Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abgelaufenes Kennwort [SQL Server], SQL Server-Agent"
  - "Kennwörter [SQL Server], SQL Server-Agent-Dienst"
  - "Kennwörter [SQL Server], ändern"
  - "Abgelaufenes Kennwort [SQL Server], Datenbankmodul"
  - "Kennwörter [SQL Server], SQL Server-Dienst"
  - "Datenbankmodul [SQL Server], Kennwörter"
  - "Ändern der von SQL Server verwendeten Kennwörter"
  - "Ändern von Kennwörtern"
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# &#196;ndern des Kennworts der von SQL Server verwendeten Konten (SQL Server-Konfigurations-Manager)
  In diesem Thema wird beschrieben, wie Sie das Kennwort der vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendeten Konten mithilfe des SQL Server-Konfigurations-Managers ändern können. Das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent werden auf einem Computer als Dienst ausgeführt, der Anmeldeinformationen verwendet, die während des Setups hinterlegt wurden. Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter einem Domänenkonto ausgeführt wird und das Kennwort für dieses Konto geändert wird, muss das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendete Kennwort auf das neue Kennwort aktualisiert werden. Wird das Kennwort nicht aktualisiert, verliert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise den Zugriff auf einige Domänenressourcen. Wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet, kann der Dienst erst wieder neu gestartet werden, wenn das Kennwort aktualisiert wurde.  
  
 Informationen zum Ändern der Kennwörter für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung finden Sie unter [Kennwort abgelaufen](../../ssms/f1-help/password-expired.md).  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ist das Tool, das zum Ändern der Einstellungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste entwickelt und autorisiert wurde. Wenn Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst mithilfe des Dienststeuerungs-Managers von Windows (**services.msc**) ändern, ändert die Anwendung nicht immer alle erforderlichen Einstellungen und verhindert u. U., dass der Dienst einwandfrei funktioniert. Nachdem Sie in einer Clusterumgebung das Kennwort für den aktiven Knoten mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers geändert haben, müssen Sie das Kennwort für den passiven Knoten jedoch mithilfe des Dienststeuerungs-Managers ändern.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie können nur als Administrator des Computers das von einem Dienst verwendete Konto ändern.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### So ändern Sie das vom SQL Server-Dienst (Datenbankmoduldienst) verwendete Kennwort  
  
1.  Klicken Sie auf **Start** , zeigen Sie auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers auf der **Startseite** Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager zu öffnen, geben Sie im Charm **Suchen** unter **Apps** die Zeichenfolge **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Klicken Sie im SQL Server-Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server (**\<instancename>**)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie im Dialogfeld **Eigenschaften von SQL Server (**\<instancename>**)** auf der Registerkarte „Anmelden“ für das im Feld **Kontoname** angegebene Konto das neue Kennwort in die Felder **Kennwort** und **Kennwort bestätigen** ein, und klicken Sie dann auf **OK**.  
  
     Das Kennwort wird sofort wirksam, ohne dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet werden muss.  
  
#### So ändern Sie das vom SQL Server-Agent-Dienst verwendete Kennwort  
  
1.  Klicken Sie auf **Start** , zeigen Sie auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
2.  Klicken Sie im SQL Server-Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server Agent (**\<instancename>**)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie im Dialogfeld **Eigenschaften von SQL Server-Agent (**\<instancename>**)** auf der Registerkarte „Anmelden“ für das im Feld **Kontoname** angegebene Konto das neue Kennwort in die Felder **Kennwort** und **Kennwort bestätigen** ein, und klicken Sie dann auf **OK**.  
  
     Bei einer eigenständigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz ist das Kennwort sofort wirksam, ohne dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet werden muss. Auf einer gruppierten Instanz kann die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressource von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline geschaltet werden und einen Neustart erfordern.  
  
## Siehe auch  
 [Verwalten von Diensten: Themen zur Vorgehensweise &#40;SQL Server-Konfigurations-Manager&#41;](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)  
  
  