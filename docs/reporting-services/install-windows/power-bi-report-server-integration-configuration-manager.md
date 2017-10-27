---
title: Power BI-Bericht-Server-Integration (Konfigurations-Manager) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: c6f8c9440a6229726c655dae42ea7ab955e35f54
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---

# <a name="power-bi-report-server-integration-configuration-manager"></a>Berichtsserverintegration für Power BI (Configuration Manager)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Die Seite  **Power BI-Integration** in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Configuration Manager wird zum Registrieren des Berichtsservers mit dem gewünschten verwalteten Azure Active Directory-Mandanten verwendet, um es Benutzern des Berichtsservers zu ermöglichen, unterstützte Elemente an [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Dashboards anzuheften. Eine Liste der unterstützten Elemente, die angeheftet werden können, finden Sie unter [Anheften von Reporting Services-Elementen an Power BI-Dashboards](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).

##  <a name="bkmk_requirements"></a> Anforderungen für die Power BI-Integration

Zusätzlich zu einer aktiven Internetverbindung zum Öffnen des [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Diensts sind die folgenden Anforderungen zum Abschließen der Integration von [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]erforderlich.

- **Azure Active Directory:** Ihr Unternehmen muss Azure Active Directory verwenden, das die Verzeichnis- und Identitätsverwaltung für Azure-Dienste und Webanwendungen bietet. Weitere Informationen finden Sie unter [Neuigkeiten von Azure Active Directory?](https://azure.microsoft.com/documentation/articles/active-directory-whatis/)

- **Verwalteter Mandant:** Das [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Dashboard, an das Sie Berichtselemente anheften möchten, muss Teil eines verwalteten Azure AD-Mandanten sein.  Ein verwalteter Mandant wird automatisch beim erstmaligen Abonnieren der Azure-Dienste wie Office 365 und Microsoft Intune für Ihr Unternehmen erstellt.   Virale Mandanten werden derzeit nicht unterstützt.  Weitere Informationen finden Sie in den Abschnitten „Erläuterung zum Azure AD-Mandanten“ und „Gewusst wie: Abrufen eines Azure AD-Verzeichnisses“ in [Erläuterungen zum Azure AD-Verzeichnis](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).

- Der Benutzer, der die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Integration durchführt, muss ein Mitglied des Azure AD-Mandanten, ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Systemadministrator und ein Systemadministrator für die ReportServer-Katalogdatenbank sein.

- Der Benutzer, der die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Integration durchführt, muss den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager über das zum Installieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]verwendete Konto oder über das Konto starten, unter dem der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst ausgeführt wird.

- Berichte, aus denen Sie Informationen anheften möchten, müssen gespeicherte Anmeldeinformationen verwenden. Dies ist keine Voraussetzung für die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Integration selbst, aber für den Aktualisierungsprozess für die angehefteten Elemente.  Beim Anheften eines Berichtselements wird ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnement zum Verwalten des Aktualisierungszeitplans der Kacheln in [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]erstellt. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnements: Erfordern gespeicherte Anmeldeinformationen. Wenn ein Bericht keine gespeicherten Anmeldeinformationen verwendet, kann ein Benutzer weiterhin Berichtselemente anheften, aber wenn das zugehörige Abonnement versucht, die Daten auf [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]zu aktualisieren, wird eine Fehlermeldung angezeigt, die der folgenden Meldung auf der Seite **Meine Abonnements** ähnelt.

        PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credential.

Weitere Informationen zum Speichern von Anmeldeinformationen finden im Abschnitt "Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle" in [Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).

Ein Administrator kann die  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Protokolldateien auf weitere Informationen überprüfen.  Es werden Meldungen wie die Folgenden angezeigt. Eine hervorragende Möglichkeit zum Überprüfen und Überwachen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Protokolldateien ist die Verwendung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Power Query für die Dateien.  Weitere Informationen und ein kurzes Video finden Sie unter [Berichtsserverdienst-Ablaufverfolgungsprotokoll](../../reporting-services/report-server/report-server-service-trace-log.md).

    subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified.

    notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error occurred processing subscription fcdb8581-d763-4b3b-ba3e-8572360df4f9: PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared data set. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified.

##  <a name="bkmk_steps2integrate"></a> So integrieren und registrieren Sie den Berichtsserver

Führen Sie die folgenden Schritte des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Managers aus. Weitere Informationen finden Sie unter [Konfigurations-Manager für Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).

1. Wählen Sie die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Integrationsseite aus.

2. Wählen Sie **Mit Power BI registrieren**aus.

3. Im [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Anmeldedialogfeld geben Sie die Anmeldeinformationen ein, die Sie zum Anmelden bei [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]verwenden.

4. Nach Abschluss der Registrierung führt der Abschnitt **Power BI-Registrierungsdaten** die Azure-Mandanten-ID und die Umleitungs-URL(s) auf.  Die URLs werden im Rahmen der Anmeldung und der Kommunikation für das [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Dashboard verwendet, um mit dem registrierten Berichtsserver kommunizieren zu können.

5. Klicken Sie auf die Schaltfläche **Kopieren** des Fensters **Ergebnisse** , um die Registrierungsdetails in die Windows-Zwischenablage zu kopieren, damit Sie sie für die zukünftige Verwendung speichern können.

##  <a name="bkmk_unregister"></a> Aufheben der Registrierung mit Power BI

**Registrierung aufheben:** Das Aufheben der Registrierung für den Berichtsserver aus Azure Active Directory führt zu Folgendem:

- Die **Meine Einstellungen** Link wird nicht mehr von der Web-portalmenüleiste sichtbar sein.

- Berichtselemente, die bereits angeheftet wurden, sind weiterhin auf Dashboards angeheftet. Die Kacheln auf dem Dashboard werden jedoch nicht mehr aktualisiert.

- Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnements, die die Kacheln aktualisiert haben, sind weiterhin auf dem Berichtsserver vorhanden, aber wenn sie zum konfigurierten Zeitplan ausgeführt werden, zeigen sie eine Fehlermeldung wie die Folgende an.

    **Die Übermittlungserweiterung für dieses Abonnement konnte nicht geladen werden.**

Wählen Sie auf der Seite **Power BI** in Configuration Manager die Schaltfläche **Aufheben der Registrierung mit Power BI** aus.

##  <a name="bkmk_updateregistration"></a> Aktualisieren der Registrierung

Verwenden Sie die Option **Registrierung aktualisieren** , wenn die Konfiguration des Berichtsservers geändert wurde. Wenn Sie z. B. die URLs hinzufügen oder entfernen möchten, die Benutzer für die Navigation zum [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]verwenden.

- Wählen Sie in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager die **Webportal-URL**aus.

     Wählen Sie **Erweitert**aus.

- Wählen Sie **Hinzufügen** aus, um eine neue HTTP-Identität für das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] hinzuzufügen, und wählen Sie dann **OK**aus.

     Das [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Symbol wird geändert, um die Änderung der Serverkonfiguration anzuzeigen.  ![Ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "Ssrs_powebi_icon_warning")

- Wählen Sie auf der Seite **Power BI-Integration** die Option **Aktualisieren der Registrierung**aus.

     Sie werden aufgefordert, sich bei Azure AD anzumelden. Die Seite wird aktualisiert und es wird die neue URL angezeigt, die in **Umleitungs-URLs**aufgeführt ist.

##  <a name="bkmk_integration_process"></a> Zusammenfassung der Power BI-Integration und des Anheftungsprozesses

In diesem Abschnitt werden die grundlegenden Schritte und die damit verbundenen Technologien zusammengefasst, die in die Integration des Berichtsservers mit [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] und das Anheften eines Berichtselements an ein Dashboard einbezogen sind.

 **Integrieren:**

1. Wenn Sie in Configuration Manager die Schaltfläche **Mit Power BI registrieren** auswählen, werden Sie aufgefordert, sich bei Azure Active Directory anzumelden.

2. Die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Client-App wird mit Ihrem verwalteten Mandanten registriert.

3. Die Power BI-Clientanwendung wird in Ihrem verwalteten Mandanten in Azure Active Directory erstellt.

4. Die Registrierung umfasst Umleitungs-URLs, die verwendet werden, wenn sich Benutzer vom Berichtsserver anmelden.  Die App-ID und die URLs werden in der ReportServer-Datenbank gespeichert. Die Umleitungs-URL wird während der Authentifizierungsaufrufe in Azure verwendet, sodass der Aufruf an den Berichtsserver zurückgegeben werden kann. Z. B. wenn Benutzer anmelden oder Elemente an ein Dashboard anheften.

5. Die App-ID und URLS werden in Configuration Manager angezeigt.

 ![Ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "Ssrs_pbiflow_integration")

 **Wenn ein Benutzer ein Berichtselement an ein Dashboard anheftet:**

1. Benutzer zeigen eine Berichtsvorschau im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] an. Wenn sie das erste Mal klicken, um ein Berichtselement aus dem [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]anzuheften.

2. Sie werden zur Azure Active Directory-Anmeldeseite umgeleitet. Sie können sich auch über die Seite [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] **My Settings** page. Wenn sich Benutzer bei einem verwalteten Azure-Mandanten anmelden, wird eine Beziehung zwischen dem Azure-Konto und den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berechtigungen erstellt.  Weitere Informationen finden Sie unter [Eigene Einstellungen für die Power BI-Integration &#40;Webportal&#41;](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5).

3. Ein Benutzersicherheitstoken wird an den Berichtsserver zurückgegeben.

4. Das Benutzersicherheitstoken wird in der ReportServer-Datenbank gespeichert.

5. Eine Liste der Gruppen und Dashboards, auf die der Benutzer Zugriff hat, werden von dem [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Dienst abgerufen.  Der Benutzer wählt die Zielgruppe und das Zieldashboard aus und konfiguriert, wie oft die Daten auf der [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Kachel aktualisiert werden sollen.

6. Das Berichtselement wird an das Dashboard angeheftet.

7. Es wird ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnement erstellt, um die geplante Aktualisierung des Berichtselements auf der Dashboardkachel zu verwalten. Das Abonnement verwendet das Sicherheitstoken, das bei der Anmeldung des Benutzers erstellt wurde.

     Das Token ist gut für **90 Tage**, nach denen die Benutzer sich erneut anmelden, um ein neues Benutzertoken zu erstellen müssen. Wenn das Token abgelaufen ist, werden die angehefteten Kacheln weiterhin im Dashboard angezeigt, aber die Daten werden nicht mehr aktualisiert.  Die für angeheftete Elemente verwendeten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnements weisen einen Fehler auf, bis ein neues Benutzertoken erstellt wird. Finden Sie unter [Meine Einstellungen für Power BI-Integration &#40; Webportal &#41;](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5). .

Wenn ein Benutzer ein Element ein zweites Mal anheftet, werden die Schritte 1 bis 4 übersprungen und stattdessen die App-ID und die URLs aus der ReportServer-Datenbank abgerufen. Der Ablauf wird dann mit Schritt 5 fortgesetzt.

![ssRS-pin-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **Wenn ein Abonnement ausgelöst wird, um eine Dashboardkachel zu aktualisieren:**

1. Wenn das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnement ausgelöst wird, wird der Bericht gerendert.

2. Das Benutzertoken wird aus der ReportServer-Datenbank abgerufen.

3. Das Zustand und die Daten des Berichtselements werden mit dem Token an den [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]-Dienst gesendet.

4. Das Token wird zur Überprüfung an Azure AD gesendet. Wenn das Token gültig ist, werden die Daten des Berichts an die Dashboardkachel gesendet, und die Date-Eigenschaft der Kachel wird aktualisiert.

5. Wenn das Token nicht gültig ist, wird ein Fehler zurückgegeben und auf dem Berichtsserver protokolliert.  Es werden keine Statusinformationen oder sonstigen Informationen an das Dashboard gesendet.

![ssRS-subscription-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="next-steps"></a>Nächste Schritte

[Meine Einstellungen für die Power BI-Integration](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5)  
[Anheften von Reporting Services-Elementen an Power BI-Dashboards](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

