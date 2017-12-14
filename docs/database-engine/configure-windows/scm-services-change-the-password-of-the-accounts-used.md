---
title: "SCM-Dienste: Ändern des Kennworts der verwendeten Konten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 04193c3a06fd99a4f69cc4da9d4ae073315963cc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="scm-services---change-the-password-of-the-accounts-used"></a>SCM-Dienste: Ändern des Kennworts der verwendeten Konten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie das Kennwort der vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendeten Konten mithilfe des SQL Server-Konfigurations-Managers ändern können. Das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent werden auf einem Computer als Dienst ausgeführt, der Anmeldeinformationen verwendet, die während des Setups hinterlegt wurden. Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter einem Domänenkonto ausgeführt wird und das Kennwort für dieses Konto geändert wird, muss das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendete Kennwort auf das neue Kennwort aktualisiert werden. Wird das Kennwort nicht aktualisiert, verliert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise den Zugriff auf einige Domänenressourcen. Wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet, kann der Dienst erst wieder neu gestartet werden, wenn das Kennwort aktualisiert wurde.  
  
 Informationen zum Ändern der Kennwörter für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung finden Sie unter [Kennwort abgelaufen](http://msdn.microsoft.com/library/9831b194-9ad5-47b0-8009-59c7aef4319b).  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ist das Tool, das zum Ändern der Einstellungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste entwickelt und autorisiert wurde. Wenn Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst mithilfe des Dienststeuerungs-Managers von Windows (**services.msc**) ändern, ändert die Anwendung nicht immer alle erforderlichen Einstellungen und verhindert u. U., dass der Dienst einwandfrei funktioniert. Nachdem Sie in einer Clusterumgebung das Kennwort für den aktiven Knoten mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers geändert haben, müssen Sie das Kennwort für den passiven Knoten jedoch mithilfe des Dienststeuerungs-Managers ändern.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie können nur als Administrator des Computers das von einem Dienst verwendete Konto ändern.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>So ändern Sie das vom SQL Server-Dienst (Datenbankmoduldienst) verwendete Kennwort  
  
1.  Klicken Sie auf **Start** , zeigen Sie auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Verwaltungskonsolenprogramm und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers auf der **Startseite**Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Apps** im Charm **Suchen** zu öffnen, geben Sie **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Klicken Sie im SQL Server-Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server (**\<Instanzname>**)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie im Dialogfeld **Eigenschaften von SQL Server (**\<Instanzname>**)** auf der Registerkarte „Anmelden“ für das im Feld **Kontoname** angegebene Konto das neue Kennwort in die Felder **Kennwort** und **Kennwort bestätigen** ein, und klicken Sie dann auf **OK**.  
  
     Das Kennwort wird sofort wirksam, ohne dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu gestartet werden muss.  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>So ändern Sie das vom SQL Server-Agent-Dienst verwendete Kennwort  
  
1.  Klicken Sie auf **Start** , zeigen Sie auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
2.  Klicken Sie im SQL Server-Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server Agent (**\<Instanzname>**)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie im Dialogfeld **Eigenschaften von SQL Server-Agent (**\<Instanzname>**)** auf der Registerkarte „Anmelden“ für das im Feld **Kontoname** angegebene Konto das neue Kennwort in die Felder **Kennwort** und **Kennwort bestätigen** ein, und klicken Sie dann auf **OK**.  
  
     Bei einer eigenständigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz ist das Kennwort sofort wirksam, ohne dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu gestartet werden muss. Auf einer gruppierten Instanz kann die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressource von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline geschaltet werden und einen Neustart erfordern.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Diensten: Themen zur Vorgehensweise &#40;SQL Server-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)  
  
  
