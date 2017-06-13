---
title: "Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
caps.latest.revision: 52
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7983325b1036809058e4866dd217c72c97c8238b
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus
  Ein Standardabonnement wird von einzelnen Benutzern erstellt, die einen Bericht per E-Mail oder an einen freigegebenen Ordner übermitteln möchten. Dieses Thema stellt Informationen zu Standardabonnements bereit, die von einzelnen Benutzern erstellt und verwaltet werden. Für datengesteuerte Abonnements gelten unterschiedliche Anforderungen und Schritte, die in einem anderen Thema behandelt werden. Weitere Informationen finden Sie unter [Erstellen, Ändern und Löschen von datengesteuerten Abonnements](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md).  
  
 **In diesem Thema:**  
  
-   [Allgemeine Anforderungen für Abonnements](#bkmk_create_subscription)  
  
-   [So erstellen Sie ein Dateifreigabeabonnement](#bkmk_create_fileshare_subscription)  
  
-   [So erstellen Sie ein E-Mail-Abonnement](#bkmk_create_email_subscription)  
  
-   [So ändern Sie ein Abonnement](#bkmk_modify_subscription)  
  
-   [So löschen Sie ein Abonnement](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> Allgemeine Anforderungen für Abonnements  
 In diesem Thema wird erläutert, wie mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichts-Manager Abonnements auf einem Berichtsserver im einheitlichen Modus erstellt werden. Nach der Definition eines Abonnements können Sie im Berichts-Manager auf der Seite Meine Abonnements oder auf der Registerkarte **Abonnements** eines bestimmten Berichts darauf zugreifen.  
  
 [Erstellen und Verwalten von Abonnements für Berichtsserver im SharePoint-Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) erklärt, wie mit den Anwendungsseiten auf einer SharePoint-Site Berichte auf einem SharePoint-Modus-Berichtsserver abonniert werden.  
  
-   Zum Verwenden der E-Mail-Übermittlung muss vor dem Erstellen des Abonnements der Berichtsserver für SMTP-Server- oder -Gateway-Verbindungen konfiguriert sein.  
  
-   Zum Verwenden der Dateifreigabeübermittlung müssen bereits Zielordner definiert sein. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Bevor Sie einen Bericht abonnieren können, muss die Berichtsdatenquelle so konfiguriert sein, dass gespeicherte oder keine Anmeldeinformationen verwendet werden. Weitere Informationen finden Sie unter [Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md). Wenn dies nicht der Fall ist, ist die Schaltfläche **Neues Abonnement** nicht verfügbar.  
  
 In diesem Thema wird nicht erläutert, wie ein datengesteuertes Abonnement erstellt wird. Informationen zum Erstellen eines datengesteuerten Abonnements finden Sie unter [Erstellen eines datengesteuerten Abonnements &#40;SSRS-Tutorial&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) oder in der Onlinehilfe zur Seite „Erstellen eines datengesteuerten Abonnements im Berichts-Manager“.  
  
###  <a name="bkmk_create_fileshare_subscription"></a> So erstellen Sie ein Dateifreigabeabonnement  
  
1.  Starten Sie den [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navigieren Sie zu dem Bericht, den Sie abonnieren möchten. Klicken Sie auf das Berichtsmenü, und klicken Sie auf **Abonnieren**.  
  
     ![Menü ' Bericht '](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "Menü ' Bericht '")  
  
3.  **Beschreibung**: Geben Sie eine Beschreibung für den Bericht ein, die maximal 512 Zeichen lang ist.  
  
4.  **Besitzer**: Das Besitzerfeld hat den aktuellen Benutzer als Standardwert und kann nicht bearbeitet werden, wenn Sie ein Abonnement erstellen. Nachdem das Abonnement gespeichert ist, können Sie jedoch die Eigenschaften des Abonnements ändern, einschließlich des Besitzers und der Beschreibung.  
  
5.  **Übermittelt von**: Wählen Sie die Option **Windows-Dateifreigabe**aus.  
  
6.  **Dateiname**: Geben Sie einen Dateinamen für den Bericht ein.  
  
7.  **Beim Erstellen der Datei eine Erweiterung hinzufügen**: Diese Option fügt dem Dateinamen eine Erweiterung um drei Zeichen hinzu. Die Dateierweiterung wird vom Berichtsausgabeformat bestimmt, das Sie auswählen.  
  
8.  **Pfad**: Geben Sie einen Pfad (UNC = Universal Naming Convention) zu einem vorhandenen Ordner, in dem Sie die Berichte zu übermitteln möchten (z. B. \\ \\< Servername\>\\< Myreports\>). Beginnen Sie die Pfadangabe mit zwei umgekehrten Schrägstrichen (\\). Geben Sie keinen umgekehrten Schrägstrich am Ende an.  
  
     ![Datei-Freigabe-Abonnement](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "file Share-Abonnement")  
  
9. **Renderformat**: Wählen Sie ein Berichtsausgabeformat zur Dateiübermittlung aus. Wählen Sie ein Format aus, das der Desktopanwendung entspricht, die Sie verwenden, um den Bericht zu öffnen. Vermeiden Sie Formate, die einen Bericht nicht in einem einzigen Datenstrom rendern oder die Interaktivität einführen, die in einer statischen Datei (beispielsweise HTML 4.0) nicht unterstützt wird.  
  
10. **Anmeldeinformationen**: Wählen Sie aus, ob Sie das Dateifreigabekonto oder normale Windows-Benutzeranmeldeinformationen verwenden möchten. **Dateifreigabekonto verwenden** ist deaktiviert, wenn Ihr Berichtsadministrator kein Dateifreigabekonto konfiguriert hat. Weitere Informationen finden Sie unter [Abonnementeinstellungen und ein Dateifreigabekonto &#40;Konfigurations-Manager&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md). In der **Benutzername** und **Kennwort** Textfelder, geben Sie die erforderlichen Anmeldeinformationen zum Zugriff auf die Dateifreigabe, mit dem Format  *\<Domäne >*\\*\<Benutzername >* für den Benutzernamen ein.  
  
11. **Optionen für das Überschreiben**:  
  
    -   **Die Datei nicht überschreiben, wenn eine frühere Version vorhanden ist**: Die Übermittlung wird nicht durchgeführt, falls eine vorhandene Datei erkannt wird.  
  
    -   **Dateinamen inkrementieren, wenn neuere Versionen hinzugefügt werden**: Der Berichtsserver fügt eine Zahl an den Dateinamen an, um ihn von vorhandenen Dateien des gleichen Namens zu unterscheiden.  
  
12. **Zeitplan**: Geben Sie an, wann der Bericht übermittelt werden soll:  
  
    -   Klicken Sie zum Festlegen eines Übermittlungszeitpunkts auf **Wenn die geplante Berichtsausführung abgeschlossen ist** , und klicken Sie auf **Zeitplan auswählen** . Eine Zeitplanseite wird geöffnet.  
  
    -   Um einen vordefinierten, freigegebenen Zeitplan auszuwählen, der bereits über das gewünschte Datum, die Uhrzeit und Wiederholungsinformationen verfügt, klicken Sie auf **Nach einem freigegebenen Zeitplan**, und wählen Sie dann den gewünschten Zeitplan aus.  
  
    -   Klicken Sie auf**Nach Aktualisierung des Berichtsinhalts**, um einen Bericht zu übermitteln, wenn eine Berichtsmomentaufnahme mit einer neueren Version aktualisiert wurde. Wenn Sie einen Bericht abonnieren, der Daten zu geplanten Zeiten abruft, legt der Zeitplan für die Aktualisierung der Daten fest, wann das Abonnement verarbeitet wird.  
  
        > [!NOTE]  
        >  Diese Option ist nur für Momentaufnahmen verfügbar, die bereits einem Updatezeitplan zugeordnet sind.  
  
13. Geben Sie für einen parametrisierten Bericht Parameter an, die für den Bericht in diesem Abonnement verwendet werden sollen. Die Parameter können sich von denen unterscheiden, die für die Ausführung des Berichts bei Bedarf oder in anderen geplanten Vorgängen verwendet werden.  
  
 Der Bericht wird als statische Datei übermittelt. Wenn der Bericht interaktive Funktionen enthält (z. B. Links zu zusätzlichen Zeilen oder Spalten), stehen diese Funktionen nicht zur Verfügung.  
  
###  <a name="bkmk_create_email_subscription"></a> So erstellen Sie ein E-Mail-Abonnement  
  
1.  Starten Sie den [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navigieren Sie zu dem Bericht, den Sie abonnieren möchten. Klicken Sie auf das Berichtsmenü, und klicken Sie auf **Abonnieren**.  
  
     ![Menü ' Bericht '](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "Menü ' Bericht '")  
  
3.  **Beschreibung**: Geben Sie eine Beschreibung für den Bericht ein, die maximal 512 Zeichen lang ist.  
  
4.  **Besitzer**: Das Besitzerfeld hat den aktuellen Benutzer als Standardwert und kann nicht bearbeitet werden, wenn Sie ein Abonnement erstellen. Nachdem das Abonnement gespeichert ist, können Sie jedoch die Eigenschaften des Abonnements ändern, einschließlich des Besitzers und der Beschreibung.  
  
5.  **Übermittelt von**: Wählen Sie **E-Mail**aus. Falls **E-Mail** nicht verfügbar ist, wurde der Berichtsserver nicht für E-Mail-Abonnements konfiguriert. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
6.  **An**: Der Empfängername im „An:“-Feld ist selbstadressiert, wofür Ihr Domänenbenutzerkonto verwendet wird. Stellen Sie sicher, dass das Format [Benutzernamename]@[Domäne.com] ist. Berichtsserver-Konfigurationseinstellungen legen fest, ob das Feld **An** bereits mit Ihrem Benutzerkonto ausgefüllt wird. Weitere Informationen zur Änderung der Konfigurationseinstellungs-E-Mail-Adressen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
    > [!NOTE]  
    >  Abhängig von Ihren Berechtigungen können Sie auch die E-Mail-Adresse eingeben, an die der Bericht geliefert werden soll. Mehrere E-Mail-Adressen müssen durch ein Semikolon (;) getrennt werden. Sie können weitere E-Mail-Adressen in die Textfelder **Cc**, **Bcc**und **Antwort an** eingeben. Für dieses Verfahren müssen Sie über die Berechtigung zum Verwalten von Abonnements verfügen.  
  
7.  **Betreff**: standardmäßig auf "@ReportName wurde ausgeführt am @ExecutionTime". Sie können den Betreff bearbeiten, aber beachten Sie, dass die @ReportName und @ExecutionTime sind die einzigen globalen Variablen in unterstützt die **Betreff** Feld.  
  
8.  Wählen Sie die Übermittlungsoptionen wie folgt aus:  
  
    -   **Bericht einschließen**: Wählen Sie diese Option aus, um eine Kopie des Berichts einzubetten oder anzufügen. Das Format des Berichts wird durch das ausgewählte Renderingformat bestimmt. Wählen Sie diese Option nicht aus, wenn Sie annehmen, dass die Berichtsgröße das maximale Limit des E-Mail-Systems überschreitet.  
  
    -   **Link einschließen**: Wählen Sie diese Option aus, um einen URL-Link zum Bericht im Textkörper der E-Mail-Nachricht einzuschließen.  
  
    > [!NOTE]  
    >  Wenn Sie diese beiden Optionen deaktivieren, wird nur der Benachrichtigungstext in der Betreffzeile gesendet.  
  
9. Wählen Sie ein Renderingformat aus dem Listenfeld **Renderformat** aus. Diese Option ist verfügbar, wenn Sie die Option **Bericht einschließen** auswählen, um eine Kopie des Berichts einzubetten oder anzufügen.  
  
    -   Um den Bericht in den Textkörper der E-Mail-Nachricht einzubetten, wählen Sie **Webarchiv**aus.  
  
    -   Um den Bericht als Anhang zu senden, wählen Sie eines der anderen Renderingformate aus.  
  
10. Wählen im Listenfeld **Priorität** eine Priorität aus. In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange legt diese Einstellung ein Flag für die Wichtigkeitsstufe der E-Mail-Nachricht fest.  
  
11. Geben Sie an, wann der Bericht übermittelt werden soll:  
  
    -   Klicken Sie zum Planen eines Übermittlungszeitpunkts auf **Wenn die geplante Berichtsausführung abgeschlossen ist** , und klicken Sie auf **Zeitplan auswählen**. Eine Zeitplanseite wird geöffnet.  
  
    -   Um einen vordefinierten, freigegebenen Zeitplan auszuwählen, der bereits über das gewünschte Datum, die Uhrzeit und Wiederholungsinformationen verfügt, klicken Sie auf **Nach einem freigegebenen Zeitplan**, und wählen Sie dann den gewünschten Zeitplan aus.  
  
    -   Klicken Sie auf**Nach Aktualisierung des Berichtsinhalts**, um einen Bericht zu übermitteln, wenn eine Berichtsmomentaufnahme mit einer neueren Version aktualisiert wurde. Wenn Sie einen Bericht abonnieren, der Daten zu geplanten Zeiten abruft, legt der Zeitplan für die Aktualisierung der Daten fest, wann das Abonnement verarbeitet wird.  
  
    > [!NOTE]  
    >  Diese Option ist nur für Momentaufnahmen verfügbar, die bereits einem Updatezeitplan zugeordnet sind.  
  
12. Geben Sie für einen parametrisierten Bericht Parameter an, die für den Bericht in diesem Abonnement verwendet werden sollen. Die von Ihnen angegebenen Parameter können sich von denen unterscheiden, die für die Ausführung des Berichts bei Bedarf oder in anderen geplanten Vorgängen verwendet werden.  
  
##  <a name="bkmk_modify_subscription"></a> So ändern Sie ein Abonnement  
 Ein Abonnement kann jederzeit geändert werden. Falls Sie ein Abonnement ändern, während es verarbeitet wird, werden die aktualisierten Einstellungen verwendet, falls sie im Berichtsserver gespeichert sind, bevor die Übermittlungserweiterung die Abonnementdaten erhält. Andernfalls werden die vorhandenen Einstellungen verwendet.  
  
 Ein Benutzer, der ein Abonnement erstellt, ist Besitzer dieses Abonnements. Jeder Benutzer kann seine eigenen Abonnements ändern oder löschen. Sie können den Besitzer des Berichts aus der Seite mit den Abonnementseigenschaften, oder programmgesteuert automatisch ändern. Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [Verwenden von PowerShell, um Reporting Services-Abonnenten zu ändern und aufzulisten sowie ein Abonnement auszuführen](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 Um nach einem Abonnement zu suchen, verwenden Sie die Seite **Meine Abonnements** , oder zeigen Sie die mit einem Bericht verknüpften Abonnementdefinitionen an. Es ist nicht möglich, direkt oder basierend auf Besitzernamen, Triggerinformationen, Statusinformationen usw. nach einem Abonnement zu suchen.  
  
 Abonnements können auch von Berichtsserveradministratoren geändert oder gelöscht werden.  
  
> [!NOTE]  
>  Ein Berichtsserveradministrator kann nicht zentral alle einzelnen Abonnements verwalten, die auf einem bestimmten Berichtsserver verwendet werden. Berichtsserveradministratoren können jedoch auf jedes einzelne Abonnement zugreifen, um es zu ändern oder zu löschen.  
  
##  <a name="bkmk_delete_subscription"></a> So löschen Sie ein Abonnement  
 So löschen Sie ein Abonnement  
  
1.  Starten Sie den [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Klicken Sie im Berichts-Manager auf der Symbolleiste auf **Meine Abonnements** , und navigieren Sie zu dem Abonnement, das Sie ändern oder löschen möchten.  
  
3.  Öffnen Sie das Berichtsmenü, und klicken Sie auf **Löschen**.  
  
     ![Menü ' Bericht '](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "Menü ' Bericht '")  
  
 Informationen zum Beenden eines Abonnements, das zurzeit auf dem Berichtsserver ausgeführt wird, finden Sie unter [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
 Falls Sie ein Abonnement beenden möchten und es nicht finden können, notieren Sie sich den Bericht, den Sie erhalten, und suchen Sie anhand des Namens danach. Wenn Sie auf den Bericht zugegriffen haben, können Sie sich aus dem Abonnement entfernen. Falls Sie das Abonnement nicht finden können, handelt es sich möglicherweise um ein datengesteuertes Abonnement. Weitere Informationen erhalten Sie von Ihrem Berichtsserveradministrator.  
  
 Ein Abonnement wird automatisch gelöscht, wenn der zugrunde liegende Bericht gelöscht wird. Wenn Sie ein Abonnement während der Verarbeitung löschen, wird das Abonnement beendet, falls der Löschvorgang durchgeführt wird, bevor die Übermittlungserweiterung die Abonnementdaten erhält. Andernfalls wird die Verarbeitung des Abonnements fortgesetzt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Abonnements für Berichtsserver im SharePoint-Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Verwenden von PowerShell, um Reporting Services-Abonnenten zu ändern und aufzulisten sowie ein Abonnement auszuführen](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Verwenden von „Meine Abonnements“ &#40;Berichtsserver im einheitlichen Modus&#41;](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
  
  
