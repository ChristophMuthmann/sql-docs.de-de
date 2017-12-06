---
title: "SharePoint-Bibliotheksübermittlung in Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
caps.latest.revision: "15"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 00e9a1ecf0d4af2348d6c23dc2810140d714e5e3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>SharePoint-Bibliotheksübermittlung in Reporting Services
  Falls der Berichtsserver für die SharePoint-Integration konfiguriert ist, enthält er eine Übermittlungserweiterung, mit der Sie einen Bericht an eine SharePoint-Bibliothek senden können.  
  
 Zum Verwenden der SharePoint-Übermittlungserweiterung müssen Sie ein Abonnement von einer Anwendungsseite auf einer SharePoint-Website aus erstellen und dann **SharePoint-Dokumentbibliothek** als Übermittlungstyp auswählen. Die SharePoint-Übermittlungserweiterung kann nicht für Abonnements verwendet werden, die Sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder im Berichts-Manager erstellen.  
  
> [!NOTE]  
>  Die Übermittlung von Berichten an eine SharePoint-Website wird von der Übermittlungserweiterung nicht unterstützt, wenn der Berichtsserver im einheitlichen Modus ausgeführt wird. Wenn Sie versuchen, die Übermittlungserweiterung für einen Berichtsserver im einheitlichen Modus programmgesteuert aufzurufen, wird vom Server der **rsDeliveryExtensionNotFound** -Fehler zurückgegeben und der **rsOperationNotSupportedSharePointMode** -Fehler in den Berichtsserver-Protokolldateien protokolliert.  
  
## <a name="requirements"></a>Anforderungen  
 Zum Übermitteln gerenderter Berichte an eine Bibliothek müssen folgende Anforderungen erfüllt werden:  
  
-   Der Berichtsserver muss für die SharePoint-Integration konfiguriert sein.  
  
-   Die SharePoint-Übermittlungserweiterung muss auf dem Berichtsserver installiert und konfiguriert sein.  
  
-   Bei dem Bericht muss es sich um eine Berichtsdefinitionsdatei (RDL) handeln. Sie können andere Berichtsserver-Inhaltstypen, beispielsweise Modelle oder Ressourcen, nicht über ein Abonnement übermitteln. Sie können keine Ad-hoc-Berichte abonnieren, in denen Modelle als eine Datenquelle verwendet werden.  
  
-   Für den Bericht müssen gespeicherte Anmeldeinformationen verwendet werden. Dies ist eine Voraussetzung zum Erstellen von Abonnements für einen Bericht, unabhängig vom Übermittlungstyp.  
  
-   Das Ziel muss eine SharePoint-Bibliothek sein. Beim Auswählen einer Zielbibliothek müssen Sie eine Bibliothek auswählen, die sich auf derselben SharePoint-Website befindet. Sie können einen Bericht nicht an eine Bibliothek auf einem anderen Server oder einer anderen Website innerhalb derselben Websitesammlung übermitteln.  
  
 Eigenschaften und Metadaten sind nicht Bestandteil der Berichtsübermittlung. Wenn der Bericht zum ersten Mal übermittelt wird, erbt er die Sicherheitseinstellungen des Ordners bzw. der Liste, in dem bzw. in der er enthalten ist. Wenn Sie anschließend die Sicherheitseinstellungen ändern oder die Berichtseigenschaften festlegen, werden diese Einstellungen beibehalten. Durch das Abonnement wird der am angegebenen Speicherort gespeicherte Bericht lediglich aktualisiert.  
  
## <a name="sharepoint-permissions"></a>SharePoint-Berechtigungen  
 Zum Erstellen des Abonnements müssen Sie für den Bericht über die Berechtigung zum Anzeigen von Elementen verfügen. Zum Übermitteln eines Berichts müssen Sie für die Bibliothek, an die der Bericht übermittelt wird, über die Berechtigung zum Hinzufügen von Elementen verfügen.  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>Erstellen, Ändern und Löschen von Abonnements  
  
1.  Wechseln Sie zu der SharePoint-Website, von der aus Sie auf den Bericht zugreifen.  
  
2.  Wählen Sie den Bericht aus, klicken Sie neben dem Bericht auf den Pfeil nach unten, und wählen Sie **Abonnements verwalten**aus.  
  
