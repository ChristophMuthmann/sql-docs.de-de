---
title: Anzeigen von Offlineprotokolldateien | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Log File Viewer, viewing offline logs
- offline log files
ms.assetid: 9223e474-f224-4907-a4f2-081e11db58f5
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2fbac24caac2af64ba28178a1cfebd9bd860581d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-offline-log-files"></a>Anzeigen von Offlineprotokolldateien
  Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokolldateien von einer lokalen oder Remoteinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzeigen, wenn die Zielinstanz offline ist oder nicht gestartet werden kann.  
  
 Auf die Offlineprotokolldateien können Sie von Registrierte Server oder programmgesteuert mit WMI- und WQL (WMI Query Language)-Abfragen zugreifen.  
  
> [!NOTE]  
>  Mit diesen Methoden können Sie auch eine Verbindung mit einer Onlineinstanz herstellen, aber aus einem bestimmten Grund nicht über eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindung.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Zum Herstellen einer Verbindung mit Offlineprotokolldateien muss eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer installiert sein, den Sie zum Anzeigen der Offlineprotokolldateien verwenden möchten, und außerdem auf dem Computer, auf dem sich die Protokolldateien befinden, die Sie anzeigen möchten. Wenn auf beiden Computern eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist, können Sie Offlinedateien für Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sowie für Instanzen anzeigen, von denen frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem der Computer ausgeführt werden.  
  
 Wenn Sie Registrierte Server verwenden, muss die Instanz, mit der Sie eine Verbindung herstellen möchten, unter **Lokale Servergruppen** oder **Zentrale Verwaltungsserver**registriert sein. (Die Instanz kann eigenständig oder als Mitglied einer Servergruppe registriert werden.) Weitere Informationen zum Hinzufügen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu Registrierte Server finden Sie in den folgenden Themen:  
  
-   [Erstellen oder Bearbeiten einer Servergruppe &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrieren eines verbundenen Servers &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/register-a-connected-server-sql-server-management-studio.md)  
  
-   [Erstellen eines zentralen Verwaltungsservers und einer Servergruppe &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)  
  
 Weitere Informationen zum programmgesteuerten Anzeigen der Offlineprotokolldateien mit WMI- und WQL-Abfragen finden Sie in den folgenden Themen:  
  
-   [SqlErrorLogEvent Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md) (Dieses Thema veranschaulicht das Abrufen von Werten für protokollierte Ereignisse in einer angegebenen Protokolldatei.)  
  
