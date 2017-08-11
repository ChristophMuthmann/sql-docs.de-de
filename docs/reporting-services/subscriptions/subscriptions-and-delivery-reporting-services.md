---
title: Abonnement und Lieferung (Reporting Services) | Microsoft-Dokumentation
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
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
caps.latest.revision: 56
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5ecd364a199f122c98471f112e153d98d2778852
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="subscriptions-and-delivery-reporting-services"></a>Subscriptions and Delivery (Reporting Services)
  Ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnement ist eine Konfiguration zur Übermittlung eines Berichts zu einem bestimmten Zeitpunkt oder als Reaktion auf ein Ereignis, in einem von Ihnen angegebenen Dateiformat. Speichern Sie beispielsweise jeden Donnerstag den Bericht MonthlySales.rdl als Microsoft Word-Dokument in eine Dateifreigabe. Sie können Abonnements verwenden, um die Übermittlung eines Berichts mit einem spezifischen Satz an Berichtsparameterwerten zeitlich festzulegen und zu automatisieren.  
  
 Pro Bericht können mehrere Abonnements erstellt werden, um die Abonnementoptionen zu variieren. Beispielsweise können Sie unterschiedliche Parameterwerte angeben, um drei Versionen eines Berichts zu erstellen, wie etwa einen Umsatzbericht West, einen Umsatzbericht Ost und einen Umsatzbericht für alle Verkäufe.  
  
 ![Beispiel: SSRS-Abonnementablauf](../../reporting-services/subscriptions/media/ssrs-subscription-example-flow.png "example ssrs subscription flow")  
  
 Abonnements sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 **In diesem Thema:**  
  
