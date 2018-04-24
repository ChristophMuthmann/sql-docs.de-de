---
title: Konfigurieren von WSUS - Analyseplattformsystem | Microsoft Docs
description: Diese Anweisungen führen Sie durch die Schritte zur Verwendung der Windows Server Update Services (WSUS)-Konfigurations-Assistent zum Konfigurieren von WSUS für Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: dfddc93672dfeb5840afe4cb97e668e3c12132c3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Konfigurieren von Windows Server Update Services (WSUS) in Analyseplattformsystem
Diese Anweisungen führen Sie durch die Schritte zur Verwendung der Windows Server Update Services (WSUS)-Konfigurations-Assistent zum Konfigurieren von WSUS für Analytics Platform System. Sie müssen zum Konfigurieren von WSUS, bevor Sie Softwareupdates auf das Gerät anwenden können. WSUS ist bereits auf dem VMM-virtuellen Computer des Geräts installiert.  
  
Weitere Informationen zum Konfigurieren von WSUS finden Sie unter der [WSUS schrittweise Anleitung für Installation](http://go.microsoft.com/fwlink/?LinkId=202417) auf die WSUS-Website. Nach dem Konfigurieren von WSUS, finden Sie unter [herunterladen und Anwenden von Microsoft-Updates &#40;Analyseplattformsystem&#41; ](download-and-apply-microsoft-updates.md) um ein Update zu initiieren.  
  
> [!WARNING]  
> Wenn bei dieser Konfiguration Fehler auftreten, beenden Sie, und wenden Sie sich an den Support, um Unterstützung zu erhalten. Ignorieren von Fehlern nicht, oder im Prozess fortgesetzt wird, wenn Fehler empfangen werden.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Um WSUS konfigurieren möchten, müssen Sie:  
  
-   Haben Sie Analytics Platform System Appliance Administrator Konto Domänenanmeldeinformationen an.  
  
-   Analyseplattformsystem Anmeldename mit Berechtigungen zum Zugriff auf die **-Verwaltungskonsole** und Zustandsinformationen für die Anwendung anzuzeigen.  
  
-   Kennen Sie die IP-Adresse des WSUS-Upstreamserver, wenn Sie planen, Synchronisieren von Updates vom WSUS-Upstreamserver statt direkt von Microsoft Update synchronisieren. Stellen Sie sicher, die WSUS-Upstreamserver auf anonyme Verbindungen zulassen festgelegt ist, und unterstützt SSL.  
  
-   Kennen Sie die IP-Adresse des Proxyservers, wenn Ihre Anwendung einen Proxyserver verwenden auf dem Upstreamserver oder Microsoft Update.  
  
-   In den meisten Fällen muss WSUS Server außerhalb der Anwendung zugreifen. Um dieses Verwendungsszenario zu unterstützen, das Analytics Platform System DNS Unterstützung eine Weiterleitung externer Name, mit dem das Analytics Platform System Hosts und virtuellen Computern (VMs), externen DNS-Server zum Auflösen von Namen verwenden können konfiguriert werden, können außerhalb von, der Appliance. Weitere Informationen finden Sie unter [mithilfe einer DNS-Weiterleitung zum Auflösen von Non-Appliance DNS-Namen &#40;Analyseplattformsystem&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>So konfigurieren Sie Windows Server Update Services (WSUS)  
  
1.  Melden Sie sich bei der **-Verwaltungskonsole**. Auf der **Anwendungszustand** Registerkarte, überprüfen Sie, ob die **Cluster** und **Netzwerk** Spalten anzeigen Grün (oder **NA**) für alle Knoten. Überprüfen Sie die Statusindikatoren für alle Knoten auf der **Anwendungszustand**.  
  
    -   Sie können ruhig grün oder NA Indikatoren fortsetzen.  
  
    -   Bewerten Sie unkritische (gelb)-Fehlermeldungen. In einigen Fällen werden Warnmeldungen Updates nicht blockiert. Ist ein unkritische Volume Datenträgerfehler, der nicht auf dem Laufwerk C:\ ist, können Sie vor dem Lösen der Datenträgerfehler Volume mit dem nächsten Schritt fortfahren.  
  
    -   Die meisten rote Indikatoren müssen vor dem Fortsetzen aufgelöst werden. Wenn Datenträgerfehler sind, verwenden Sie die **Admin Console Warnungen** Seite, um sicherzustellen, besteht darin, nicht mehr als ein Datenträger nicht innerhalb von jedem oder SAN-Array. Ist nicht mehr als ein Datenträgerfehler in jedem Server oder SAN-Array, können Sie mit dem nächsten Schritt fortfahren, vor der Behebung der Datenträgerausfällen. Achten Sie darauf, wenden Sie sich an Microsoft Support, um die Datenträgerfehlern so bald wie möglich zu beheben.  
  
2.  Melden Sie sich an den virtuellen Computer von VMM als ein Domänenadministrator Einheit an.  
  
3.  Starten Sie den Konfigurations-Assistenten.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Um den Konfigurations-Assistenten zu starten.  
  
    1.  In der **Server-Manager-Dashboard**auf die **Tools** Menü klicken Sie auf **Windows Server Update Services**.  
  
    2.  Im linken Bereich des der **Updatedienste** klicken, um die Virtual Machine Management-Knoten-Server zu erweitern (***Appliance_domain *-VMM**), und klicken Sie dann auf **Optionen**.  
  
    3.  In der **Optionen** Bereich, klicken Sie auf **WSUS-Server-Konfigurations-Assistenten** um den Konfigurations-Assistenten zu starten.  
  
        ![Server-Manager-Dashboard-Menü](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Wenn dies das erste Mal ist Sie den WSUS-Assistenten ausgeführt haben, werden Sie möglicherweise aufgefordert, ein Verzeichnis zum Speichern der Updates konfigurieren. `C:\wsus` ist Sie ein geeigneten Speicherort. Sie können jedoch einen anderen Pfad bereitstellen.  
  
        ![WSUS-Pfad](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Überprüfen Sie die **Vorbereitung** Liste von Elementen, die abgeschlossen sein, bevor Sie den Assistenten abzuschließen.  
  
        ![WSUS – Vorbereitungen](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  Auf der **verknüpfen das Programm zur Verbesserung von Microsoft Update** Seite **Ja, ich möchte dem Programm zur Verbesserung von Microsoft Update teilnehmen**, und klicken Sie dann auf **Weiter**.  
  
        ![WSUS – Verbesserungsprogramm](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    Jetzt sollte die **Upstreamserver auswählen** Seite. Der folgende Screenshot stammt den Ausgangspunkt des Konfigurations-Assistenten.  
  
    ![WSUS – Upstreamserversynchronisierung](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Wählen Sie die upstream-Server.  
  
    Auf der **Upstreamserver auswählen** Seite des WSUS-Konfigurations-Assistenten werden Sie auswählen, wie WSUS auf dem Virtual Machine Management-Knoten eine Verbindung mit einem Upstreamserver zum Abrufen von Softwareupdates herstellen. Zwei Optionen stehen, mit dem Upstreamserver synchronisiert [Microsoft Update](http://go.microsoft.com/fwlink/?LinkId=133349) oder für die Synchronisierung von Updates mit einem anderen Windows Server Update Services-Server.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Mithilfe von Microsoft Update aktualisiert  
  
    1.  Wenn Sie die Synchronisierung mit Microsoft Update entscheiden, müssen Sie keine Änderungen an den stellen die **Upstreamserver auswählen** Seite. Klicken Sie auf **Weiter**.  
  
        ![WSUS – Upstreamserversynchronisierung](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Um von einem anderen WSUS-Server zu aktualisieren.  
  
    1.  Wenn Sie zum Synchronisieren mit einer anderen Quelle als Microsoft-Update (einen upstream-Server) auswählen, geben Sie den Server (Geben Sie die IP-Adresse) und den Port auf dem dieser Server mit dem Upstreamserver kommuniziert.  
  
        ![WSUS – Upstreamserversynchronisierung von WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Um Secure Sockets Layer (SSL) verwenden möchten, wählen die **verwenden SSL beim Synchronisieren der Updateinformationen** Kontrollkästchen. In diesem Fall werden der Server Port 443 für die Synchronisierung verwenden.  
  
        ![WSUS – Upstreamserversynchronisierung von WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Wenn es sich um einen Replikatserver handelt, wählen Sie die **Dies ist ein Replikat des Upstreamservers** Kontrollkästchen. Es ist möglich, wählen Sie beide **verwenden SSL beim Synchronisieren der Updateinformationen** und **Dies ist ein Replikat des Upstreamservers**.  
  
        ![WSUS – Upstreamserverreplikat](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  An diesem Punkt können Sie mit der upstream-Server-Konfiguration nicht mehr benötigen. Klicken Sie auf **Weiter**, oder wählen Sie **Proxyserver angeben** im linken Navigationsbereich.  
  
5.  Geben Sie den Proxyserver an.  
  
    Wenn dieser Server einen Proxyserver für den Zugriff auf Microsoft Update oder einen anderen upstream-Server erfordert, können Sie die proxyservereinstellungen hier konfigurieren. Klicken Sie andernfalls auf **Weiter**.  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>So konfigurieren Sie die proxyservereinstellungen  
  
    1.  Auf der **Proxyserver angeben** auf der Seite im Konfigurations-Assistenten wählen Sie die **Proxyserver beim Synchronisieren von** Kontrollkästchen und geben Sie die Proxy-Server IP-Adresse (nicht-Name) und die Portnummer (Port 80 als (Standard) in die entsprechenden Felder.  
  
    2.  Gegebenenfalls Verbindung mit dem Proxyserver bestimmte Benutzeranmeldeinformationen, wählen Sie über die **mithilfe von Benutzeranmeldeinformationen für die Verbindung mit dem Proxyserver** Kontrollkästchen und geben Sie dann in der entsprechenden Benutzername, Domäne und Kennwort des Benutzers zu deaktivieren. Wenn Sie die Standardauthentifizierung für den Benutzer eine Verbindung mit dem Proxyserver herstellen aktivieren möchten die **Standardauthentifizierung zulassen (Kennwort wird in Klartext gesendet)** Kontrollkästchen.  
  
        ![WSUS – Proxyanmeldeinformationen](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  An diesem Punkt können Sie mit der Konfiguration der Proxyserver nicht mehr benötigen. Klicken Sie auf **Weiter** zur nächsten Seite wechseln, können Sie beginnen, den Synchronisierungsprozess einrichten.  
  
6.  Starten Sie eine Verbindung herstellen.  
  
    ![WSUS – Start der Proxyverbindung](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Klicken Sie auf **Start der Proxyverbindung**.  
  
    Nachdem die Verbindung erfolgreich war, klicken Sie auf **Weiter** zur nächsten Seite wechseln, in dem Sie Sprachen auswählen.  
  
7.  Wählen Sie die Sprachen.  
  
    Wählen Sie **Updates nur in folgenden Sprachen herunterladen**.  
  
    Wählen Sie **Englisch**, und klicken Sie dann auf **Weiter**.  
  
    ![Wählen Sie die Sprachen](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Auswählen von Produkten.  
  
    > [!NOTE]  
    > Wenn Sie einen Upstream-Server verwenden, können Sie nicht Produkte auswählen können. Wenn diese Option nicht verfügbar ist, überspringen Sie diesen Schritt.  
  
    Deaktivieren Sie alle ausgewählten Updates.  
  
    Wählen Sie **SQLServer 2014**, **SQLServer 2016**, **Windows Server 2012 R2**, und **System Center 2012 R2 – Virtual Machine Manager**, und Klicken Sie dann auf **Weiter**.  
  
9. Auswählen von Klassifizierungen.  
  
    > [!NOTE]  
    > Wenn Sie einen Upstream-Server verwenden, können Sie nicht Klassifizierungen auswählen können.  Wenn diese Option nicht verfügbar ist, überspringen Sie diesen Schritt.  
  
    Deaktivieren Sie alle zuvor ausgewählten Updates.  
  
    Wählen Sie **kritische Updates** und **Sicherheitsupdates** für die Updates, die für das Analytics Platform System Gerät synchronisiert werden sollen, und klicken Sie dann auf **Weiter**.  
  
    ![Auswählen von Klassifizierungen](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Konfigurieren Sie den Synchronisierungszeitplan an.  
  
    Wählen Sie **manuell synchronisieren**, und klicken Sie dann auf **Weiter**.  
  
    ![Festlegen des Synchronisierungszeitplans](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Erste Synchronisierung zu starten.  
  
    Wählen Sie **Erstsynchronisierung**, klicken Sie dann auf **Weiter**.  
  
12. Fertig stellen.  
  
    Klicken Sie auf **Fertig stellen**.  
  
## <a name="bkmk_WSUSGroup"></a>Gruppieren Sie die Appliance-Server in WSUS  
Als Nächstes werden nach dem Konfigurieren von WSUS für Analytics Platform System, die Appliance Servergruppe. Von allen Servern Appliance zu einer Gruppe hinzufügen, wird WSUS Softwareupdates auf allen Servern in der Einheit anwenden können.  
  
> [!NOTE]  
> Der WSUS-System ist darauf ausgelegt, asynchron ausgeführt wird. Initiieren einer Aktivität immer führt nicht zu einer sofort zu aktualisieren. Aus diesem Grund müssen Sie eine Weile warten, bis Computer in der WSUS-Dialogfelder angezeigt werden. Ausführen der `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` Befehl am Ende dieses Themas beschriebenen [herunterladen und Anwenden von Microsoft-Updates &#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md) Dialogfelder aktualisieren können.  
  
#### <a name="to-group-the-appliance-servers"></a>Um die Appliance-Server zu gruppieren.  
  
1.  Öffnen Sie die WSUS-Konsole, mit der rechten Maustaste **alle Computer** , und klicken Sie dann auf **Computergruppe hinzufügen**.  
  
    ![Fügen Sie eine Computergruppe hinzu. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Geben Sie den Namen "APS" für die Computergruppe aus, und klicken Sie dann auf **hinzufügen**.  
  
    ![Geben Sie Namen für die neue Computergruppe ein. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Klicken Sie auf **alle Computer** erneut aus, ändern Sie den Status in der **Status** Dropdown-Menü **alle**, und klicken Sie dann auf **aktualisieren**. Sie müssen möglicherweise erweitern **alle Computer** durch Klicken auf das Steuerelement der Strukturansicht auf der linken Seite um die neue Gruppe sehen Sie gerade hinzugefügt haben.  
  
    ![Schutzstatus "auf" alle aus, und klicken Sie auf aktualisieren. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Wählen Sie alle Computer, die Teil der Appliance, mit der rechten Maustaste, und klicken Sie dann auf **Mitgliedschaft ändern**.  
  
    ![Ändern Sie die Mitgliedschaft aller PDW-Computer. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Wählen Sie die neue Computergruppe aus, die Sie erstellt haben, indem Sie auf das Kontrollkästchen, und klicken Sie dann auf **OK**.  
  
    ![Gruppe der Gruppe "Computer"](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Wählen Sie die neue Computergruppe aus, ändern Sie seine **Status** auf **alle**, und klicken Sie dann auf **aktualisieren**. Alle Computer sollte jetzt zu dieser Gruppe zugewiesen, und im rechten Bereich aufgeführt. Es ist im Allgemeinen sicher, um den Vorgang fortzusetzen, wenn Warnungen wie z. B. zeigen **dieser Knoten verfügt über kein Status gemeldet noch**.  
  
    ![Schutzstatus "auf" alle aus, und klicken Sie auf aktualisieren. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
