---
title: "Help Viewer und Offlineinhalt für SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: "8"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 048b1d257287b8f0a4645f57ce88c30b24a9f654
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="help-viewer-and-offline-content-for-sql-server"></a>Help Viewer und Offlineinhalt für SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  
  
Dieser Artikel beschreibt, wie Sie den Help Viewer installieren und die SQL Server-Dokumentation offline anzeigen. Dieser Artikel umfasst die Dokumentation für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] SQL Server 2016 und SQL Server 2017. 

## <a name="install-help-viewer"></a>Installieren von Help Viewer
In der folgenden Tabelle sind die Tools aufgeführt, die Help Viewer basierend auf der von Ihnen verwendeten SQL Server-Version installieren. Installieren Sie eines der aufgeführten Tools, um Help Viewer zu installieren.


|**SQL Server-Version**|**Tools, die Help Viewer installieren**|**Version des installierten Help Viewer**|
|---------|---------|---------|
|SQL Server 2017<br>SQL Server 2016     |   [Neueste Version von SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br><br>[Neueste Version von SQL Server Data Tools für Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br><br>Visual Studio 2017 (*unterstützt nur SQL Server 2016*)  |  v2.x       |
|SQL Server 2014    | SQL Server 2014 Management Studio<br><br>Versionen von Visual Studio vor Visual Studio 2012        |  v1.x       |


> [!IMPORTANT]
> SQL Server 2016 installiert Help Viewer 1.1, der nicht zum Anzeigen von Dokumentation für SQL Server 2016 und 2017 verwendet werden kann.
> <br>
> <br>
> SQL Server 2017 installiert nicht Help Viewer.
> <br>
> <br>
> Um Help Viewer mit Visual Studio 2017 zu installieren, klicken Sie auf die Registerkarte **Einzelne Komponenten** im **Visual Studio-Installer**-Programm, klicken Sie anschließend auf **Help Viewer** in der Kategorie **Codetools** und dann auf **Installieren**. 
> <br>
> <br>
> Sie können lokale Hilfe für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] anzeigen und Help Viewer 2.x nur verwenden, wenn Sie **Inhalt von einem Datenträger installieren**. 


## <a name="sql-server-2016-sql-server-2017-offline-content"></a>SQL Server 2016-, SQL Server 2017-Offlineinhalt  
 
**So installieren Sie Offlineinhalt**  
1. Öffnen Sie Help Viewer, indem Sie SQL Server Management Studio oder Visual Studio starten und im Menü **Hilfe** auf **Hilfeinhalt hinzufügen und entfernen** klicken.  
2. Klicken Sie auf die Registerkarte **Inhalt verwalten**.  
3. Klicken Sie zum Installieren der Hilfe von einer Onlinequelle im Bereich **Installationsquelle** auf **Online**.  
![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/helpviewer2-managecontent-onlinesource.png)  
7. Klicken Sie neben der Dokumentation, die Sie installieren möchten, auf **Hinzufügen** und dann auf **Aktualisieren**.  
![HelpViewer2_ManageContent_AddContent](../sql-server/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >In SQL Server Management Studio und Visual Studio kann die Anwendung Help Viewer während des Hinzufügens der Dokumentation einfrieren (hängenbleiben). Gehen Sie zur Lösung des Problems wie folgt vor: Weitere Informationen zu diesem Problem finden Sie unter [Visual Studio Help Viewer friert beim Begrüßungsbildschirm ein](https://msdn.microsoft.com/library/mt654096.aspx).  
   >>Öffnen Sie die Datei „%LOCALAPPDATA%\Microsoft\HelpViewer2.3\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio15_en-US.settings“ im Editor, und ändern Sie das Datum im folgenden Code in einen Zeitpunkt in der Zukunft. Diese Datei ist auf dem lokalen Computer nur verfügbar, wenn Sie Visual Studio installiert haben. 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    Das Inhaltsverzeichnis im linken Bereich wird automatisch um die Dokumentation aktualisiert, die Sie hinzugefügt haben.  
![HelpViewer2_withContentInstalled](../sql-server/media/helpviewer2-withcontentinstalled.png)

1. (Optional) Das Feld **Lokaler Speicherpfad** auf der Registerkarte **Inhalt verwalten** zeigt, wo die Dokumentation auf dem lokalen Computer installiert wird. Wenn Sie die Dokumentation an einen anderen Speicherort verschieben möchten, klicken Sie auf **Verschieben**, geben Sie im Dialogfeld **Inhalt verschieben** in das Feld **To** (Nach) einen Ordnerpfad ein, und klicken Sie dann auf **Ok**.

   ![HelpViewer2_Move Content Dialog](../sql-server/media/helpviewer2-move-content-dialog.png)

   Nach dem Verschieben des Inhalts wird der neue Speicherort unter **Lokaler Speicherpfad** angezeigt.
      
   >[!IMPORTANT]
   > Wenn eine Meldung angezeigt wird, die angibt, dass der Verschiebevorgang fehlgeschlagen ist, schließen Sie das Meldungsfeld und den Help Viewer, und öffnen Sie dann den Help Viewer erneut. Der neue Speicherort für den Inhalt sollte nun unter **Lokaler Speicherpfad** angezeigt werden.   
 
## <a name="includesssql14mdincludessssql14-mdmd-offline-content"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Offlineinhalt 
 
  
**So installieren Sie Offlineinhalt**  
1. Navigieren Sie zur [Downloadwebsite](https://www.microsoft.com/en-us/download/details.aspx?id=42557) für die Hilfeinhalte, und klicken Sie auf **Download**.  
2. Klicken Sie im Meldungsfeld auf **Speichern**, um die Datei „SQLServer2014Documentation_*.exe“ auf Ihrem Computer zu speichern.  

 Speichern Sie bei firewall- und proxygeschützten Umgebungen die Downloaddatei auf einem USB-Laufwerk oder anderen Wechselmedium, auf das in der Umgebung zugegriffen werden kann.   

3. Doppelklicken Sie auf die EXE-Datei, um die Datei mit Hilfeinhalten zu entpacken und in einem lokalen oder freigegebenen Ordner zu speichern.  
4. Öffnen Sie den **Hilfebibliotheks-Manager**, indem Sie SQL Server Management Studio oder Visual Studio starten und im Menü **Hilfe** auf **Hilfeeinstellungen verwalten** klicken.  
5. Klicken Sie auf **Inhalt von Datenträger installieren**, und suchen Sie den Ordner, in den Sie die Datei mit Hilfeinhalten entpackt haben.  
  
     Wählen Sie „Inhalt von Datenträger installieren“ aus  |Navigieren Sie zur Datei mit Hilfeinhalten   
     ---------|---------  
     ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
     >[!IMPORTANT]
     > Verwenden Sie im **Hilfebibliotheks-Manager** die Option **Inhalt von Datenträger installieren**, um zu vermeiden, dass lokale Hilfeinhalte installiert werden, bei denen das Inhaltsverzeichnis nur teilweise vorhanden ist.  
     >>Wenn Sie die Option **Inhalt von Onlinespeicherort installieren** gewählt haben und der Help Viewer das Inhaltsverzeichnis nur teilweise anzeigt, finden Sie in diesem [Blogbeitrag](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) Schritte zur Fehlerbehebung. 

8. Klicken Sie auf die Datei „HelpContentSetup.msha“, klicken Sie dann auf **Öffnen** und dann auf **Weiter**.  
9. Klicken Sie neben der Dokumentation, die Sie installieren möchten, auf **Hinzufügen** und dann auf **Aktualisieren**.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. Klicken Sie auf **Fertig stellen** und dann auf **Beenden**.
11. Öffnen Sie erneut den **Hilfebibliotheks-Manager**, klicken Sie auf **Onlinehilfe oder lokale Hilfe auswählen**, und klicken Sie dann auf **Ich möchte lokale Hilfe verwenden**.
12. Öffnen Sie den Help Viewer zum Anzeigen des Inhalts, indem Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken. Der Inhalt, den Sie installiert haben, sollte nun im Inhaltsverzeichnis im linken Bereich angezeigt werden.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
## <a name="view-online-content-in-help-viewer"></a>Anzeigen von Onlineinhalt im Help Viewer

Sie können im Help Viewer v2.x Onlineinhalt anzeigen, indem Sie Folgendes tun.

- Klicken Sie in SQL Server Management Studio auf **Hilfe anzeigen** im Menü **Hilfe**. Die Dokumentation wird in einem Browser angezeigt.
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)

- Klicken Sie in Visual Studio im Menü **Hilfe** auf **Hilfeeinstallungen festlegen**, und klicken Sie auf **Im Browser starten**. Wenn Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken, wird die Dokumentation in einem Browser angezeigt.

![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)   

Sie können im Help Viewer v1.x Onlineinhalt anzeigen, indem Sie Folgendes tun.
1. Öffnen Sie den **Hilfebibliotheks-Manager**, indem Sie im Menü **Hilfe** auf **Hilfeeinstellungen verwalten** klicken.  
2. Klicken Sie im Dialogfeld **Hilfebibliotheks-Manager** auf **Onlinehilfe oder lokale Hilfe auswählen**.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. Klicken Sie auf **Ich möchte Onlinehilfe verwenden**, dann auf **OK** und anschließend auf **Beenden**.  

   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

## <a name="f1-help-and-other-tips"></a>F1-Hilfe und andere Tipps

Wenn Sie F1 drücken, wird das entsprechende Thema online angezeigt. Das Thema kann nicht in der lokalen Hilfe angezeigt werden.

Der Help Viewer unterstützt Proxyeinstellungen und das ISO-Format nicht. 

## <a name="additional-information"></a>Zusätzliche Informationen
[Microsoft Help Viewer – Visual Studio](/visualstudio/ide/microsoft-help-viewer)  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
