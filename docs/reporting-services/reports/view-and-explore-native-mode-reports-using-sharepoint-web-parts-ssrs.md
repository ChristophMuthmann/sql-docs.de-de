---
title: "Anzeigen und Durchsuchen von Berichten im einheitlichen Modus mithilfe von SharePoint-Webparts (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
caps.latest.revision: 9
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# Anzeigen und Durchsuchen von Berichten im einheitlichen Modus mithilfe von SharePoint-Webparts (SSRS)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt nicht mehr die Verwendung von Webparts im einheitlichen Modus („RSWebParts.cab“) für den Zugriff auf Berichtsserverinhalt auf einer SharePoint-Website von einem Berichtsserver im einheitlichen Modus aus. Verwenden Sie ein [Berichts-Viewer-Webpart für eine SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] werden verschiedene Webparts bereitgestellt, die mit bestimmten Versionen eines Berichtsservers und in bestimmten Bereitstellungsmodi verwendet werden können.  
  
-   **Einheitlicher Modus:** Wenn Sie von einem Berichtsserver, der im einheitlichen Modus ausgeführt wird, auf Berichtsserverinhalte auf einer SharePoint-Website zugreifen möchten, verwenden Sie die in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]enthaltenen SharePoint 2.0-Webparts. Anweisungen zur Installation und Verwendung der 2.0-Webparts finden Sie in diesem Thema.  
  
