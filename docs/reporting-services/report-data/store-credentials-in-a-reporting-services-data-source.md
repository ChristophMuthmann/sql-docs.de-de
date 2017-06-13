---
title: Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 09/23/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ca8d81025d48af07b5e2ce9336a8e031ea4fb1a
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle
  Sie können gespeicherte Anmeldeinformationen, mit denen ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver auf externe Daten für einen Bericht zugreift, konfigurieren. Gespeicherte Anmeldeinformationen werden verwendet, wenn der unbeaufsichtigt ausgeführt, beispielsweise bei einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnement, das einen Bericht als E-Mail veröffentlicht. Der Berichtsserver ruft die Anmeldeinformationen ab und verwendet sie, wenn die Berichtsverarbeitung geplant oder ausgelöst wird. In diesem Thema werden die einzelnen Schritte für die Konfiguration gespeicherter Anmeldeinformationen für Berichtsserver im einheitlichen Modus und im SharePoint-Modus dargestellt.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus|  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (einheitlicher Modus)](#bkmk_stored_credentials_data_source_native)  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (SharePoint-Modus)](#bkmk_stored_credentials_data_source_sharepoint)  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (einheitlicher Modus)](#bkmk_stored_credentials_shared_data_source_native)  
  
-   [Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (SharePoint-Modus)](#bkmk_stored_credentials_shared_data_source_sharepoint)  
  
##  <a name="bkmk_top"></a> Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen  
 ![As_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "As_powerpivot_refresh_sss_set_key") ist es erforderlich, das Konto, das Sie für gespeicherte Anmeldeinformationen verwenden, das für eine der folgenden Sicherheitsrichtlinien auf dem Berichtsserver konfiguriert ist. Es wird empfohlen, dass Sie die Richtlinie mit den mindestens erforderlichen Berechtigungen für Ihre Umgebung auswählen.  
  
1.  **Lokal anmelden zulassen**. Weitere Informationen finden Sie unter [Lokal anmelden zulassen](http://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Anmelden als Stapelverarbeitungsauftrag**. Weitere Informationen finden Sie unter [Anmelden als Stapelverarbeitungsauftrag](http://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Allgemeine Informationen zu Richtlinien finden Sie unter [Bearbeiten von Sicherheitseinstellungen für ein Gruppenrichtlinienobjekt](http://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (einheitlicher Modus)  
  
1.  Navigieren Sie im Berichts-Manager im einheitlichen Modus zu dem Ordner, der den Bericht enthält. Klicken Sie auf das Elementkontextmenü ![Kontextmenü im Berichts-Manager für Ssrs-Elemente](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "Kontextmenü im Berichts-Manager für Ssrs-Elemente").  
  
2.  Klicken Sie auf **Verwalten** und dann auf **Datenquellen**.  
  
3.  Wählen Sie **Eine benutzerdefinierte Datenquelle**.  
  
4.  Wählen Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung aus, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] hergestellt wird:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Wählen Sie für **Verbindung herstellen über**die Option **Anmeldeinformationen, die sicher auf dem Berichtsserver gespeichert sind**aus.  
  
7.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben sie im folgenden Format: \<Domäne >\\< Konto\>, und wählen Sie dann **als Windows-Anmeldeinformationen beim Verbinden mit der Datenquelle verwenden.**  
  
    -   Wenn Benutzername und Kennwort Datenbank-Anmeldeinformationen sind, wählen Sie **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden**nicht aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, können Sie die Option **Die Identität des authentifizierten Benutzers annehmen, nachdem eine Verbindung zur Datenquelle hergestellt wurde**auswählen.  
  
8.  Klicken Sie auf **Anwenden**.  
  
     ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (SharePoint-Modus)  
  
1.  Navigieren Sie zu der Dokumentbibliothek mit dem Bericht, und klicken Sie dann auf das Menü öffnen ![Kontextmenü der Dokumentbibliothek für Ssrs-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für Ssrs-Elemente").  
  
2.  Klicken Sie auf die zweite Menü zum Öffnen ![Kontextmenü der Dokumentbibliothek für Ssrs-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für Ssrs-Elemente") , und klicken Sie dann auf **Datenquellen verwalten**.  
  
3.  Klicken Sie auf den Namen der **benutzerdefinierten** Datenquelle, die Sie mit gespeicherten Anmeldeinformationen konfigurieren möchten.  
  
4.  Wählen Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung aus, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] hergestellt wird:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Wählen Sie für **Anmeldeinformationen**die Option **Gespeicherte Anmeldeinformationen**aus.  
  
7.  Geben Sie einen **Benutzernamen** und ein **Kennwort**ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben sie im folgenden Format: \<Domäne >\\< Konto\>, und wählen Sie dann **als Windows-Anmeldeinformationen beim Verbinden mit der Datenquelle verwenden.**  
  
    -   Wenn der Benutzername und das Kennwort Datenbankanmeldeinformationen sind, wählen Sie nicht **Als Windows-Anmeldeinformationen verwenden**aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, wählen Sie ggf. die Option **Ausführungskontext für dieses Konto festlegen**aus.  
  
8.  Klicken Sie auf **OK**.  
  
     ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (einheitlicher Modus)  
  
1.  Navigieren Sie im Berichts-Manager im einheitlichen Modus zum freigegebenen Datenquellenelement. ![Symbol für freigegebene Datenquelle](../../reporting-services/report-data/media/hlp-16datasource.png "Symbol für freigegebene Datenquelle")  
  
2.  Klicken Sie im Kontextmenü den Befehl ![Kontextmenü im Berichts-Manager für Ssrs-Elemente](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "Kontextmenü im Berichts-Manager für Ssrs-Elemente") , und klicken Sie dann auf **verwalten**.  
  
3.  Geben Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
4.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben sie im folgenden Format: \<Domäne >\\< Konto\>, und wählen Sie dann **als Windows-Anmeldeinformationen beim Verbinden mit der Datenquelle verwenden.**  
  
    -   Wenn Benutzername und Kennwort Datenbank-Anmeldeinformationen sind, wählen Sie **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden**nicht aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, können Sie die Option **Die Identität des authentifizierten Benutzers annehmen, nachdem eine Verbindung zur Datenquelle hergestellt wurde**auswählen.  
  
6.  Klicken Sie auf **Anwenden**.  
  
     ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (SharePoint-Modus)  
  
1.  Navigieren Sie in der Dokumentbibliothek zum freigegebenen Datenquellenelement. ![Symbol für freigegebene Datenquelle](../../reporting-services/report-data/media/hlp-16datasource.png "Symbol für freigegebene Datenquelle")  
  
2.  Klicken Sie im Kontextmenü den Befehl ![Kontextmenü der Dokumentbibliothek für Ssrs-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für Ssrs-Elemente") , und klicken Sie dann auf das zweite Kontextmenü ![Kontextmenü der Dokumentbibliothek für Ssrs-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "Kontextmenü der Dokumentbibliothek für Ssrs-Elemente").  
  
3.  Klicken Sie auf **Datenquellendefinition bearbeiten**.  
  
4.  Geben Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben sie im folgenden Format: \<Domäne >\\< Konto\>, und wählen Sie dann **als Windows-Anmeldeinformationen verwenden.**  
  
    -   Wenn der Benutzername und das Kennwort Datenbankanmeldeinformationen sind, wählen Sie nicht **Als Windows-Anmeldeinformationen verwenden**aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, wählen Sie ggf. die Option **Ausführungskontext für dieses Konto festlegen**aus.  
  
7.  Klicken Sie auf **OK**.  
  
     ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Konfigurieren von Datenquelleneigenschaften für einen Bericht &#40;Berichts-Manager&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Datenquellen &#40;Seite „Eigenschaften“, Berichts-Manager&#41;](http://msdn.microsoft.com/library/f37edda0-19e6-489e-b544-8751fa6b6cfb)   
 [Neue Datenquelle &#40;Seite, Berichts-Manager&#41;](http://msdn.microsoft.com/library/35563d4c-a3d5-4f95-bf46-605da9dfcbb8)  
  
  

