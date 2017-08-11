---
title: Vorabladen des Caches (Berichts-Manager) | Microsoft Docs
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
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c5543c648289dee007a2249299ecb006d41f6b98
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="preload-the-cache-report-manager"></a>Vorabladen des Caches (Berichts-Manager)
  Sie können den Cache für ein freigegebenes Dataset vorab laden, indem Sie einen Cacheaktualisierungsplan für das freigegebene Dataset erstellen.  
  
 Sie können den Cache für einen Bericht in die zwei Weisen vorab laden:  
  
1.  Erstellen Sie einen Cacheaktualisierungsplan für den Bericht. Dies ist die bevorzugte Methode.  
  
2.  Verwenden Sie ein datengesteuertes Abonnement zum Vorabladen des Caches mit Instanzen parametrisierter Berichte. In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Versionen vor [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]bestand darin die einzige Möglichkeit, den Cache vorab zu laden. Weitere Informationen finden Sie unter [Zwischenspeichern von Berichten &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)bestand darin die einzige Möglichkeit, den Cache vorab zu laden.  
  
 Die folgenden Bedingungen müssen erfüllt sein, bevor Sie einen Bericht oder ein freigegebenes Dataset zwischenspeichern können:  
  
-   Für das freigegebene Dataset oder den Bericht muss die Zwischenspeicherung aktiviert sein.  
  
-   Die freigegebenen Datenquellen für das freigegebene Dataset oder den Bericht müssen für die Verwendung gespeicherter Anmeldeinformationen oder keiner Anmeldeinformationen konfiguriert sein.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst muss ausgeführt werden.  
  
### <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>So laden Sie den Cache vorab, indem Sie einen Cacheaktualisierungsplan erstellen  
  