-   **SharePoint-Modus:** Wenn Sie auf einen Berichtsserver zugreifen möchten, der im SharePoint-Modus ausgeführt wird, verwenden Sie die Webparts, die vom [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In für SharePoint-Produkte installiert werden. Weitere Informationen zu dem Add-In finden Sie unter [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
> [!NOTE]  
>  Das Berichts-Viewer-Webpart für den einheitlichen Modus („SPViewer.dwp“) unterscheidet sich von dem Webpart („ReportViewer.dwp“), das vom [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In für SharePoint-Produkte installiert wird. Die Webparts haben andere Schemas und Implementierungen, aber beide können in der gleichen SharePoint-Farm installiert sein. Optisch können Sie die beiden Webparts anhand des folgenden Merkmals unterscheiden: Das mit dem Add-In installierte Report Viewer-Webpart weist auf der Symbolleiste das Menü **Aktionen** auf.  
  
 Weitere Informationen zu Berichtsservermodi finden Sie unter [Reporting Services-Berichtsserver](../../reporting-services/report-server-sharepoint/reporting-services-berichtsserver.md).  
  
 In diesem Thema:  
  
-   [Informationen zum Berichts-Explorer und zum Berichts-Viewer](#bkmk_aboutwebparts)  
  
-   [Anforderungen zum Verwenden der Webparts](#bkmk_requirements)  
  
-   [Installieren von Webparts](#bkmk_installingwebparts)  
  
-   [Hinzufügen und Konfigurieren von Webparts](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> Informationen zum Berichts-Explorer und zum Berichts-Viewer  
 Die SharePoint 2.0-Webparts Berichts-Explorer und Berichts-Viewer wurden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Service Pack 2 (SP2) eingeführt und sind auch in aktuellen Versionen verfügbar.  
  
 Die Webparts bieten eine Möglichkeit, auf einer SharePoint-Website Berichte anzuzeigen und die Ordnerhierarchie des Berichtsservers zu durchsuchen.  
  
 Beachten Sie, dass das Anpassen der Webparts nicht unterstützt wird. Die Webparts müssen unverändert verwendet werden und dürfen weder erweitert noch bearbeitet werden.  
  
-   Der **Berichts-Explorer** („SPExplorer.dwp“) stellt eine Verbindung mit dem Berichts-Manager auf dem Berichtsservercomputer her. Sie können die verfügbaren Berichte auf einem Berichtsserver durchsuchen und einzelne Berichte abonnieren. Wenn der Berichts-Generator aktiviert ist und Sie über ausreichende Berechtigungen verfügen, können Sie den Berichts-Generator über das Berichts-Explorer-Webpart starten.  
  
     Im Berichts-Explorer wird der Inhalt eines Ordners auf einer Seite im Berichts-Manager angezeigt. Der Zugriff auf einzelne Elemente und Ordner in der Ordnerhierarchie des Berichtsservers wird über Rollenzuweisungen auf dem Berichtsserver gesteuert. Wenn Sie einen Bericht auswählen, wird dieser automatisch in einem neuen Browserfenster geöffnet. Die Anzeige des Berichts und die Bereitstellung der Berichtssymbolleiste erfolgen nicht im Berichts-Viewer-Webpart, sondern im HTML-Viewer auf dem Berichtsserver. Wenn Sie die Symbolleisteneinstellungen anpassen möchten, müssen Sie die URL-Zugriffsparameter auf dem Berichtsserver angeben. Anleitungen finden Sie unter [URL-Zugriffsparameterverweis](../../reporting-services/url-access-parameter-reference.md).  
  
-   Im **Berichts-Viewer** („SPViewer.dwp“) wird ein Bericht angezeigt. Außerdem wird eine Symbolleiste bereitgestellt, mit der Sie auf Seiten navigieren, nach Inhalten suchen oder den Bericht exportieren können. Sie können das Berichts-Viewer-Webpart einer Webpartseite hinzufügen, um auf der betreffenden Seite stets einen bestimmten Bericht anzuzeigen. **Sie können das Webpart auch mit dem Berichts-Explorer verbinden** , um Berichte anzuzeigen, die über dieses Webpart geöffnet werden.  
  
##  <a name="bkmk_requirements"></a> Anforderungen zum Verwenden der Webparts  
 Für die Verwendung der Webparts Berichts-Viewer und Berichts-Explorer gelten die folgenden Anforderungen:  
  
-   Folgende Versionen von SharePoint-Produkten und Technologien werden unterstützt:  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] und [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   Bei der Berichtsserverversion für den einheitlichen Modus muss es sich um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oder höher handeln.  
  
-   Der Berichtsserver muss im einheitlichen Modus ausgeführt werden. Sie können mit den Webparts Berichts-Explorer und Berichts-Viewer **keine** Verbindungen mit einem Berichtsserver im integrierten SharePoint-Modus herstellen oder Berichte auf einem solchen anzeigen.  
  
-   Der Berichts-Manager muss installiert sein.  
  
 Die Webparts Berichts-Explorer und Berichts-Viewer werden mithilfe einer CAB-Datei (Cabinet-Datei) verteilt, die in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthalten ist. Anweisungen zur Installation, Konfiguration und Verwendung der Webparts finden Sie in den folgenden Abschnitten dieses Themas.  
  
##  <a name="bkmk_installingwebparts"></a> Installieren von Webparts  
 Webparts werden als CAB-Datei an einen SharePoint-Server übermittelt. Führen Sie über die Befehlszeile das SharePoint-Tool Stsadm.exe für die CAB-Datei aus, um die Webparts zu installieren. Weitere Informationen zu diesem Tool und zur Bereitstellung von Webparts finden Sie in der SharePoint-Dokumentation.  
  
#### Installieren von Webparts mit PowerShell  
  
1.  Kopieren Sie **RSWebParts.cab** in einen Ordner auf dem SharePoint-Server. Sie können sie in einen beliebigen Ordner auf dem SharePoint-Server kopieren und nach der Installation der Webparts löschen. Standardmäßig installiert [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] die Datei "RSWebParts.cab" im folgenden Ordner:  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  Öffnen Sie auf dem Computer, auf dem das SharePoint-Produkt installiert ist, die **SharePoint 2010-Verwaltungsshell** mit **Administratorrechten**.  
  
3.  Führen Sie den folgenden PowerShell-Befehl aus:  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  Eine Meldung ähnlich der folgenden sollte angezeigt werden, die angibt, dass das Webpart bereitgestellt wurde.  
  
    > Name               SolutionId                                             Deployed  
  
    > ----                    ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     Weitere Informationen zum Verwenden von PowerShell finden Sie unter [Install-SPWebPartPack (http://technet.microsoft.com/library/ff607840.aspx)](http://technet.microsoft.com/library/ff607840.aspx).  
  
#### Installieren von Webparts mit STSADM.exe  
  
1.  Kopieren Sie die Datei **RSWebParts.cab** an den gleichen Speicherort auf dem SharePoint-Server wie in diesem Dokument im Abschnitt zu PowerShell beschrieben.  
  
2.  Öffnen Sie auf dem Computer, auf dem das SharePoint-Produkt installiert ist, mit Administratorrechten ein Eingabeaufforderungsfenster, und navigieren Sie zu dem Ordner, in dem sich das Tool **Stsadm.exe** befindet. Der Standardpfad für [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ist:  
  
    > C:\Programme\Gemeinsame Dateien\Microsoft Shared\Web Server Extensions\14\BIN.  
  
3.  Führen Sie Stsadm.exe für die CAB-Datei mit der folgenden Syntax aus:  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  Die Meldung "Der Vorgang wurde erfolgreich abgeschlossen" sollte angezeigt werden.  
  
     Durch Angeben von `-globalinstall` werden die Webparts dem globalen Assemblycache (Global Assembly Cache, GAC) hinzugefügt. Dieser Schritt ist notwendig, wenn Sie eine Verbindung mit den Webparts herstellen möchten.  
  
##  <a name="bkmk_configurewebparts"></a> Hinzufügen und Konfigurieren von Webparts  
 Wenn Sie die Webparts installiert haben, können Sie diese einer oder mehreren Webseiten auf einer SharePoint-Website hinzufügen. Sie müssen die Berechtigung zum Erstellen von Websites und Hinzufügen von Inhalten besitzen.  
  
 Mit der folgenden Vorgehensweise werden beide Webparts einer Seite hinzugefügt und dann Berichts-Explorer und Berichts-Viewer miteinander verbunden, damit ein Bericht im Berichts-Viewer angezeigt wird, wenn Sie im Berichts-Explorer auf diesen Bericht klicken.  
  
#### Hinzufügen von Berichts-Viewer  
  
1.  Klicken Sie im Menü Websiteaktionen auf **Seite bearbeiten**.  
  
2.  Klicken Sie in einer Zone der Seite auf **Webpart hinzufügen**.  
  
3.  Führen Sie im Dialogfeld **Webparts hinzufügen** einen Bildlauf zur Kategorie **Sonstiges** durch.  
  
4.  Wählen Sie **Berichts-Viewer**aus.  
  
    > [!WARNING]  
    >  Wählen Sie nicht **Berichts-Viewer für SQL Server Reporting Services** aus. Dieses Webpart wird beim Installieren des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-Ins für SharePoint-Produkte registriert und zum Ausführen eines Berichtsservers im SharePoint-Modus verwendet. Es kann auf einem Berichtsserver im einheitlichen Modus zum Anzeigen von Berichten verwendet werden.  
  
5.  Klicken Sie auf **Hinzufügen**.  
  
6.  Klicken Sie im Berichts-Viewer-Webpart auf **Webpart bearbeiten** , während sich die Seite im Bearbeitungsmodus befindet.  
  
7.  Geben Sie unter **Report Manager URL**eine URL zu einer Berichts-Manager-Instanz ein, die mit dem Berichtsserver im einheitlichen Modus verbunden ist, auf den Sie zugreifen möchten. In der Standardeinstellung weist die Berichts-Manager-URL die folgende Syntax auf: **http://\<Servername>/reports**.  
  
8.  Geben Sie unter **Berichtspfad**einen Schrägstrich an, gefolgt vom Ordnerpfad und dem Berichtsnamen. Der Servername oder das virtuelle Berichts-Manager-Verzeichnis dürfen **nicht** angegeben werden. Wenn Sie z.B. den Bericht „Company Sales“ im Ordner „Adventure Works“ öffnen möchten, geben Sie **/Adventure Works/Company Sales** an. Im Folgenden wird ein weiteres Beispiel gezeigt, in dem sich der Bericht „Produkte“ im Stammordner **/Products** des Berichtsservers befindet.  
  
9. Klicken Sie auf **OK**.  
  
#### Hinzufügen von Berichts-Explorer und Verbinden mit Berichts-Viewer  
  
1.  Klicken Sie in einem anderen Bereich der Seite auf **Webpart hinzufügen** . Klicken Sie im Ordner Sonstiges auf **Berichts-Explorer** , und klicken Sie dann auf **Hinzufügen**.  
  
2.  Klicken Sie im Kontextmenü Webpart des Berichts-Explorers auf **Webpart bearbeiten**.  
  
3.  Geben Sie unter **Report Manager URL**eine URL zu einer Berichts-Manager-Instanz ein, die mit dem Berichtsserver im einheitlichen Modus verbunden ist, auf den Sie zugreifen möchten.  
  
4.  Sie können auch den **Startpfad**festlegen. Der Startpfad ist ein Ordner in der Berichtsserver-Ordnerhierarchie. Einen Startpfad können Sie angeben, wenn als Standardseite ein Ordner in einer unteren Ebene der Ordnerhierarchie verwendet werden soll. Der Pfad muss mit einem Schrägstrich (/) beginnen. Sie müssen einen vollständigen Pfad angeben, der mit dem Stammknoten der Ordnerhierarchie auf dem Berichtsserver beginnt, jedoch nicht den Servernamen oder das virtuelle Berichts-Manager-Verzeichnis enthält. Wenn Sie z.B. den Ordner „Adventure Works“ genau unter dem Stammknoten öffnen möchten, geben Sie als Startpfad **/Adventure Works** an.  
  
5.  Klicken Sie auf **OK**.  
  
6.  Im Berichts-Explorer wird eine Liste der Berichtselemente im Berichtsserver angezeigt. Wenn Sie auf den Namen eines Berichts klicken, wird der Bericht standardmäßig in einem neuen Fenster geöffnet. Führen Sie die folgenden Schritte aus, wenn Sie den Berichts-Explorer und den Berichts-Viewer miteinander verbinden möchten, damit beim Klicken auf einen Berichtsnamen im Berichts-Explorer dieser Bericht im Berichts-Viewer angezeigt wird.  
  
    1.  Klicken Sie im Kontextmenü des Berichts-Explorers auf **Verbindungen**.  
  
    2.  Klicken Sie auf **Bericht anzeigen in**.  
  
    3.  Klicken Sie auf **Berichts-Viewer**.  
  
## Siehe auch  
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)   
 [Reporting Services-Berichtsserver &#40;SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)   
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  