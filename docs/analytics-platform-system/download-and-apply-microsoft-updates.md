---
title: Herunterladen und Anwenden von Microsoft-Updates (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f69df44-8549-4a8a-b10c-f91908594856
caps.latest.revision: "51"
ms.openlocfilehash: 7c91a5ed97d5aedfa456fd63e16c0178c5241706
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="download-and-apply-microsoft-updates"></a>Herunterladen und Anwenden von Microsoft-Updates
In diesem Thema wird erläutert, wie Updates von Microsoft Update-Katalog zu Windows Server Update Services (WSUS) herunterladen und diese Updates auf die Analytics Platform System Appliance-Server angewendet werden. Microsoft Update werden alle anwendbaren Updates für Windows und SQL Server installieren. WSUS ist auf dem VMM-virtuellen Computer von dem Gerät installiert.  
  
## <a name="TOP"></a>Vorbereitungen  
  
> [!WARNING]  
> Versuchen Sie nicht anwenden von Updates wird von dem Gerät oder eine beliebige Komponente Appliance heruntergefahren oder in einem fehlerhaften Zustand. In diesem Fall erhalten Sie Support um Unterstützung zu erhalten.  
>   
> Microsoft-Updates werden nicht angewendet werden, während das Gerät verwendet wird. Anwenden von Updates kann dazu führen, dass Appliance Knoten neu starten. Während eines Wartungsfensters sollten die Updates angewendet werden, wenn das Gerät nicht verwendet wird.  
  
### <a name="prerequisites"></a>Voraussetzungen  
Bevor Sie diese Schritte ausführen, müssen Sie:  
  
-   Konfigurieren von WSUS auf Ihrer Anwendung entsprechend den Anweisungen im [Konfigurieren von Windows Server Update Services &#40; WSUS &#41; &#40; Analyseplattformsystem &#41; ](configure-windows-server-update-services-wsus.md).  
  
-   Kenntnisse in Bezug auf eine Fabric-Domänenadministrator Anmeldung Kontoinformationen.  
  
-   Haben Sie einen Anmeldenamen mit Berechtigungen zum Zugriff auf das Analytics Platform System-Verwaltungskonsole und Anzeigen von Statusinformationen Appliance.  
  
-   In den meisten Fällen muss WSUS Server außerhalb der Anwendung zugreifen. Um dieses Verwendungsszenario zu unterstützen, das Analytics Platform System DNS Unterstützung eine Weiterleitung externer Name, mit dem das Analytics Platform System Hosts und virtuellen Computern (VMs), externen DNS-Server zum Auflösen von Namen verwenden können konfiguriert werden, können außerhalb von, der Appliance. Weitere Informationen finden Sie unter [mithilfe einer DNS-Weiterleitung zum Auflösen von Non-Appliance DNS-Namen &#40; Analyseplattformsystem &#41; ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="bkmk_ImportUpdates"></a>Herunterladen und Anwenden von Microsoft-updates  
  
#### <a name="verify-the-appliance-state-indicators"></a>Überprüfen Sie die Appliance Statusindikatoren  
  
1.  Öffnen Sie die Admin-Konsole, und navigieren Sie zu der Seite "Anwendungszustand". Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Vergewissern Sie sich die Statusindikatoren für alle Knoten auf den Zustand der Anwendung.  
  
    -   Sie können ruhig grün oder NA Indikatoren fortsetzen.  
  
    -   Bewerten Sie unkritische (gelb)-Fehlermeldungen. In einigen Fällen werden Warnmeldungen Updates nicht blockiert. Ist ein unkritische Volume Datenträgerfehler, der nicht auf dem Laufwerk C:\ ist, können Sie vor dem Lösen der Datenträgerfehler Volume mit dem nächsten Schritt fortfahren.  
  
    -   Die meisten rote Indikatoren müssen vor dem Fortsetzen aufgelöst werden. Wenn Datenträgerfehler sind, verwenden der Admin-Konsole Warnungsseite, stellen Sie sicher, dass nicht mehr als ein Fehler auf dem Datenträger in jedem Server oder SAN-Array vorhanden ist. Ist nicht mehr als ein Datenträgerfehler in jedem Server oder SAN-Array, können Sie mit dem nächsten Schritt fortfahren, vor der Behebung der Datenträgerausfällen. Achten Sie darauf, wenden Sie sich an Microsoft Support, um die Datenträgerfehlern so bald wie möglich zu beheben.  
  
#### <a name="synchronize-the-wsus-server"></a>Synchronisieren Sie den WSUS-server  
  
1.  Melden Sie sich an den virtuellen Computer von VMM als Domänenadministrator an.  
  
2.  In der **Server-Manager-Dashboard**auf die **Tools** Menü klicken Sie auf **Windows Server Update Services** (**wsus.msc**).  
  
3.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Synchronisierungen**.  
  
4.  Wenn die Synchronisierung nicht ausgeführt wird, klicken Sie auf **jetzt synchronisieren** im rechten Bereich. Im unteren Bereich werden eine Synchronisierungsstatus. Warten Sie, bis die Synchronisierung abgeschlossen ist.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Microsoft-Updates in WSUS genehmigt  
  
1.  Klicken Sie im linken Bereich der WSUS-Verwaltungskonsole auf **alle Updates**.  
  
2.  In der **alle Updates** Bereich, klicken Sie auf der **Genehmigung** Dropdown-Menü, Set **Genehmigung** auf **alle bis auf abgelehnte**. Klicken Sie auf die **Status** Dropdown-Menü, Satz **Status** auf **alle**. Klicken Sie auf **Aktualisieren**.  
  
    Mit der rechten Maustaste die **Titel** Spalte, und wählen **Dateistatus** um den Status der Datei zu überprüfen, nachdem der Download abgeschlossen ist.  
  
    Sie können auch auswählen **kritische Updates** oder **Sicherheitsupdates** im linken Bereich und die Ansicht verfügbaren Updates für diese Kategorien.  
  
    ![Wählen Sie alle Updates und Schutzstatus "auf" alle. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  Wählen Sie alle Updates, und klicken Sie dann auf die **genehmigen** Link im rechten Bereich.  
  
    Sie können auch Maustaste die ausgewählten Updates, und klicken Sie dann auf **genehmigen**. Sie möglicherweise aufgefordert, "Microsoft Software License Terms" zu akzeptieren. Wenn dies der Fall ist, klicken Sie auf **ich stimme** in das Fenster, um den Vorgang fortzusetzen.  
  
    ![Wählen Sie alle Updates, die gelten, und klicken Sie auf genehmigen. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  Wählen Sie die Appliance Server-Gruppe, die Sie erstellt, in haben [Konfigurieren von Windows Server Update Services &#40; WSUS &#41; &#40; Analyseplattformsystem &#41; ](configure-windows-server-update-services-wsus.md).  
  
5.  Klicken Sie auf **für die Installation genehmigt**, und klicken Sie dann auf **OK**.  
  
    ![Genehmigen Sie Updates für die Computergruppe ein. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  In der **Status der Genehmigung** (Dialogfeld), nach Abschluss des Genehmigungsprozesses, klicken Sie auf **schließen**.  
  
    ![Schließen Sie Fenster, wenn Updates genehmigt wurden. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Stellen Sie sicher, dass die Updates in WSUS  
  
-  Überprüfen Sie den Dateistatus aller Updates aus. Jede Datei muss auf einen grünen Pfeil links neben dem Titel haben. Dies gibt an, dass die Datei zur Installation bereit ist.  
  
    ![Dateistatus ist erfolgreich](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Stellen Sie bevor die Updates installiert werden sicher, dass sie alle heruntergeladen und in der WSUS-Konsole verfügbar sind.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Um sicherzustellen, dass alle Updates heruntergeladen werden  
  
-  Überprüfen Sie die **Downloadstatus** von Updates in der WSUS-Verwaltungskonsole, wie im folgenden Screenshot gezeigt. Überprüfen Sie, ob **Updates, die Dateien erfordern** ist 0, um zu bestätigen, dass alle Updates heruntergeladen werden. Wenn diese Zahl größer als NULL ist, müssen Sie ggf. zurückgehen und weitere Updates genehmigen.  
  
    ![Stellen Sie sicher, dass alle Updates heruntergeladen werden. ] (./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Anwenden von Microsoft-updates  
  
1.  Bevor Sie beginnen, öffnen Sie die [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41; ](monitor-the-appliance-by-using-the-admin-console.md), klicken Sie auf die **Anwendungszustand** Registerkarte, und überprüfen Sie, ob die **Cluster** und **Netzwerk** Spalten anzeigen, die grünen (oder NV) für alle Knoten. Wenn keine Warnungen in einem dieser Spalten vorhanden sind, das Gerät nicht ordnungsgemäß installiert. Updates möglicherweise. Beheben Sie alle vorhandene Warnungen in der **Cluster** und **Netzwerk** Spalten, bevor Sie fortfahren.  
  
2.  Melden Sie sich an den *< Domänenname >***-HST01** als Domänenadministrator Fabric-Knoten.  
  
3.  Um alle Updates für WSUS genehmigt anzuwenden, führen Sie das Update-Programm. Finden Sie unter [führen Sie das Update-Programm](#RunUpdateWizard) unten Anweisungen.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Überprüfen Sie die Updates auf allen Knoten  
  
1.  Starten Sie die WSUS-Verwaltungskonsole aus der VMM-Knoten. Diese Anwendung finden Sie unter **starten**, **Verwaltung**, **Windows Server Update Services**.  
  
2.  Erweitern Sie **Computer**.  
  
3.  Erweitern Sie **alle Computer**.  
  
4.  Wählen Sie die Appliance Server-Gruppe, die Sie erstellt, in haben [Konfigurieren von Windows Server Update Services &#40; WSUS &#41; &#40; Analyseplattformsystem &#41; ](configure-windows-server-update-services-wsus.md).  
  
5.  In der **Status** wählen Sie im Dropdownmenü **alle** , und klicken Sie auf **aktualisieren**.  
  
6.  Erweitern Sie **Aktualisierungsdienste**,  *<appliance name>* - VMM **Updates**, **alle Updates**, wobei  *<appliance name>*  ist der Gerätename Ihres.  
  
7.  In der **alle Updates** Fenster Satz **Genehmigung** auf **alle bis auf abgelehnte**.  
  
8.  In der **alle Updates** legen **Status** auf **erforderlich oder Fehler**.  
  
9. Klicken Sie auf **Aktualisieren**.  
  
10. Wenn **erforderlichen Updates** ist größer als 0 (null), wenden Sie den Support um Unterstützung zu erhalten.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Stellen Sie sicher, dass es sind keine kritischen Warnungen in der SQL Server PDW-Verwaltungskonsole  
  
1.  Öffnen Sie die Admin-Konsole, klicken Sie auf der Registerkarte "Anwendungszustand". Finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41; ](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Überprüfen Sie, ob die **Cluster** und **Netzwerk** Spalten anzeigen, die grünen (oder NV) für alle Knoten. Wenn keine Warnungen in einem dieser Spalten vorhanden sind, das Gerät nicht ordnungsgemäß installiert. Updates möglicherweise. Kontaktieren Sie Support, wenn kritische Warnungen vorhanden sind.  
  
## <a name="RunUpdateWizard"></a>Führen Sie das Update-Programm  
Um das Analytics Platform System Update-Programm auszuführen, gehen Sie wie folgt vor.  
  
> [!NOTE]  
> Der WSUS-System dient zur Ausführung asynchron kann einige Zeit dauern vollständig alle Updates anwenden. Initiieren ein Update plant ein Update gewährleistet jedoch nicht unmittelbar Updateaktivitäten.  
  
1.  Stellen Sie sicher, dass Sie in den Knoten "HST01" als der Fabric-Domänenadministrator angemeldet sind.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie die folgenden Befehle. Ersetzen Sie  *<parameter>*  mit den angegebenen Informationen.  
  
**So führen Sie die Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Um den Microsoft Update-Status zu melden:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Siehe auch  
[Deinstallieren Sie Microsoft Updates &#40; Analyseplattformsystem &#41;](uninstall-microsoft-updates.md)  
[Anwenden von Analytics Platform System Hotfixes &#40; Analyseplattformsystem &#41;](apply-analytics-platform-system-hotfixes.md)  
[Vorgehensweise: Deinstallieren Sie Analytics Platform System Hotfixes &#40; Analyseplattformsystem &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Wartung von Software &#40; Analyseplattformsystem &#41;](software-servicing.md)  
  
