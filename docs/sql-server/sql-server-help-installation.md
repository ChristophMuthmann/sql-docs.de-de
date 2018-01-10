---
title: "Hilfeinhalt und Help Viewer für SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 12/15/2017
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
ms.openlocfilehash: 679d0fb003a8a59185d860a125cfdd8b5601367c
ms.sourcegitcommit: f2fde1c324466530f92006561a9a29decb711e1b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="sql-server-offline-help-and-help-viewer"></a>Offlinehilfe und Help Viewer für SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Sie können Help Viewer in SQL Server Management Studio (SSMS) oder Visual Studio (VS) verwenden, um Hilfepakete für SQL Server von Onlinequellen oder Datenträgern herunterzuladen und zu installieren, sodass Sie diese auch abrufen können, wenn Sie offline sind. In diesem Artikel werden Tools beschrieben, die Help Viewer installieren. Außerdem erhalten Sie eine Anleitung zum Installieren von Hilfeinhalt, der offline verfügbar ist, und es wird beschrieben, wie Sie Hilfe für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 und SQL Server 2017 abrufen.

> [!NOTE]
> Die Hilfe für SQL Server 2016 und SQL Server 2017 wird gemeinsam erläutert. Es wird darauf hingewiesen, wenn ein Thema nur für einzelne Versionen von Belang ist. Die meisten Themen gelten für beide Versionen.

## <a name="install-the-help-viewer"></a>Installieren von Help Viewer

Es gibt zwei Versionen von Help Viewer: Version 2.x unterstützt Hilfe für SQL Server 2016 und SQL Server 2017, und Version 1.x unterstützt Hilfe für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]. Der Help Viewer unterstützt Proxyeinstellungen und das ISO-Format nicht. 

Help Viewer wird mithilfe der folgenden Tools installiert: 

|**Tool, das Help Viewer installiert**|**Installierte Help Viewer-Version**|
|---------|---------|
|[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)| v2.2|
|[SQL Server Data Tools für Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)| v2.2|
|Visual Studio 2017* | v2.3|
|Visual Studio 2015 | v2.2|
|SQL Server 2014 Management Studio | v1.x|
|Frühere Versionen von Visual Studio | v1.x|
|SQL Server 2016 | v1.x|

\* Um Help Viewer mit Visual Studio 2017 zu installieren, klicken Sie auf die Registerkarte „Einzelne Komponenten“ im Visual Studio-Installer, wählen Sie unter „Codetools“ **Help Viewer** aus, und klicken Sie dann auf **Installieren**. 

>[!NOTE]
> - SQL Server 2016 installiert Help Viewer 1.1. Diese Version unterstützt allerdings nicht die Hilfe für SQL Server 2016. 
> - Bei der Installation von SQL Server 2017 wird keine Help Viewer-Version installiert.
> - Help Viewer v2.x kann außerdem die Hilfe für [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] unterstützen, wenn Sie den Inhalt von einem Datenträger installieren.

## <a name="use-help-viewer-v2x"></a>Verwenden Sie Help Viewer v2.x

SSMS 17.x und VS 2015 und 2017 verwenden Help Viewer 2.x. Diese Version unterstützt die Hilfe für SQL Server 2016 und 2017. 

**Herunterladen und Installieren von offline verfügbarem Hilfeinhalt mit Help Viewer v2.x**

