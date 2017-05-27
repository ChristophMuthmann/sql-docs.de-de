---
title: "Help Viewer für SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fc2435ccea3b01328c3c4623e62fbf12ee53e400
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="help-viewer-for-sql-server"></a>Help Viewer für SQL Server
  
  
  
Dieser Artikel führt Sie durch die Installation der lokalen Hilfe und das Anzeigen von Online-Hilfe und lokaler Hilfe. Der Artikel befasst sich mit Microsoft Help Viewer 1.1 und 2.2 sowie den Dokumentationen für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] und [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]. 

>[!IMPORTANT]
>Der Help Viewer unterstützt Proxyeinstellungen und das ISO-Format nicht.  

>**F1 und Help**
>>Wenn Sie F1 drücken, wird das entsprechende Thema online angezeigt. Das Thema kann nicht in der lokalen Hilfe angezeigt werden.

## <a name="includesscurrentmdincludessscurrent-mdmd-and-help-viewer-22"></a>[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] und Help Viewer 2.2  
Help Viewer 2.2 ist in [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio ab April 2016 Preview (13.0.12500.29) und in Visual Studio 2015 verfügbar.  

> [![Herunterladen von SSMS](../release-notes/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) Laden Sie die neueste Version von **[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) herunter.**  

**Installieren der lokalen Hilfe zur Verwendung mit Help Viewer 2.2**  
1. Öffnen Sie Help Viewer 2.2, indem Sie SQL Server Management Studio oder Visual Studio starten und im Menü **Hilfe** auf **Hilfeinhalt hinzufügen und entfernen** klicken.  
2. Klicken Sie auf die Registerkarte **Inhalt verwalten**.  
3. Klicken Sie zum Installieren der Hilfe von einer Onlinequelle im Bereich **Installationsquelle** auf **Online**.  
![HelpViewer2_ManageContent_OnlineSource](../release-notes/media/helpviewer2-managecontent-onlinesource.png)  
7. Klicken Sie neben der Dokumentation, die Sie installieren möchten, auf **Hinzufügen** und dann auf **Aktualisieren**.  
![HelpViewer2_ManageContent_AddContent](../release-notes/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >In SQL Server Management Studio und Visual Studio kann die Anwendung Help Viewer während des Hinzufügens der Dokumentation einfrieren (hängenbleiben). Gehen Sie zur Lösung des Problems wie folgt vor: Weitere Informationen zu diesem Problem finden Sie unter [Visual Studio Help Viewer friert beim Begrüßungsbildschirm ein](https://msdn.microsoft.com/library/mt654096.aspx).  
   >>Öffnen Sie die Datei „%LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings“ | „HlpViewer_VisualStudio14_en-US.settings“ im Editor, und ändern Sie das Datum im folgenden Code in einen Zeitpunkt in der Zukunft. Diese Datei ist auf dem lokalen Computer nur verfügbar, wenn Sie Visual Studio installiert haben. 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    Das Inhaltsverzeichnis im linken Bereich wird automatisch um die Dokumentation aktualisiert, die Sie hinzugefügt haben.  
![HelpViewer2_withContentInstalled](../release-notes/media/helpviewer2-withcontentinstalled.png)

1. (Optional) Das Feld **Lokaler Speicherpfad** auf der Registerkarte **Inhalt verwalten** zeigt, wo die Dokumentation auf dem lokalen Computer installiert wird. Wenn Sie die Dokumentation an einen anderen Speicherort verschieben möchten, klicken Sie auf **Verschieben**, geben Sie im Dialogfeld **Inhalt verschieben** in das Feld **To** (Nach) einen Ordnerpfad ein, und klicken Sie dann auf **Ok**.

   ![HelpViewer2_Move Content Dialog](../release-notes/media/helpviewer2-move-content-dialog.png)

   Nach dem Verschieben des Inhalts wird der neue Speicherort unter **Lokaler Speicherpfad** angezeigt.
      
   >[!IMPORTANT]
   > Wenn eine Meldung angezeigt wird, die angibt, dass der Verschiebevorgang fehlgeschlagen ist, schließen Sie das Meldungsfeld und den Help Viewer, und öffnen Sie dann den Help Viewer erneut. Der neue Speicherort für den Inhalt sollte nun unter **Lokaler Speicherpfad** angezeigt werden.   
  
**Anzeigen von lokaler Hilfe oder Onlinehilfe in SQL Server Management Studio**  
* Klicken Sie zum Anzeigen lokaler Hilfe im Menü **Hilfe** auf **Hilfeinhalt hinzufügen und entfernen** und dann auf die Registerkarte **Help Viewer – Startseite**, um die Dokumentation anzuzeigen.  
    >[!NOTE]
    >Der Text **Help Viewer – Startseite** ändert sich je nachdem welches Thema Sie im Inhaltsverzeichnis angeklickt haben.   
* Klicken Sie zum Anzeigen von Onlinehilfe im Menü **Hilfe** auf **Hilfe anzeigen**. Die Dokumentation wird in einem Browser angezeigt.  
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)  
  
  
**Anzeigen von lokaler Hilfe oder Onlinehilfe in Visual Studio**  
* Klicken Sie im Menü **Hilfe** auf **Help Set Preference** (Hilfeeinstellungen festlegen), und führen Sie eine der folgenden Aktionen aus.  
   * Klicken Sie auf **Im Browser starten**, um die Onlinehilfe anzuzeigen. Wenn Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken, wird die Dokumentation in einem Browser angezeigt.  
   * Klicken Sie auf **In Help Viewer starten**, um die lokale Hilfe anzuzeigen. Wenn Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken, wird die Dokumentation im Help Viewer angezeigt.  
     
     ![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)  
  
  
## <a name="includesssql14mdincludessssql14-mdmd-and-help-viewer-11"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] und Help Viewer 1.1  
 Help Viewer 1.1 ist in [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Management Studio und Versionen von Visual Studio vor Visual Studio 2012 verfügbar.   
 
>[!NOTE]
> Sie können auch lokale Hilfe für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] anzeigen und Help Viewer 2.2 nur verwenden, wenn Sie **Inhalt von einem Datenträger installieren**. Help Viewer 2.2 ist in [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio ab April 2016 Preview (13.0.12500.29) und in Visual Studio 2015 verfügbar. 
   
**Installieren der lokalen Hilfe zur Verwendung mit Help Viewer 1.1**  
1. Navigieren Sie zur [Downloadwebsite](https://www.microsoft.com/en-us/download/details.aspx?id=42557) für die Hilfeinhalte, und klicken Sie auf **Download**.  
2. Klicken Sie im Meldungsfeld auf **Speichern**, um die Datei „SQLServer2014Documentation_*.exe“ auf Ihrem Computer zu speichern.  
   >[!NOTE]
   >Speichern Sie bei firewall- und proxygeschützten Umgebungen die Downloaddatei auf einem USB-Laufwerk oder anderen Wechselmedium, auf das in der Umgebung zugegriffen werden kann.   
3. Doppelklicken Sie auf die EXE-Datei, um die Datei mit Hilfeinhalten zu entpacken und in einem lokalen oder freigegebenen Ordner zu speichern.  
4. Öffnen Sie den **Hilfebibliotheks-Manager**, indem Sie SQL Server Management Studio oder Visual Studio starten und im Menü **Hilfe** auf **Hilfeeinstellungen verwalten** klicken.  
7. Klicken Sie auf **Inhalt von Datenträger installieren**, und suchen Sie den Ordner, in den Sie die Datei mit Hilfeinhalten entpackt haben.  
  
Wählen Sie „Inhalt von Datenträger installieren“ aus  |Navigieren Sie zur Datei mit Hilfeinhalten   
---------|---------  
![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
>[!IMPORTANT]
> Verwenden Sie im **Hilfebibliotheks-Manager** die Option **Inhalt von Datenträger installieren**, um zu vermeiden, dass lokale Hilfeinhalte installiert werden, bei denen das Inhaltsverzeichnis nur teilweise vorhanden ist.  
>>Wenn Sie die Option **Inhalt von Onlinespeicherort installieren** gewählt haben und der Help Viewer das Inhaltsverzeichnis nur teilweise anzeigt, finden Sie in diesem [Blogbeitrag](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) Schritte zur Fehlerbehebung. 

8. Klicken Sie auf die Datei „HelpContentSetup.msha“, klicken Sie dann auf **Öffnen** und dann auf **Weiter**.  
9. Klicken Sie neben der Dokumentation, die Sie installieren möchten, auf **Hinzufügen** und dann auf **Aktualisieren**.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. Klicken Sie auf **Fertig stellen** und dann auf **Beenden**. Öffnen Sie den Help Viewer zum Anzeigen des Inhalts, indem Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken. Der Inhalt, den Sie installiert haben, sollte nun im Inhaltsverzeichnis im linken Bereich angezeigt werden.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
**Anzeigen von lokaler Hilfe oder Onlinehilfe**  
1. Öffnen Sie den **Hilfebibliotheks-Manager**, indem Sie im Menü **Hilfe** auf **Hilfeeinstellungen verwalten** klicken.  
2. Klicken Sie im Dialogfeld **Hilfebibliotheks-Manager** auf **Onlinehilfe oder lokale Hilfe auswählen**.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. Führen Sie eine der folgenden Aktionen aus, klicken Sie auf **OK** und dann auf **Beenden**.  
   * Klicken Sie auf **Ich möchte Onlinehilfe verwenden**.  
   * Klicken Sie auf **Ich möchte lokale Hilfe verwenden**.  
  
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)  
  
Wenn Sie die Onlinehilfe gewählt haben und im Menü **Hilfe** auf **Hilfe anzeigen** klicken, wird der Browser gestartet und der Artikel [Onlinedokumentation für SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx) auf MSDN angezeigt. Wenn Sie die lokale Hilfe gewählt haben, wird durch Klicken auf **Hilfe anzeigen** der Help Viewer gestartet.  

## <a name="additional-information"></a>Zusätzliche Informationen
[Microsoft Help Viewer – Visual Studio 2015](https://msdn.microsoft.com/library/hh580782.aspx)