-   [SqlErrorLogFile Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md) (Dieses Thema veranschaulicht das Abrufen von Informationen zu allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokolldateien für eine angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
##  <a name="BeforeYouBegin"></a> Berechtigungen  
 Wenn Sie eine Verbindung mit einer Offlineprotokolldatei herstellen möchten, müssen Sie auf dem lokalen und dem Remotecomputer über die folgenden Berechtigungen verfügen:  
  
-   Lesezugriff auf den **Root\Microsoft\SqlServer\ComputerManagement12** -WMI-Namespace. Standardmäßig verfügt jeder Benutzer durch die Berechtigung Konto aktivieren über Lesezugriff. Weitere Informationen finden Sie im Verfahren "So überprüfen Sie WMI-Berechtigungen" weiter unten in diesem Abschnitt.  
  
-   Leseberechtigung für den Ordner mit den Fehlerprotokolldateien. Standardmäßig befinden sich die Fehlerprotokolldateien unter dem folgenden Pfad (wobei <\<*Laufwerk>*das Laufwerk darstellt, auf dem Sie installiert haben[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und\<*<Instanzname* den Namen der Instanz von[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] darstellt):  
  
     **\<Laufwerk>:\Programme\Microsoft SQL Server\MSSQL13.\<Instanzname>\MSSQL\Log**  
  
 Zum Überprüfen der Sicherheitseinstellungen für den WMI-Namespace können Sie das Snap-In WMI-Kontrolle verwenden.  
  
#### <a name="to-verify-wmi-permissions"></a>So überprüfen Sie WMI-Berechtigungen  
  
1.  Öffnen Sie das Snap-In WMI-Kontrolle. Führen Sie dazu je nach Betriebssystem eine der folgenden Aktionen aus:  
  
    -   Klicken Sie im **Startmenü** auf **Suche starten**, geben Sie **wmimgmt.msc** ein, und drücken Sie dann die EINGABETASTE.  
  
    -   Klicken Sie auf **Start**, dann auf **Ausführen**, geben Sie **wmimgmt.msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Standardmäßig wird mit dem Snap-In WMI-Kontrolle der lokale Computer verwaltet.  
  
     Wenn Sie eine Verbindung mit einem Remotecomputer herstellen möchten, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **WMI-Kontrolle (Lokal)**, und klicken Sie dann auf **Verbindung mit anderem Computer herstellen**.  
  
    2.  Klicken Sie im Dialogfeld **Verwalteten Computer ändern** auf **Anderem Computer**.  
  
    3.  Geben Sie den Namen des Remotecomputers ein, und klicken Sie dann auf **OK**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **WMI-Steuerung (Lokal)** oder **WMI-Steuerung (***Remotecomputername***)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie im Dialogfeld **Eigenschaften von WMI-Kontrolle** auf die Registerkarte **Sicherheit** .  
  
5.  Suchen Sie in der Namespacestruktur den folgenden Namespace, und klicken Sie auf diesen:  
  
     **Root\Microsoft\SqlServer\ComputerManagement10**  
  
6.  Klicken Sie auf **Sicherheit**.  
  
7.  Stellen Sie sicher, dass das verwendete Konto über die Berechtigung **Konto aktivieren** verfügt. Diese Berechtigung erlaubt den Lesezugriff auf WMI-Objekte.  
  
### <a name="view-log-files"></a>Anzeigen von Protokolldateien  
 Das folgende Verfahren veranschaulicht das Anzeigen von Offlineprotokolldateien über Registrierte Server. Dabei wird Folgendes vorausgesetzt:  
  
 Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mit der Sie eine Verbindung herstellen möchten, wurde bereits in Registrierte Server registriert.  
  
##### <a name="to-view-log-files-for-instances-that-are-offline"></a>So zeigen Sie Protokolldateien für Offlineinstanzen an  
  
1.  Wenn Sie Offlineprotokolldateien für eine lokale Instanz anzeigen möchten, stellen Sie sicher, dass Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit erhöhten Berechtigungen starten. Dazu klicken Sie beim Starten von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]mit der rechten Maustaste auf **SQL Server Management Studio**, und klicken Sie dann auf **Als Administrator ausführen**.  
  
2.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Ansicht** auf **Registrierte Server**.  
  
3.  Suchen Sie in der Konsolenstruktur die Instanz, in der Sie die Offlinedateien anzeigen möchten.  
  
4.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Wenn die Instanz unter **Lokale Servergruppen**aufgeführt wird, erweitern Sie **Lokale Servergruppen**und die Servergruppe (wenn die Instanz Mitglied einer Gruppe ist), klicken Sie mit der rechten Maustaste auf die Instanz, und klicken Sie dann auf **SQL Server-Protokoll anzeigen**.  
  
    -   Wenn es sich bei der Instanz um den zentralen Verwaltungsserver selbst handelt, erweitern Sie **Zentrale Verwaltungsserver**, klicken Sie mit der rechten Maustaste auf die Instanz, zeigen Sie auf **Aktionen des zentralen Verwaltungsservers**, und klicken Sie dann auf **SQL Server-Protokoll**anzeigen.  
  
    -   Wenn die Instanz unter **Zentrale Verwaltungsserver**aufgeführt wird, erweitern Sie **Zentrale Verwaltungsserver**und den zentralen Verwaltungsserver, klicken Sie mit der rechten Maustaste auf die Instanz (oder erweitern Sie eine Servergruppe, und klicken Sie mit der rechten Maustaste auf die Instanz), und klicken Sie dann auf **SQL Server-Protokoll anzeigen**.  
  
5.  Wenn Sie eine Verbindung mit einer lokalen Instanz herstellen, wird die Verbindung mit den aktuellen Benutzeranmeldeinformationen hergestellt.  
  
     Wenn Sie eine Verbindung mit einer Remoteinstanz herstellen, führen Sie im Dialogfeld **Protokolldatei-Viewer – Verbinden als** eine der folgenden Aktionen aus:  
  
    -   Wenn Sie eine Verbindung als der aktuelle Benutzer herstellen möchten, stellen Sie sicher, dass das Kontrollkästchen **Als anderer Benutzer verbinden** deaktiviert ist, und klicken Sie dann auf **OK**.  
  
    -   Wenn Sie eine Verbindung als ein anderer Benutzer herstellen möchten, aktivieren Sie das Kontrollkästchen **Als anderer Benutzer verbinden** , und klicken Sie dann auf **Benutzer festlegen**. Wenn Sie dazu aufgefordert werden, geben Sie die Benutzeranmeldeinformationen ein (mit dem Benutzernamen im Format *Domänenname*\\*Benutzername*), klicken Sie auf **OK**, und klicken Sie dann erneut auf **OK** , um eine Verbindung herzustellen.  
  
    > [!NOTE]  
    >  Wenn das Laden der Protokolldateien zu lange dauert, können Sie auf der Symbolleiste des Protokolldatei-Viewers auf **Beenden** klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [Protokolldatei-Viewer](../../relational-databases/logs/log-file-viewer.md)  
  
  
