---
title: Verwalten von Berichtsdatenquellen | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
caps.latest.revision: 52
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9791cd34a321173e30bf2016956f02e54e62112c
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="manage-report-data-sources"></a>Verwalten von Berichtsdatenquellen
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]rufen Berichte, Berichtsmodelle und datengesteuerte Abonnements Daten von externen Datenquellen ab. Zum Herstellen einer Verbindung mit einer externen Datenquelle verwendet ein Berichtsserver Verbindungsinformationen für die Datenquelle, die im Bericht, Modell oder Abonnement definiert werden oder auf die dort verwiesen wird. Verbindungseigenschaften der Datenquellen werden bei Erstellung des Berichts oder Modells definiert. Sie können jedoch unabhängig verwaltet werden, nachdem der Bericht oder das Modell auf einem Berichtsserver veröffentlicht wurde.  
  
 Wenn der Berichtsserver im integrierten SharePoint-Modus bereitgestellt wird, können Sie den Berichts-Manager für Berichtsserver im einheitlichen Modus oder Anwendungsseiten für SharePoint-Sites verwenden, um Berichtsdatenquellen zu verwalten.  
  
 Im Zuge der Verwaltung von Datenquellenverbindungen führen Sie die folgenden in diesem Thema beschriebenen Tasks aus:  
  
-   Ändern von Verbindungszeichenfolgen  
  
-   Ändern von Anmeldeinformationen  
  
-   Erstellen und Verwenden von freigegebenen Datenquellen auf einem Berichtsserver, einschließlich des Wechselns einer eingebetteten Datenquelle in eine freigegebene Datenquelle  
  
-   Steuern des Zugriffs auf Datenquelleneigenschaften durch Festlegen von Berechtigungen für Bericht, Modell oder verwendete freigegebene Datenquellen  
  
 Beachten Sie, dass das Ändern von Abfragen nicht zu den Verwaltungsaufgaben für Datenquellverbindungen gehört. Um eine Abfrage für einen Bericht oder ein Modell zu ändern, müssen Sie Ihre Änderungen in der Berichts- oder Modelldefinition mit einem Berichterstellungstool durchführen.  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>Verwaltete Eigenschaften: Datenquelltyp, Verbindungszeichenfolge und Anmeldeinformationen  
 Datenquelleneigenschaften, die Sie auf einem Berichtsserver verwalten können:  
  
|Eigenschaft|Description|Verwaltung|  
|--------------|-----------------|----------------------|  
|Datenquellentyp|Legt fest, welche Datenverarbeitungserweiterung auf dem Berichtsserver für die externen Daten verwendet werden soll. Beispiele für Datenprozessoren: SQL Server, Analysis Services und Oracle.|Der Datenquellentyp ist eine verwaltete Eigenschaft, da er konfigurierbar ist. Sie sollten einen Datenquellentyp jedoch nur konfigurieren, wenn Sie eine neue freigegebene Datenquelle erstellen.<br /><br /> Ändern Sie den Datenquelltyp nicht auf den Eigenschaftenseiten eines veröffentlichten Berichts oder Modells. Andernfalls wird die Verbindung mit Sicherheit ungültig. Es ist sehr unwahrscheinlich, dass die von einem Bericht oder Modell benötigten Datenstrukturen auf einer anderen Datenplattform identisch sind.|  
|Verbindungszeichenfolge|Richtet die Anfangsverbindung zu einer externen Datenquelle ein. Ein Bericht kann statische oder dynamische Verbindungszeichenfolgen verwenden.<br /><br /> Eine *statische Verbindungszeichenfolge* ist ein Wertesatz, der verwendet wird, um bei jeder Berichtsausführung eine Verbindung zur selben Datenquelle herzustellen.<br /><br /> Eine *dynamische Verbindungszeichenfolge* ist ein Ausdruck, den Sie in den Bericht aufnehmen. Benutzer können mit diesem Ausdruck auswählen, welche Datenquelle zur Laufzeit verwendet werden soll. Sie müssen den Ausdruck und die Datenquellenauswahlliste beim Erstellen des Berichts im Berichts-Generator in den Bericht integrieren.|Es ist sinnvoll, eine Verbindungszeichenfolge zu ändern, wenn Sie eine Datenquelle auf einen anderen Computer verschieben, oder wenn Sie Berichte, die Sie mit Testdaten erstellt haben, in einer Produktionsdatenbank bereitstellen möchten.<br /><br /> Sie können eine statische Verbindungszeichenfolge verwalten, indem Sie die ursprüngliche Zeichenfolge durch eine andere Zeichenfolge ersetzen.<br /><br /> Die Verwaltung einer dynamischen Verbindungszeichenfolge im Berichts-Manager oder auf einer SharePoint-Site ist auf das Ersetzen durch eine statische Verbindungszeichenfolge beschränkt. Sie können den Ausdruck selbst nicht bearbeiten und auch nicht die Auswahlliste der Datenquellen ändern. Um den Ausdruck oder die gültige Werteliste zu ändern, müssen Sie die Berichtsdefinition bearbeiten und auf dem Berichtsserver neu veröffentlichen. Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).|  
|Anmeldeinformationen|Stellt den Namen und das Kennwort eines Benutzers bereit, der berechtigt ist, Daten aus der Datenquelle zu lesen.<br /><br /> Wenn eine Datenquelle die Authentifizierung nicht unterstützt (beispielsweise ist die Datenquelle eine XML-Datei im Dateisystem), können Sie das Konto für die unbeaufsichtigte Ausführung so konfigurieren, dass sich der Berichtsserver an der externen Datenquelle anmelden kann, ohne Anmeldeinformationen zu übergeben.|Im Zuge der Verwaltung von Anmeldeinformationen können Sie abgelaufene Benutzerkonten oder Kennwörter aktualisieren.<br /><br /> Sie können darüber hinaus den Abruf von Anmeldeinformationen ändern (z. B. Benutzer auffordern, zur Laufzeit Anmeldeinformationen einzugeben).<br /><br /> Wenn Sie möchten, dass Benutzer einen Bericht abonnieren können, müssen Sie den Bericht für die Verwendung von gespeicherten Anmeldeinformationen konfigurieren.|  
  