1. Klicken Sie in SSMS oder VS im Menü „Hilfe“auf **Hilfeinhalt hinzufügen und entfernen**. 

   ![HelpViewer2: Hinzufügen und Entfernen von Inhalt](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   Help Viewer öffnet die Registerkarte „Inhalt verwalten“.  
   
2. Wählen Sie unter „Installationsquelle“ **Online** aus, um das neuste Paket mit Hilfeinhalten zu installieren.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > Wenn Sie die Installation über einen Datenträger (Hilfe für SQL Server 2014) installieren möchten, wählen Sie unter „Installationsquelle“ **Datenträger** aus, und geben Sie den Speicherort der Datenquelle an.
   
   Der lokale Speicherpfad auf der Registerkarte „Inhalt verwalten“ zeigt an, wo der Inhalt auf dem lokalen Computer installiert wird. Wenn Sie den Speicherort ändern möchten, klicken Sie auf **Verschieben**, geben Sie einen anderen Ordnerpfad im Feld **Nach** ein, und klicken Sie anschließend auf **OK**.
   Wenn die Installation der Hilfe fehlschlägt, nachdem Sie den lokalen Speicherpfad geändert haben, schließen Sie Help Viewer, und öffnen Sie das Programm erneut. Vergewissern Sie sich, dass der neue Speicherort im lokalen Speicherpfad angezeigt wird, und führen Sie die Installation erneut durch.

3. Klicken Sie neben jedem Inhaltspaket (Buch), das Sie installieren möchten, auf **Hinzufügen**. 
   Fügen Sie alle 13 Bücher unter „SQL Server“ hinzu, um sämtlichen Hilfeinhalt auf SQL Server zu installieren. 
   
4. Klicken Sie im unteren rechten Bereich auf **Aktualisieren**. 
   Das Inhaltsverzeichnis der Hilfe im linken Bereich wird automatisch mit den hinzugefügten Büchern aktualisiert. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> Nicht alle Titel des höchsten Knotens im Inhaltsverzeichnis von SQL Server stimmen genau mit den Namen der jeweiligen Hilfebücher überein, die heruntergeladen werden können. Die Titel im Inhaltsverzeichnis werden den Buchnamen wie folgt zugeordnet:

| Inhaltsbereich | SQL Server-Buch |
|-----|-----|
|Analysis Services-Sprachreferenz | Analysis Services-Sprachreferenz (MDX)|
|DAX-Referenz (Data Analysis Expressions) | DAX-Referenz (Data Analysis Expressions)|
|DMX-Referenz (Data Mining-Erweiterungen) | DMX-Referenz (Data Mining-Erweiterungen)|
|Leitfäden für Entwickler für SQL Server | SQL Server Developer-Referenz|
|Hier können Sie SQL Server Management Studio herunterladen. | SQL Server Management Studio|
|Erste Schritte mit Machine Learning in SQL Server | Microsoft Machine Learning Services|
|Power Query M-Referenz | Power Query M-Referenz|
|SQL Server-Treiber | Treiber für die SQL Server-Verbindung|
|SQL Server unter Linux | SQL Server unter Linux|
|Technische Dokumentation zu SQL Server | Technische Dokumentation für SQL Server (SSIS, SSRS, Datenbank-Engine, Setup)|
|Tools und Hilfsprogramme für Azure SQL-Datenbank | SQL Server-Tools|
|Transact-SQL-Referenz (Datenbankmodul) | Transact-SQL-Referenz|
|XQuery-Sprachreferenz (SQL Server) | XQuery-Sprachreferenz (SQL Server)|

> [!NOTE]
> Wenn Help Viewer beim Hinzufügen von Inhalt nicht mehr reagieren sollte, ändern Sie die Cachezeile „LastRefreshed=\<mm/dd/yyyy> 00:00:00“ in den Dateien „%LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings“ oder „HlpViewer_VisualStudiox_en-US.settings“ in ein Datum, das in der Zukunft liegt. Weitere Informationen zu diesem Problem finden Sie unter [Visual Studio Help Viewer friert beim Begrüßungsbildschirm ein](https://msdn.microsoft.com/en-us/library/dd831853.aspx).

**Anzeigen von offline verfügbarem Hilfeinhalt in SSMS mit Help Viewer v2.x**

Drücken Sie STRG+ALT+F1, um die installierte Hilfe in SSMS anzuzeigen, oder wählen Sie im Menü „Hilfe“ **Hilfeinhalt hinzufügen und entfernen** aus, um Help Viewer zu starten. 

   ![HelpViewer2: Hinzufügen und Entfernen von Inhalt](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

Help Viewer öffnet sich in der Registerkarte „Inhalt verwalten“ mit dem installierten Inhaltsverzeichnis für die Hilfe im linken Bereich. Klicken Sie im Inhaltsverzeichnis auf ein Thema, um dieses auf der rechten Seite anzuzeigen. 
> [!TIP]
> Wenn der Inhaltsbereich nicht angezeigt wird, klicken Sie auf „Inhalt“ auf der linken Seite. Klicken Sie auf das Reißzweckensymbol, damit der Inhaltsbereich geöffnet bleibt.  

   ![Help Viewer v2.x mit Inhalt](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**Anzeigen von offline verfügbarem Hilfeinhalt in VS mit Help Viewer v2.x**

Führen Sie die folgenden Schritte aus, damit die in Visual Studio installierte Hilfe angezeigt wird:
1. Zeigen Sie im Menü „Hilfe“ auf **Hilfeeinstellungen festlegen**, und wählen Sie **In Help Viewer starten** aus. 

   ![Hilfeansicht für Visual Studio: Einstellungen für Help Viewer festlegen](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. Klicken Sie im Menü „Hilfe“ auf **Hilfe anzeigen**, damit der Inhalt in Help Viewer angezeigt wird. 

   ![Hilfe anzeigen](../sql-server/media/sql-server-help-installation/viewhelp.png)

   Das Inhaltsverzeichnis der Hilfe wird auf der linken Seite und das ausgewählte Hilfethema auf der rechten Seite angezeigt. 
   
## <a name="use-help-viewer-v1x"></a>Verwenden von Help Viewer v1.x

Frühere Versionen von SSMS und Visual Studio verwenden Help Viewer 1.x. Diese Version unterstützt die Hilfe für SQL Server 2014. 

**Herunterladen und Installieren von offline verfügbarem Hilfeinhalt mit Help Viewer v1.x**

In diesem Vorgang wird Help Viewer 1.x verwendet, um die Hilfe für SQL Server 2014 aus dem Microsoft Download Center herunterzuladen und auf dem Computer zu installieren.

1. Navigieren Sie zur Downloadwebsite [Product Documentation for Microsoft SQL Server 2014 (Produktdokumentation für Microsoft SQL Server 2014)](https://www.microsoft.com/en-us/download/details.aspx?id=42557), und klicken Sie auf **Herunterladen**.  
2. Klicken Sie im Meldungsfeld auf **Speichern**, um die Datei *SQLServer2014Documentation\_\*.exe* auf Ihrem Computer zu speichern.  
   
   >[!NOTE]
   >Speichern Sie bei firewall- und proxygeschützten Umgebungen die Downloaddatei auf einem USB-Laufwerk oder anderen Wechselmedium, auf das in der Umgebung zugegriffen werden kann.   
   
3. Doppelklicken Sie auf die EXE-Datei, um die Datei mit Hilfeinhalten zu entpacken und in einem lokalen oder freigegebenen Ordner zu speichern.  
4. Öffnen Sie den **Hilfebibliotheks-Manager**, indem Sie SSMS oder Visual Studio starten und im Menü „Hilfe“ auf **Hilfeeinstellungen verwalten** klicken.  
5. Klicken Sie auf **Install content from disk** (Inhalt von Datenträger installieren), und suchen Sie nach dem Ordner, in dem Sie die Datei mit Hilfeinhalten entpackt haben.  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > Verwenden Sie im **Hilfebibliotheks-Manager** die Option **Install content from disk** (Inhalt von Datenträger installieren), um zu vermeiden, dass lokale Hilfeinhalte installiert werden, bei denen das Inhaltsverzeichnis nur teilweise vorhanden ist.  Wenn Sie **Install content from online** (Inhalt von Onlinespeicherort installieren) ausgewählt haben und Help Viewer das Inhaltsverzeichnis nur teilweise anzeigt, finden Sie in diesem [Blogbeitrag](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) Anweisungen zur Fehlerbehebung. 
   
8. Klicken Sie auf die Datei „HelpContentSetup.msha“, klicken Sie dann auf **Öffnen** und dann auf **Weiter**.  
9. Klicken Sie neben der Dokumentation, die Sie installieren möchten, auf **Hinzufügen** und dann auf **Aktualisieren**.  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. Klicken Sie auf **Fertig stellen** und dann auf **Beenden**.

**Anzeigen von offline verfügbarem Hilfeinhalt mit Help Viewer v1.x**

11. Öffnen Sie erneut den **Hilfebibliotheks-Manager**, klicken Sie auf **Choose online or local help** (Onlinehilfe oder lokale Hilfe auswählen), und klicken Sie dann auf **I want to use local help** (Ich möchte lokale Hilfe verwenden).
12. Öffnen Sie den Help Viewer zum Anzeigen des Inhalts, indem Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken. Die von Ihnen installierten Inhalte werden auf der linken Seite aufgeführt.  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   
## <a name="view-online-help"></a>Anzeigen der Onlinehilfe

In der Onlinehilfe werden stets die aktuellsten Inhalte angezeigt. 

**Anzeigen der Onlinehilfe für SQL Server in SSMS 17.x**

- Klicken Sie im Menü **Hilfe** auf **Hilfe anzeigen**. Im Browser wird unter [https://docs.microsoft.com/sql/https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation) die neuste Dokumentation für SQL Server 2016/2017 angezeigt. 

   ![Hilfe anzeigen](../sql-server/media/sql-server-help-installation/viewhelp.png)

**Anzeigen der Visual Studio Onlinehilfe in Visual Studio**

1. Zeigen Sie im Menü „Hilfe“ auf **Hilfeeinstellungen festlegen**, und wählen Sie entweder **In Browser starten** oder **In Help Viewer starten** aus. 
2. Klicken Sie im Menü „Hilfe“ auf **Hilfe anzeigen**. Die neuste Hilfe für Visual Studio wird in der ausgewählten Umgebung angezeigt. 

**Anzeigen der Onlinehilfe mit Help Viewer v1.x**

1. Öffnen Sie den **Hilfebibliotheks-Manager**, indem Sie im Menü „Hilfe“ auf **Hilfeeinstellungen verwalten** klicken.  
2. Klicken Sie im Dialogfeld „Hilfebibliotheks-Manager“ auf **Choose online or local help** (Onlinehilfe oder lokale Hilfe auswählen).  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. Klicken Sie auf **I want to use online help** (Ich möchte Onlinehilfe verwenden), dann auf **OK** und anschließend auf **Beenden**.  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)
   
4. Öffnen Sie den Help Viewer zum Anzeigen des Inhalts, indem Sie im Menü **Hilfe** auf **Hilfe anzeigen** klicken. 

## <a name="view-f1-help"></a>Anzeigen der F1-Hilfe

Wenn Sie F1 drücken oder in einem Dialogfeld in SSMS oder Visual Studio auf **Hilfe** oder das Symbol **?** klicken, wird ein Thema der kontextbezogenen Onlinehilfe im Browser oder in Help Viewer angezeigt. 

**Anzeigen der F1-Hilfe**

1. Zeigen Sie im Menü „Hilfe“ auf **Hilfeeinstellungen festlegen**, und wählen Sie entweder **In Browser starten** oder **In Help Viewer starten** aus. 
2. Drücken Sie F1, oder klicken Sie in den Dialogfeldern auf **Hilfe** oder **?**, falls verfügbar, um Themen der kontextbezogenen Onlinehilfe in der ausgewählten Umgebung anzuzeigen.

>  [!NOTE]
>  Die F1-Hilfe funktioniert nur, wenn Sie online sind. Es sind keine Offlinequellen für F1-Hilfe verfügbar. 
   

## <a name="next-steps"></a>Nächste Schritte
[Microsoft Help Viewer – Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
