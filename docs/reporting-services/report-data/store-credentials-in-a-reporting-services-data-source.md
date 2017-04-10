---
title: "Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "09/23/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anmeldeinformationen [Reporting Services]"
  - "Sicherheit [Analysis Services ], Datenquellen"
  - "Gespeicherte Anmeldeinformationen [Reporting Services]"
  - "Datenquellen [Reporting Services] gespeicherte Anmeldeinformationen"
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle
  Sie können gespeicherte Anmeldeinformationen, mit denen ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver auf externe Daten für einen Bericht zugreift, konfigurieren. Gespeicherte Anmeldeinformationen werden verwendet, wenn der unbeaufsichtigt ausgeführt, beispielsweise bei einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Abonnement, das einen Bericht als E-Mail veröffentlicht. Der Berichtsserver ruft die Anmeldeinformationen ab und verwendet sie, wenn die Berichtsverarbeitung geplant oder ausgelöst wird. In diesem Thema werden die einzelnen Schritte für die Konfiguration gespeicherter Anmeldeinformationen für Berichtsserver im einheitlichen Modus und im SharePoint-Modus dargestellt.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus|  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (einheitlicher Modus)](#bkmk_stored_credentials_data_source_native)  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (SharePoint-Modus)](#bkmk_stored_credentials_data_source_sharepoint)  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (einheitlicher Modus)](#bkmk_stored_credentials_shared_data_source_native)  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (SharePoint-Modus)](#bkmk_stored_credentials_shared_data_source_sharepoint)  
  
##  <a name="bkmk_top"></a> Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen  
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.png "as_powerpivot_refresh_sss_set_key") Das Konto, dass Sie für gespeicherte Anmeldeinformationen verwenden, muss für eine der folgenden Sicherheitsrichtlinien auf dem Berichtsserver konfiguriert sein. Es wird empfohlen, dass Sie die Richtlinie mit den mindestens erforderlichen Berechtigungen für Ihre Umgebung auswählen.  
  
1.  **Lokal anmelden zulassen**. Weitere Informationen finden Sie unter [Lokal anmelden zulassen](http://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Anmelden als Stapelverarbeitungsauftrag**. Weitere Informationen finden Sie unter [Anmelden als Stapelverarbeitungsauftrag](http://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Allgemeine Informationen zu Richtlinien finden Sie unter [Bearbeiten von Sicherheitseinstellungen für ein Gruppenrichtlinienobjekt](http://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (einheitlicher Modus)  
  
1.  Navigieren Sie im Berichts-Manager im einheitlichen Modus zu dem Ordner, der den Bericht enthält. Klicken Sie auf das Elementkontextmenü ![Kontextmenü im Berichts-Manager für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "Kontextmenü im Berichts-Manager für SSRS-Elemente").  
  
2.  Klicken Sie auf **Verwalten** und dann auf **Datenquellen**.  
  
3.  Wählen Sie **Eine benutzerdefinierte Datenquelle**.  
  
4.  Wählen Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung aus, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] hergestellt wird:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Wählen Sie für **Verbindung herstellen über**die Option **Anmeldeinformationen, die sicher auf dem Berichtsserver gespeichert sind**aus.  
  
7.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und wählen Sie dann **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden** aus.  
  
    -   Wenn Benutzername und Kennwort Datenbank-Anmeldeinformationen sind, wählen Sie **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden**nicht aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, können Sie die Option **Die Identität des authentifizierten Benutzers annehmen, nachdem eine Verbindung zur Datenquelle hergestellt wurde**auswählen.  
  
8.  Klicken Sie auf **Anwenden**.  
  
     ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (SharePoint-Modus)  
  
1.  Navigieren Sie zur Dokumentbibliothek, die den Bericht enthält, und klicken Sie dann auf das Menü zum Öffnen ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für SSRS-Elemente").  
  
2.  Klicken Sie auf das zweite Menü zum Öffnen ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für SSRS-Elemente"), und klicken Sie dann auf **Datenquellen verwalten**.  
  
3.  Klicken Sie auf den Namen der **benutzerdefinierten** Datenquelle, die Sie mit gespeicherten Anmeldeinformationen konfigurieren möchten.  
  
4.  Wählen Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung aus, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] hergestellt wird:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Wählen Sie für **Anmeldeinformationen**die Option **Gespeicherte Anmeldeinformationen**aus.  
  
7.  Geben Sie einen **Benutzernamen** und ein **Kennwort**ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und wählen Sie dann **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden** aus.  
  
    -   Wenn der Benutzername und das Kennwort Datenbankanmeldeinformationen sind, wählen Sie nicht **Als Windows-Anmeldeinformationen verwenden**aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, wählen Sie ggf. die Option **Ausführungskontext für dieses Konto festlegen**aus.  
  
8.  Klicken Sie auf **OK**.  
  
     ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (einheitlicher Modus)  
  
1.  Navigieren Sie im Berichts-Manager im einheitlichen Modus zum freigegebenen Datenquellenelement. ![Freigegebene Datenquelle (Symbol)](../../reporting-services/report-data/media/hlp-16datasource.png "Freigegebene Datenquelle (Symbol)")  
  
2.  Klicken Sie auf das Kontextmenü ![Kontextmenü im Berichts-Manager für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "Kontextmenü im Berichts-Manager für SSRS-Elemente") und dann auf **Verwalten**.  
  
3.  Geben Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
4.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und wählen Sie dann **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden** aus.  
  
    -   Wenn Benutzername und Kennwort Datenbank-Anmeldeinformationen sind, wählen Sie **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden**nicht aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, können Sie die Option **Die Identität des authentifizierten Benutzers annehmen, nachdem eine Verbindung zur Datenquelle hergestellt wurde**auswählen.  
  
6.  Klicken Sie auf **Anwenden**.  
  
     ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (SharePoint-Modus)  
  
1.  Navigieren Sie in der Dokumentbibliothek zum freigegebenen Datenquellenelement.![Freigegebene Datenquelle (Symbol)](../../reporting-services/report-data/media/hlp-16datasource.png "Freigegebene Datenquelle (Symbol)")  
  
2.  Klicken Sie auf das Kontextmenü ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für SSRS-Elemente") und dann auf das zweite Kontextmenü ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für SSRS-Elemente").  
  
3.  Klicken Sie auf **Datenquellendefinition bearbeiten**.  
  
4.  Geben Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und wählen Sie dann **Windows-Anmeldeinformationen verwenden** aus.  
  
    -   Wenn der Benutzername und das Kennwort Datenbankanmeldeinformationen sind, wählen Sie nicht **Als Windows-Anmeldeinformationen verwenden**aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, wählen Sie ggf. die Option **Ausführungskontext für dieses Konto festlegen**aus.  
  
7.  Klicken Sie auf **OK**.  
  
     ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
## Siehe auch  
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Konfigurieren von Datenquelleneigenschaften für einen Bericht &#40;Berichts-Manager&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [Datenquellen &#40;Seite „Eigenschaften“, Berichts-Manager&#41;](../Topic/Data%20Sources%20Properties%20Page%20\(Report%20Manager\).md)   
 [Neue Datenquelle &#40;Seite, Berichts-Manager&#41;](../Topic/New%20Data%20Source%20Page%20\(Report%20Manager\).md)  
  
  