-   [Abonnement- und Übermittlungsszenarien](#bkmk_subscription_scenarios)  
  
-   [Standardabonnements und datengesteuerte Abonnements](#bkmk_standard_and_datadriven)  
  
-   [Abonnementanforderungen](#bkmk_subscription_requirements)  
  
-   [Übermittlungserweiterungen](#bkmk_delivery_extensions)  
  
-   [Bestandteile eines Abonnements](#bkmk_parts_of_subscription)  
  
-   [So werden Abonnements verarbeitet](#bkmk_subscription_processing)  
  
-   [Programmgesteuerte Kontrolle von Abonnements](#bkmk_code)  
  
 **Themen in diesem Abschnitt:**  
  
-   [E-Mail-Übermittlung in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md) Erläutert den E-Mail-Zustellungsvorgang des Berichtsservers und die Konfiguration.  
  
-   [Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) Ausführliche Schritte zum Erstellen von Abonnements mit einem Berichtsserver im einheitlichen Modus.  
  
-   [Erstellen und Verwalten von Abonnements für Berichtsserver im SharePoint-Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) Ausführliche Schritte zum Erstellen von Abonnements mit einem Berichtsserver im SharePoint-Modus.  
  
-   [Dateifreigabeübermittlung in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md) Erläutert den Zustellungsvorgang bei Verwenden von Dateifreigabe des Berichtsservers und die Konfiguration.  
  
-   [Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).  
  
-   [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md) Erläutert die Bereitstellung eines Abonnements in einer SharePoint-Bibliothek.  
  
-   [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md) Bietet Informationen zur Verwendung datengesteuerter Abonnements zum Anpassen der Berichtsausgabe zur Laufzeit.  
  
-   [Überwachen von Reporting Services-Abonnements](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
-   [Verwenden von PowerShell, um Reporting Services-Abonnenten zu ändern und aufzulisten sowie ein Abonnement auszuführen](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> Abonnement- und Übermittlungsszenarien  
 Für jedes Abonnement konfigurieren Sie Übermittlungsoptionen, und die verfügbaren Optionen werden entsprechend der von Ihnen gewählten Übermittlungserweiterung bestimmt. Eine Übermittlungserweiterung ist ein Modul, das einige Verteilungsarten unterstützt. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält mehrere Bereitsellungserweiterungen und Bereitstellungserweiterungen, die möglicherweise bei Drittanbietern erhältlich sind.  
  
 Wenn Sie Entwickler sind, können Sie benutzerdefinierte Übermittlungserweiterungen erstellen, um zusätzliche Szenarien zu unterstützen. Weitere Informationen finden Sie unter [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
 In der folgenden Tabelle werden häufige Abonnementszenarien für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] beschrieben.  
  
|Szenario|Description|  
|--------------|-----------------|  
|Senden von Berichten als E-Mail|Senden Sie Berichte als E-Mail an einzelne Benutzer und Gruppen. Erstellen Sie ein Abonnement, und geben Sie einen Gruppenalias oder einen E-Mail-Alias für den Empfang eines von Ihnen verteilten Berichts an. Sie können die Abonnementdaten von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zur Laufzeit bestimmen lassen. Wenn Sie den gleichen Bericht an eine Gruppe senden möchten, deren Mitgliederliste sich häufig ändert, können Sie die Abonnementliste mithilfe einer Abfrage zur Laufzeit abrufen.|  
|Anzeigen von Berichten im Offlinemodus|Benutzer können eines der folgenden Formate für die Abonnementausgabe wählen:<br /><br /> XML-Datei mit Berichtsdaten<br />CSV (durch Trennzeichen getrennt)<br />PDF<br />MHTML (Webarchiv)<br />Microsoft Excel<br />TIFF-Datei<br />Microsoft Word<br /><br /> Berichte, die Sie archivieren möchten, können direkt an einen freigegebenen Ordner gesendet werden, den Sie beispielsweise nachts sichern lassen. Umfangreiche Berichte, die zu lange Ladezeiten im Browser verursachen würden, können in einem Format an einen freigegebenen Ordner gesendet werden, das in einer Desktopanwendung angezeigt werden kann.|  
|Vorabladen des Caches|Wenn Sie über mehrere Instanzen eines parametrisierten Berichts verfügen oder ein Bericht von zahlreichen Berichtsbenutzern angezeigt werden soll, können Sie Berichte vorab in den Cache laden, um die erforderliche Verarbeitungszeit für die Anzeige des Berichts zu reduzieren.|  
|Datengesteuerte Berichte|Verwenden Sie datengesteuerte Abonnements, um die Berichtsausgabe, Übermittlungsoptionen und Berichtsparametereinstellungen zur Laufzeit anzupassen. Zur Laufzeit werden die Eingabewerte vom Abonnement mithilfe einer Abfrage aus einer Datenquelle abgerufen. Mithilfe datengesteuerter Abonnements können Sie einen E-Mail-Serienvorgang ausführen, durch den ein Bericht an eine Liste von Abonnenten gesendet wird, die erst während der Verarbeitung des Abonnements ermittelt wird.|  
  
##  <a name="bkmk_standard_and_datadriven"></a> Standardabonnements und datengesteuerte Abonnements  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt zwei Arten von Abonnements: **Standardabonnements** und **datengesteuerte Abonnements**. Standardabonnements werden von einzelnen Benutzern erstellt und verwaltet. Ein Standardabonnement enthält statische Werte, die während der Abonnementverarbeitung nicht variiert werden können. Für jedes Standardabonnement ist exakt eine Gruppe von Berichtspräsentationsoptionen, Übermittlungsoptionen und Berichtsparametern vorhanden.  
  
 Datengesteuerte Abonnements rufen zur Laufzeit Abonnementinformationen ab, indem sie eine externe Datenquelle abfragen, die Werte für einen Empfänger, Berichtsparameter oder ein Anwendungsformat liefert. Sie können datengesteuerte Abonnements verwenden, wenn Sie eine sehr große Empfängerliste haben oder unterschiedliche Berichtsausgaben für unterschiedliche Empfänger verwenden möchten. Wenn Sie datengesteuerte Abonnements verwenden möchten, müssen Sie über Fachkenntnisse im Erstellen von Abfragen und zur Verwendungsweise von Parametern verfügen. In der Regel werden diese Abonnements von Berichtsserveradministratoren erstellt und verwaltet. Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
  
-   [Erstellen eines datengesteuerten Abonnements &#40;SSRS-Tutorial&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> Abonnementanforderungen  
 Vor dem Erstellen eines Abonnements für einen Bericht müssen die folgenden Voraussetzungen erfüllt sein:  
  
|Anforderung|Description|  
|-----------------|-----------------|  
|Berechtigungen|Sie benötigen Zugriff auf den Bericht. Zum Abonnieren eines Berichts benötigen Sie die Berechtigung zum Anzeigen des Berichts.<br /><br /> Für Berichtsserver im einheitlichen Modus wirken sich die folgenden Rollenzuweisungen auf Abonnements aus:<br /><br /> Mit dem Task „Einzelne Abonnements verwalten“ können Benutzer für einen bestimmten Bericht Abonnements erstellen, ändern und löschen. In den vordefinierten Rollen ist dieser Task Teil der Browser- und Berichts-Generator-Rollen. Mit Rollenzuweisungen, die diesen Task enthalten, können Benutzer nur die Abonnements verwalten, die sie oder er erstellt hat.<br />Mit dem Task „Alle Abonnements verwalten“ kann der Benutzer auf alle Abonnements zugreifen und diese ändern. Dieser Task ist für das Erstellen eines datengesteuerten Abonnements erforderlich. In vordefinierten Rollen enthält nur die Inhalts-Manager-Rolle diesen Task.|  
|Gespeicherte Anmeldeinformationen|Der Bericht muss gespeicherte oder keine Anmeldeinformationen zum Abrufen des Inhalts zur Laufzeit verwenden, um ein Abonnement zu erstellen. Sie können keinen Bericht abonnieren, für den die Verwendung der anonymisierten oder delegierten Anmeldeinformationen des aktuellen Benutzers zum Herstellen einer Verbindung mit einer externen Datenquelle konfiguriert ist. Bei den gespeicherten Anmeldeinformationen kann es sich um ein Windows-Konto oder ein Datenbank-Benutzerkonto handeln. Weitere Informationen finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).<br /><br /> Außerdem müssen Sie über die Berechtigung verfügen, den Bericht anzuzeigen und einzelne Abonnements zu erstellen. **Geplante Ereignisse und Berichtsübermittlung** muss auf dem Berichtsserver aktiviert sein. Weitere Informationen finden Sie unter [Alt_Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b).|  
|Benutzerabhängige Werte in einem Bericht|Nur bei Standardabonnements können Sie Abonnements für Berichte erstellen, bei denen Benutzerkontoinformationen in einen Filter integriert sind oder als Text im Bericht angezeigt werden. Im Bericht wird der Name des Benutzerkontos über den **User!UserID** -Ausdruck angegeben, der in den aktuellen Benutzer aufgelöst wird. Beim Erstellen eines Abonnements wird der Benutzer, der das Abonnement erstellt, als aktueller Benutzer betrachtet.|  
|Keine Modellelementsicherheit|Sie können keine mit dem Berichts-Generator erstellten Berichte abonnieren, die ein Modell als Datenquelle verwenden, wenn das Modell Sicherheitseinstellungen für Modellelemente enthält. Diese Einschränkung bezieht sich nur auf Berichte, die Sicherheitseinstellungen für Modellelemente verwenden.|  
|Parameterwerte|Falls der Bericht Parameter verwendet, muss ein Parameterwert im Bericht selbst oder im Abonnement, das Sie definieren, angegeben werden. Falls im Bericht Standardwerte definiert wurden, können Sie den Standardwert für den Parameterwert festlegen.|  
  
##  <a name="bkmk_delivery_extensions"></a> Übermittlungserweiterungen  
 Abonnements werden auf dem Berichtsserver verarbeitet und über Übermittlungserweiterungen verteilt, die auf dem Server bereitgestellt werden. Standardmäßig können Sie Abonnements erstellen, die Berichte an einen freigegebenen Ordner oder an eine E-Mailadresse senden. Ist der Berichtsserver für den integrierten SharePoint-Modus konfiguriert, können Sie auch einen Bericht an eine SharePoint-Bibliothek senden.  
  
 Beim Erstellen eines Abonnements kann der Benutzer eine der verfügbaren Übermittlungserweiterungen auswählen, um die Art der Übermittlung zu bestimmen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] beinhaltet die folgenden Übermittlungserweiterungen:  
  
|Übermittlungserweiterung|Description|  
|------------------------|-----------------|  
|Windows-Dateifreigabe|Übermittelt einen Bericht als statische Anwendungsdatei an einen freigegebenen Ordner, der über das Netzwerk zugänglich ist.|  
|E-Mail|Übermittelt eine Benachrichtigung oder einen Bericht als E-Mail-Anlage oder URL-Link.|  
|SharePoint-Bibliothek|Übermittelt einen Bericht als statische Anwendungsdatei an eine SharePoint-Bibliothek, die über eine SharePoint-Website zugänglich ist. Die Website muss in einen Berichtsserver integriert werden, der im integrierten SharePoint-Modus ausgeführt wird.|  
|NULL|Der NULL-Übermittlungsanbieter ist eine in hohem Maße spezialisierte Übermittlungserweiterung, die zum Vorabladen eines Caches mit anzeigebereiten parametrisierten Berichten verwendet wird. Dieses Verfahren steht Benutzern bei individuellen Abonnements nicht zur Verfügung. Die NULL-Übermittlung wird von Administratoren in datengesteuerten Abonnements zur Verbesserung der Berichtsserverleistung verwendet, indem vorab Daten in den Cache geladen werden.|  
  
> [!NOTE]  
>  Die Berichtsübermittlung stellt einen erweiterbaren Bestandteil der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Architektur dar. Drittanbieter können benutzerdefinierte Übermittlungserweiterungen erstellen, um Berichte an andere Speicherorte oder Geräte weiterzuleiten. Weitere Informationen zu benutzerdefinierten Übermittlungserweiterungen finden Sie unter [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
##  <a name="bkmk_parts_of_subscription"></a> Bestandteile eines Abonnements  
 Eine Abonnementdefinition besteht aus den folgenden Bestandteilen:  
  
-   Ein Zeiger auf einen Bericht, der unbeaufsichtigt ausgeführt werden kann (d. h. ein Bericht, der gespeicherte oder keine Anmeldeinformationen verwendet).  
  
-   Eine Übermittlungsmethode (z. B. E-Mail) und Einstellungen für den Übermittlungsmodus (z. B. eine E-Mail-Adresse).  
  
-   Eine Renderingerweiterung zum Darstellen des Berichts in einem bestimmten Format.  
  
-   Bedingungen für die Verarbeitung des Abonnements in Form von Ereignissen.  
  
     In der Regel sind die Bedingungen zum Ausführen eines Berichts zeitbasiert. Sie möchten beispielsweise jeden Dienstag um 15.00 Uhr einen bestimmten Bericht ausführen. UTC. Falls der Bericht jedoch für die Ausführung als Momentaufnahme konfiguriert ist, können Sie angeben, dass das Abonnement bei jeder Aktualisierung der Momentaufnahme ausgeführt wird.  
  
-   Parameter zum Ausführen des Berichts.  
  
     Parameter sind optional und werden nur für Berichte angegeben, die Parameterwerte akzeptieren. Da sich ein Abonnement in der Regel im Besitz eines Benutzers befindet, variieren die angegebenen Parameterwerte von Abonnement zu Abonnement. Beispielsweise verwenden Vertriebs-Manager für verschiedene Abteilungen Parameter, die Daten für ihre jeweilige Abteilung zurückgeben. Für alle Parameter muss explizit ein Wert definiert werden oder ein gültiger Standardwert vorhanden sein.  
  
 Abonnementinformationen werden zusammen mit dem jeweiligen Bericht in einer Berichtsserver-Datenbank gespeichert. Abonnements können nicht getrennt vom zugehörigen Bericht verwaltet werden. Beachten Sie, dass Abonnements nicht um Beschreibungen, sonstigen benutzerdefinierten Text oder andere Elemente erweitert werden können. Abonnements dürfen nur die weiter oben aufgeführten Elemente enthalten.  
  
##  <a name="bkmk_subscription_processing"></a> So werden Abonnements verarbeitet  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält einen Plan- und Bereitstellungsprozessor, der Funktionen zum Planen von Berichten und Bereitstellen der Berichte für die Benutzer umfasst. Der Berichtsserver antwortet auf Ereignisse, die er ständig überwacht. Beim Auftreten eines Ereignisses, das den für ein Abonnement definierten Bedingungen entspricht, liest der Berichtsserver das Abonnement, um zu ermitteln, wie der Bericht verarbeitet und übermittelt werden soll. Der Berichtsserver fordert die Übermittlungserweiterung an, die im Abonnement angegeben ist. Wenn die Übermittlungserweiterung ausgeführt wird, extrahiert der Berichtsserver Übermittlungsinformationen aus dem Abonnement und übergibt sie zur Verarbeitung an die Übermittlungserweiterung.  
  
 Die Übermittlungserweiterung rendert den Bericht in dem im Abonnement definierten Format und übermittelt dann den Bericht oder die Benachrichtigung an den angegebenen Empfänger. Falls ein Bericht nicht zustellbar ist, erfolgt ein entsprechender Eintrag in der Berichtsserver-Protokolldatei. Zum Unterstützen von Wiederholungsvorgängen können Sie den Berichtsserver so konfigurieren, dass die Übermittlung erneut versucht wird, falls der erste Versuch fehlschlägt.  
  
### <a name="processing-a-standard-subscription"></a>Verarbeiten eines Standardabonnements  
 Standardabonnements erstellen eine Berichtsinstanz. Der Bericht wird an einen einzigen freigegebenen Ordner oder an die im Abonnement angegebenen E-Mail-Adressen übermittelt. Das Berichtslayout und die Berichtsdaten variieren nicht. Falls der Bericht Parameter verwendet, wird ein Standardabonnement mit einem einzigen Wert pro Berichtsparameter verarbeitet.  
  
### <a name="processing-a-data-driven-subscription"></a>Verarbeiten eines datengesteuerten Abonnements  
 Datengesteuerte Abonnements können zahlreiche Berichtsinstanzen erstellen, die an mehrere Ziele übermittelt werden. Das Berichtslayout variiert nicht, aber die Berichtsdaten können variieren, falls Parameterwerte von einem Abonnentenresultset übergeben werden. Die Übermittlungsoptionen, die beeinflussen, wie ein Bericht gerendert wird und ob der Bericht an die E-Mail-Nachricht angehängt oder damit verknüpft wird, können ebenfalls von Abonnent zu Abonnent variieren, wenn die Werte vom Rowset übergeben werden.  
  
 Datengesteuerte Abonnements können eine große Anzahl von Übermittlungen erstellen. Der Berichtsserver erstellt eine Übermittlung für jede Zeile im Rowset, die von der Abonnementabfrage zurückgegeben wird.  
  
### <a name="report-delivery-characteristics"></a>Merkmale der Berichtsübermittlung  
 Berichte, die über Standardabonnements übermittelt werden, werden in der Regel als statische Berichte gerendert. Diese Berichte basieren entweder auf der neuesten Momentaufnahme zur Berichtsausführung oder werden als statischer Bericht für das Abschließen einer Übermittlung generiert. Wenn Sie die Option **Link einschließen** in einem Abonnement für einen Bericht auswählen, der bei Bedarf ausgeführt wird, führt der Berichtsserver den Bericht beim Klicken auf den Link aus.  
  
> [!NOTE]  
>  Berichte, die über eine URL übermittelt werden, bleiben mit dem Berichtsserver verbunden und können zwischen Anzeigevorgängen aktualisiert oder gelöscht werden. Durch die für Ihr Abonnement ausgewählten Übermittlungsoptionen wird festgelegt, ob der Bericht als URL übermittelt, in den Textkörper einer E-Mail-Nachricht eingebettet oder als Anlage gesendet wird.  
  
 Berichte, die über ein datengesteuertes Abonnement übermittelt werden, können möglicherweise während der Verarbeitung des Abonnements erneut generiert werden. Der Berichtsserver führt keine Sperrung einer bestimmten Instanz des Berichts oder seines Datasets durch, um ein datengesteuertes Abonnement zu verarbeiten. Falls im Abonnement für verschiedene Abonnenten unterschiedliche Parameterwerte verwendet werden, generiert der Berichtsserver den Bericht erneut, um das erforderliche Ergebnis zu erstellen. Falls die zugrunde liegenden Daten nach dem Erstellen und Übermitteln der ersten Berichtskopie aktualisiert werden, sehen Benutzer, die erst später Berichte erhalten, möglicherweise Daten, die auf unterschiedlichen Resultsets basieren. Mithilfe eines Berichts, der als Momentaufnahme ausgeführt wird, können Sie sicherstellen, dass alle Abonnenten dieselbe Berichtsinstanz empfangen. Wenn jedoch ein geplantes Update der Momentaufnahme während der Verarbeitung des Abonnements ausgeführt wird, erhalten Benutzer möglicherweise dennoch unterschiedliche Daten in ihren Berichten.  
  
### <a name="triggering-subscription-processing"></a>Auslösen der Abonnementverarbeitung  
 Der Berichtsserver verwendet zwei Arten von Ereignissen, um die Abonnementverarbeitung auszulösen: zeitgesteuerte Ereignisse, die in einem Zeitplan angegeben werden, und Momentaufnahme-Updateeignisse.  
  
 Zeitgesteuerte Trigger verwenden berichtsspezifische Zeitpläne oder einen freigegebenen Zeitplan, um den Zeitpunkt der Ausführung eines Abonnements anzugeben. Bei bedarfsgesteuerten und zwischengespeicherten Berichten sind Zeitpläne die einzige Triggeroption.  
  
 Bei Momentaufnahme-Updateereignissen wird das geplante Update einer Berichtsmomentaufnahme verwendet, um ein Abonnement auszulösen. Sie können ein Abonnement definieren, das ausgelöst wird, wenn ein Bericht mit neuen Daten aktualisiert wird. Grundlage hierfür sind die Berichtsausführungseigenschaften, die für den Bericht festgelegt wurden.  
  
##  <a name="bkmk_code"></a> Programmgesteuerte Kontrolle von Abonnements  
 Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Objektmodell ermöglicht Ihnen, Abonnements und Abonnementverarbeitung programmgesteuert zu überwachen und zu steuern.  Im Folgenden finden Sie Beispiele und erste Schritte:  
  
-   [Verwenden von PowerShell, um Reporting Services-Abonnenten zu ändern und aufzulisten sowie ein Abonnement auszuführen](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   Beispiele zum Verwenden von PowerShell zum Aktivieren und Deaktivieren von Abonnements finden Sie unter [Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
-   Ein Beispiel-PowerShell-Skript zum Auflisten aller [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Abonnements, die für die Verwendung des **Dateifreigabekontos** konfiguriert sind, finden Sie unter [Abonnementeinstellungen und ein Dateifreigabekonto &#40;Konfigurations-Manager&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines datengesteuerten Abonnements &#40;SSRS-Tutorial&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Zeitpläne](../../reporting-services/subscriptions/schedules.md)   
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Überwachen von Reporting Services-Abonnements](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
  