3.  Klicken Sie auf **Erstellen**, **Bearbeiten**oder **Löschen**.  
  
 In der Liste Abonnements verwalten werden die aktuellen Informationen zum Abonnement angezeigt, einschließlich der Informationen über dessen Erfolg sowie über das Datum und den Zeitpunkt der letzten Ausführung des Abonnements.  
  
## <a name="setting-delivery-options"></a>Festlegen von Übermittlungsoptionen  
 Sie können die im Folgenden aufgeführten Übermittlungsoptionen für ein Abonnement festlegen, das einen Bericht an eine SharePoint-Bibliothek übermittelt.  
  
 Ausgabeformat rendern  
 Geben Sie das Anwendungsformat an, in dem der Bericht übermittelt werden soll. Der Bericht wird vor der Übermittlung in diesem Format gerendert. Durch das von Ihnen ausgewählte Ausgabeformat wird die Standarddateierweiterung bestimmt.  
  
 Die Liste der Ausgabeformate, aus der Sie auswählen können, entspricht einer Gruppe von Renderingerweiterungen, die auf dem Berichtsserver installiert sind.  
  
 Beachten Sie, dass Sie keine Ausgabeformate angeben können, die ausschließlich für die interne Verwendung bestimmt sind oder die nicht für Berichtsserver unterstützt werden, die im integrierten SharePoint-Modus ausgeführt werden. Zu diesen Formaten zählen NULL, RGDI und HTMLOWC.  
  
 Dateiname und Dateierweiterung  
 Geben Sie den Dateinamen und die Dateierweiterung des Berichts so an, wie sie in der Zielbibliothek angezeigt werden sollen. Wenn Sie keine Dateierweiterung angeben, wird vom Berichtsserver eine Dateierweiterung basierend auf dem Ausgabeformat des Berichts erstellt. Dieser Wert ist erforderlich. Verwenden Sie keines der folgenden Zeichen: : \ / * ? " < > | # { } %  
  
 Titel  
 Gibt eine optionale **Title** -Eigenschaft für den Bericht in der Zielbibliothek an. Dies ist eine Standardeigenschaft für alle in einer Bibliothek gespeicherten Elemente. Benutzer können angeben, ob diese Eigenschaft beim Anzeigen des Inhalts der Bibliothek auf einer SharePoint-Website angezeigt oder ausgeblendet werden soll.  
  
 Pfad  
 Gibt eine vollqualifizierte URL zur SharePoint-Bibliothek an, einschließlich der SharePoint-Webanwendung und -Website. Beispielsweise `http://mySharePointWeb/MySite/MyDocLib`, wobei `http://mySharePointWeb` die Webanwendung angibt, „MySite“ die SharePoint-Website ist und „MyDocLib“ der SharePoint-Bibliothek entspricht, an die der Bericht übermittelt wird.  
  
 Sie können keine Seite, Website oder Liste angeben. Der Zielcontainer muss eine Bibliothek auf derselben Website oder Webfarm sein.  
  
 Optionen für das Überschreiben  
 Gibt an, ob eine Datei mit demselben Namen und derselben Erweiterung beim Verarbeiten des Abonnements durch eine neuere Version ersetzt wird. Wählen Sie **Überschreiben** aus, wenn eine vorhandene Datei durch eine neuere Version ersetzt werden soll. Wählen Sie **Keine** aus, wenn das Abonnement keine Datei ersetzen soll. In diesem Fall wird keine Übermittlung ausgeführt, wenn bereits eine Datei mit demselben Zielnamen und derselben Zielerweiterung vorhanden ist. Wählen Sie **Automatisch inkrementieren** aus, wenn Folgeversionen derselben Datei durch Anfügen einer Nummer an das Ende des Dateinamens hinzugefügt werden sollen.  
  
 Automatisches Kopieren  
 Wenn Sie die Funktion zum automatischen Kopieren verwenden, um die neueste Version einer Datei an mehrere Speicherorte zu kopieren, wird die Datei kopiert, sofern **Überschreiben** aktiviert ist. Wenn **Automatisch inkrementieren** oder **Keine**verwendet wurde, tritt bei der Übermittlung ein Fehler auf, und der **rsDeliveryError** -Fehler wird angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Abonnements für Berichtsserver im SharePoint-Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Specify Credential and Connection Information for Report Data Sources (Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen)](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