1.  Starten Sie den [Berichts-Manager im einheitlichen SSRS-Modus](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt** und dann zu dem Element, das zwischengespeichert werden soll.  
  
3.  Zeigen Sie auf das Element, und klicken Sie auf die Dropdownliste und anschließend auf **Verwalten**.  
  
4.  Klicken Sie auf die Registerkarte **Optionen zur Cacheaktualisierung** .  
  
5.  Klicken Sie auf der Symbolleiste auf **Neuer Cacheaktualisierungsplan**.  
  
    > [!NOTE]  
    >  Wenn für das Element keine Zwischenspeicherung aktiviert ist, werden Sie aufgefordert, das Zwischenspeichern zu aktivieren. Um das Zwischenspeichern zu aktivieren, klicken Sie auf **OK**.  
  
     Die Seite Cacheaktualisierungsplan wird geöffnet.  
  
6.  Geben Sie optional eine Beschreibung für den Aktualisierungsplan ein.  
  
7.  Klicken Sie für einen freigegebenen Zeitplan auf **Freigegebener Zeitplan**, und wählen Sie dann den Namen des zu verwendenden Zeitplans aus.  
  
     Klicken Sie für einen benutzerdefinierten Zeitplan auf **Elementspezifischer Zeitplan**und anschließend auf **Konfigurieren**.  
  
8.  Konfigurieren Sie den Zeitplan.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>So laden Sie den Cache mit einem benutzerspezifischen Bericht vorab, indem Sie ein datengesteuertes Abonnement verwenden  
  
1.  Starten Sie den [Berichts-Manager im einheitlichen SSRS-Modus](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt** und dann zum Bericht, für den Sie ein Abonnement erstellen möchten.  
  
3.  Klicken Sie auf den Bericht und auf die Registerkarte **Abonnements** , und klicken Sie anschließend auf **Neues datengesteuertes Abonnement**.  
  
4.  Optional geben Sie eine Beschreibung für das Abonnement ein.  
  
5.  Wählen Sie in der Liste **Geben Sie an, wie Empfänger benachrichtigt werden** die Option **NULL-Übermittlungsanbieter**.  
  
6.  Geben Sie einen Datenquellentyp an, und klicken Sie auf **Weiter** , um die Datenquelle zu konfigurieren.  
  
7.  Geben Sie den Verbindungstyp, die Verbindungszeichenfolge und die Anmeldeinformationen für den Zugriff auf die Datenquelle mit Abonnentendaten an. Im folgenden Beispiel wird eine Verbindungszeichenfolge erläutert, die für die Verbindung zur Subscribers-Datenbank von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird:  
  
    ```  
    data source=<servername>; initial catalog=Subscribers  
    ```  
  
8.  Klicken Sie auf **Weiter**.  
  
9. Geben Sie die Abfrage oder den Befehl an, die bzw. der Abonnentendaten abruft. Sie können auch den Timeoutzeitraum für Abfragen erhöhen, deren Verarbeitung lange dauert. Beispiel:  
  
    ```  
    Select * from UserInfo  
    ```  
  
10. Klicken Sie auf **Überprüfen**. Die Abfrage muss überprüft werden, bevor der Vorgang fortgesetzt werden kann. Wenn die Meldung **Die Abfrage wurde erfolgreich überprüft** angezeigt wird, klicken Sie auf **Weiter**.  
  
11. Da für den NULL-Übermittlungsanbieter keine Einstellungen für die Übermittlungserweiterung konfiguriert werden können, klicken Sie auf **Weiter**.  
  
12. Geben Sie Berichtsparameterwerte für das Abonnement an, und klicken Sie auf **Weiter**.  
  
13. Geben Sie an, wann das Abonnement verarbeitet wird. Wählen Sie nicht **Wenn die Berichtsdaten auf dem Berichtsserver aktualisiert werden**. Diese Option ist nur für Berichtsmomentaufnahmen verfügbar. Wenn Sie einen vorhandenen Zeitplan verwenden möchten, wählen Sie **Nach einem freigegebenen Zeitplan**.  
  
     Oder klicken Sie zum Erstellen eines benutzerdefinierten Zeitplans auf **Nach einem Zeitplan, der für dieses Abonnement erstellt wurde** , und klicken Sie dann auf **Weiter**. Konfigurieren Sie den Zeitplan, und klicken Sie dann auf **Fertig stellen**.  
  
    > [!NOTE]  
    >  Die Abonnenten empfangen nur dann den neuesten Bericht, wenn der von Ihnen konfigurierte Zeitplan konsistent mit dem Zeitplan für die Berichtsübermittlung ist, den Sie für die Abonnenten definiert haben. Weitere Informationen finden Sie unter [Berichts-Manager &#40; SSRS im einheitlichen Modus &#41; ](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
14. Konfigurieren Sie die Ausführungsoptionen für den Bericht wie folgt: Klicken Sie auf der Berichtsseite auf die Registerkarte **Eigenschaften** .  
  
15. Klicken Sie im linken Bereich auf die Registerkarte **Ausführung** .  
  
16. Wählen Sie auf der Seite die Option **Diesen Bericht mit den neuesten Daten rendern**.  
  
17. Wählen Sie eine der folgenden zwei Cacheoptionen aus, und konfigurieren Sie die Ablaufzeit wie folgt:  
  
    -   Wenn die zwischengespeicherte Kopie nach einem bestimmten Zeitraum ablaufen soll, klicken Sie auf **Eine temporäre Kopie des Berichts zwischenspeichern. Kopie des Berichts nach einer Anzahl von Minuten abläuft.** Geben Sie die Anzahl von Minuten für den Berichtsablauf ein.  
  
    -   Wenn die zwischengespeicherte Kopie nach einem Zeitplan ablaufen soll, klicken Sie auf **eine temporäre Kopie des Berichts Zwischenspeichern. Kopie des Berichts nach folgendem Zeitplan abläuft.** Klicken Sie auf **Konfigurieren**, oder wählen Sie einen freigegebenen Zeitplan aus, um einen Zeitplan für den Berichtsablauf festzulegen.  
  
18. Klicken Sie auf **Anwenden**.  
  
## <a name="see-also"></a>Siehe auch  
 [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Erstellen eines datengesteuerten Abonnements &#40;SSRS-Tutorial&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Leistung, Momentaufnahmen, Zwischenspeichern &#40; Reporting Services &#41;](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)   
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Zwischenspeichern von Berichten &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
  