## <a name="creating-and-using-shared-data-sources"></a>Erstellen und Verwenden freigegebener Datenquellen  
 Wenn Sie einen Bericht veröffentlichen, in den Datenquelleneigenschaften eingebettet sind, können Sie zu freigegebenen Datenquelleneigenschaften wechseln. Freigegebene Datenquellen lassen sich einfacher verwalten, da Sie Anmeldeinformationen und Verbindungszeichenfolgen auf einer Seite aktualisieren können. Alle Berichte, Modelle und datengesteuerten Abonnements, die auf die Datenquelle zugreifen, übernehmen die Änderungen sofort. Sie können freigegebene Datenquellen auch offline stellen. Auf diese Weise können Sie den Bericht oder das Abonnement effektiv unterbrechen, wenn Sie aufgetretene Probleme prüfen oder behandeln müssen.  
  
## <a name="controlling-access-data-source-properties"></a>Steuern des Zugriffs auf Datenquelleneigenschaften  
 Standardmäßig können alle Benutzer, die berechtigt sind Berichte zu verwalten, Eigenschaften für den Bericht festlegen. Dazu gehören Eigenschaften, die den Datenquelltyp, die Verbindungszeichenfolge, Anmeldeinformationen und die Datenquelle für Verbindungsinformationen (eingebettete oder freigegebene Datenquelle) definieren. Weitere Informationen darüber, welche Tasks und Berechtigungen den Zugriff auf Datenquelleigenschaften auf einem im einheitlichen Modus ausgeführten Berichtsserver steuern, finden Sie unter [Sichern freigegebener Datenquellenelemente](../../reporting-services/security/secure-shared-data-source-items.md) und [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md).  
  
 Berechtigungen zum Anzeigen und Bearbeiten von Eigenschaften für Elemente in einer SharePoint-Bibliothek werden vom Websiteadministrator zugeteilt. Weitere Informationen darüber, welche Berechtigungen den Zugriff auf Datenquellen-Verbindungseigenschaften steuern, finden Sie unter [Referenz zu SharePoint-Website- und Listenberechtigungen für Berichtsserverelemente](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>Arbeiten mit Datenquelleneigenschaften auf Berichtsservern  
 Sie können eine Vielzahl von Tools verwenden, um Datenquelleneigenschaften zu erstellen und zu ändern. In der folgenden Tabelle sind die verschiedenen Methoden und Tools zusammengefasst. Ein Link führt zu weiteren Anweisungen.  
  
|Task|Tool|Link|  
|----------|----------|----------|  
|Anzeigen von Beispielen für Verbindungszeichenfolgen||[Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|Wählen Sie eine Methode zum Abrufen von Anmeldeinformationen, um eine Verbindung mit einer Datenquelle herzustellen.||[Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)|  
|Hinzufügen von Eigenschaften für die Datenquellenverbindung zu einer Berichtsdefinitionsdatei (.rdl)|Berichts-Designer|[Erstellen einer eingebetteten oder freigegebenen Datenquelle &#40;SSRS&#41;](http://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b)|  
|Hinzufügen und Verknüpfen mit einer freigegebenen Datenquellendatei (.rds) im Berichtsprojekt|Berichts-Designer|[Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)|  
|Erstellen einer vordefinierten Liste von Datenquellen, die Benutzer zur Laufzeit auswählen können. Wenn Benutzer Berichte anfordern, stellt der Bericht eine Liste von Datenquellen bereit. Benutzer müssen auswählen, welche Datenquelle vor dem Ausführen des Berichts verwendet werden soll. Um einem Bericht eine Liste der auszuwählenden Datenquellen hinzuzufügen, verwenden Sie einen Ausdruck.<br /><br /> Dies wird als dynamische Datenquellenverbindung bezeichnet.|Berichts-Designer|[Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|Erstellen eines freigegebenen Datenquellenelements auf einem Berichtsserver|Berichts-Manager|[Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)|  
|Speichern von Anmeldeinformationen als Voraussetzung für das Erstellen von Abonnements oder Berichtsmomentaufnahmen|Berichts-Manager|[Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)|  
|Bearbeiten von Eigenschaften für die Datenquellenverbindung in einem veröffentlichten Bericht|Berichts-Manager|[Konfigurieren von Datenquelleneigenschaften für einen Bericht &#40;Berichts-Manager&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)|  
|Erstellen eines freigegebenen Datenquellenelements auf einem Berichtsserver|SharePoint-Site|[Erstellen und Verwalten von freigegebenen Datenquellen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)|  
|Verwenden vorhandener ODC-Verbindungsinformationen mit einem Bericht|SharePoint-Site|[Verwenden einer Office Data Connection &#40;.odc&#41; für Berichte &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  Das Verwalten von Datenquellenverbindungen mit Berichtsdatenquellen ist nicht identisch mit dem Verwalten der Berichtsserververbindung mit der Berichtsserver-Datenbank. Weitere Informationen zur Verbindung eines Berichtsservers mit seinem internen Datenspeicher finden Sie unter [Konfigurieren einer Berichtsserver-Datenbankverbindung &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Binden eines Berichts oder Modells an eine freigegebene Datenquelle &#40;SSRS&#41;](../../reporting-services/report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   
 [Verwalten von Berichtsserverinhalten &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
