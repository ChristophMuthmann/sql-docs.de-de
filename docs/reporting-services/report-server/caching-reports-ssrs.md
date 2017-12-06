---
title: Zwischenspeichern von Berichten (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
caps.latest.revision: "44"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 31a4eb9c303fe2c7d676cca535de3c64272f0caa
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="caching-reports-ssrs"></a>Zwischenspeichern von Berichten (SSRS)
  Ein Berichtsserver kann eine Kopie eines verarbeiteten Berichts zwischenspeichern und diese anzeigen, wenn ein Benutzer den Bericht öffnet. Für den Benutzer ist der einzige Hinweis darauf, dass es sich bei dem Bericht um eine zwischengespeicherte Kopie handelt, das Datum und die Uhrzeit des Berichts. Wenn der Bericht kein aktuelles Datum oder keine aktuelle Uhrzeit aufweist und es sich um keine Momentaufnahme handelt, wurde der Bericht aus dem Cache abgerufen.  
  
 Durch die Zwischenspeicherung kann ein Bericht schneller abgerufen werden, falls der Bericht sehr umfangreich ist oder häufig abgerufen wird. Beim Neustart des Servers werden alle zwischengespeicherten Instanzen wiederhergestellt, wenn der Berichtsserverdienst wieder online ist.  
  
 Die Zwischenspeicherung ist eine Technik zur Leistungsoptimierung. Der Inhalt des Zwschenspeichers ist flüchtig und kann sich beim Hinzufügen, Ersetzen oder Entfernen von Berichten ändern. Falls Sie eine zuverlässigere Zwischenspeicherungsstrategie benötigen, sollten Sie eine Momentaufnahme erstellen. Weitere Informationen finden Sie unter [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] speichert temporäre Dateien in einer Datenbank, damit Benutzersitzungen und Berichtsverarbeitung unterstützt werden. Diese Dateien werden zur internen Verwendung und zur Unterstützung einer konsistenten Anzeige während einer einzelnen Browsersitzung zwischengespeichert. Weitere Informationen zur Zwischenspeicherung von temporären Dateien für die interne Verwendung finden Sie unter [Berichtsserver-Datenbank (einheitlicher SSRS-Modus)](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md).  
  
## <a name="cached-instances"></a>Zwischengespeicherte Instanzen  
 Eine zwischengespeicherte Instanz eines Berichts basiert auf dem Berichtszwischenformat. Der Berichtsserver führt im Allgemeinen die Zwischenspeicherung einer Berichtsinstanz basierend auf dem Berichtsnamen durch. Wenn allerdings ein Bericht gemäß den Abfrageparametern verschiedene Daten enthalten kann, können jeweils mehrere Versionen des Berichts zwischengespeichert werden. Angenommen, Sie haben einen parametrisierten Bericht, der einen Landes-/Regionscode als Parameterwert verwendet. Wenn vier verschiedene Benutzer vier eindeutige Landes-/Regionscodes angeben, werden vier zwischengespeicherte Kopien erstellt.  
  
 Der erste Benutzer, der den Bericht mit einem eindeutigen Landes-/Regionscode ausführt, erstellt einen zwischengespeicherten Bericht mit Daten für dieses Land bzw. diese Region. Benutzern, die später den Bericht mithilfe desselben Landes-/Regionscodes anfordern, wird dann die zwischengespeicherte Kopie angezeigt.  
  
 Nicht alle Berichte können zwischengespeichert werden. Falls ein Bericht benutzerabhängige Daten enthält, Benutzer zur Eingabe von Anmeldeinformationen auffordert oder die Windows-Authentifizierung verwendet, ist keine Zwischenspeicherung möglich.  
  
## <a name="refreshing-the-cache"></a>Aktualisieren des Caches  
 Ein zwischengespeicherter Bericht wird durch eine neuere Version ersetzt, wenn ein Benutzer den Bericht auswählt, nachdem eine zuvor zwischengespeicherte Version bereits abgelaufen ist. Berichte, die zum Ausführen als zwischengespeicherte Instanzen konfiguriert sind, werden gemäß den Ablaufeinstellungen regelmäßig aus dem Cache entfernt. Sie können die Ablaufzeit eines Berichts gemäß den Unmittelbarkeitsanforderungen in Minuten oder zu einer geplanten Uhrzeit festlegen. Berichte können nicht direkt aus dem Cache gelöscht werden, nur wenn Sie die SOAP-API benutzen.  
  
 Zum Konfigurieren eines Cacheablaufzeitpunkts können Sie einen freigegebenen oder einen berichtsspezifischen Zeitplan verwenden. Falls Sie einen freigegebenen Zeitplan verwenden und diesen später anhalten, läuft der Cache nicht ab, während der Zeitplan deaktiviert ist. Wird der freigegebene Zeitplan später gelöscht, wird eine Kopie der Zeitplaneinstellungen als berichtsspezifischer Zeitplan gespeichert.  
  
 Wenn ein Zeitplan abläuft oder das Zeitplanungsmodul zum Ablaufzeitpunkt des Caches nicht verfügbar ist, führt der Berichtsserver einen Livebericht aus, bis die geplanten Operationen fortgesetzt werden können (durch Erweitern des Zeitplans oder Starten des Zeitplanungsdiensts).  
  
## <a name="preloading-the-cache"></a>Vorabladen des Caches  
 Zur Verbesserung der Serverleistung können Sie vorab Daten in den Cache laden. Sie können den Cache auf die folgenden beiden Weisen mit einer Auflistung parametrisierter Berichtsinstanzen vorab laden:  
  
1.  Erstellen Sie einen Cacheaktualisierungsplan. Wenn Sie einen Aktualisierungsplan erstellen, können Sie einen Zeitplan für einen einzelnen Bericht oder einen freigegebenen Zeitplan angeben.  
  
2.  Erstellen Sie ein datengesteuertes Abonnement, das den NULL-Übermittlungsanbieter verwendet. Wenn Sie den NULL-Übermittlungsanbieter als eine Übermittlungsmethode im Abonnement angeben, sieht der Berichtsserver die Berichtsserver-Datenbank als Ziel der Übermittlung an und verwendet eine spezielle Renderingerweiterung, die als NULL-Renderingerweiterung bezeichnet wird. Im Gegensatz zu anderen Übermittlungserweiterungen verfügt die NULL-Übermittlungserweiterung nicht über Übermittlungseinstellungen, die mithilfe einer Abonnementdefinition konfiguriert werden können.  
  
 Das Zwischenspeichern eines Berichts ist besonders hilfreich, wenn Sie mehrere Instanzen eines parametrisierten Berichts zwischenspeichern möchten, wobei zum Erstellen unterschiedlicher Berichtsinstanzen unterschiedliche Parameterwerte verwendet werden. Beachten Sie, dass nur abfragebasierte Parameter im Bericht angegeben werden können.  
  
 Beim Angeben eines Zeitplans oder Erstellen des datengesteuerten Abonnements planen Sie, wie oft Berichte an den Cache übermittelt werden. Damit neue Kopien an den Cache übermittelt werden, müssen die alten Kopien abgelaufen sein. Deshalb müssen die Ausführungseigenschaften des Berichts die Einstellungen für den Cacheablaufzeitpunkt enthalten. Die Einstellungen für den Cacheablaufzeitpunkt müssen mit dem von Ihnen definierten Abonnementzeitplan konsistent sein. Wenn Sie z. B. ein Abonnement erstellen, das jede Nacht ausgeführt wird, sollte der Cache ebenfalls jede Nacht zur Laufzeit des Abonnements abgelaufen sein. Wenn auf der Eigenschaftenseite Ausführung keine Ablaufzeiten angegeben sind, werden neue Übermittlungen ignoriert. Weitere Informationen zu Cacheaktualisierungsplänen finden Sie unter [Zeitpläne](../../reporting-services/subscriptions/schedules.md). Weitere Informationen zur Einstellung von Eigenschaften finden Sie unter [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md). Weitere Informationen zum Verwenden datengesteuerter Abonnements finden Sie unter [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Bedingungen, die zum Ablaufen des Caches führen  
 Ein zwischengespeicherter Bericht wird als Konsequenz aus den folgenden Ereignissen ungültig: Die Berichtsdefinition wird geändert, Berichtsparameter werden geändert, die Datenquellen-Anmeldeinformationen ändern sich, oder die Optionen zum Ausführen des Berichts werden geändert. Wenn Sie einen Bericht löschen, wird auch die zwischengespeicherte Version gelöscht, falls sie schon im Cache gespeichert wurde.  
  
 Falls ein Bericht aus irgendeinem Grund nicht aus einer zwischengespeicherten Instanz generiert werden kann (z. B., wenn die von einem Benutzer angegebenen Parameterwerte von den Werten abweichen, mit denen der zwischengespeicherte Bericht erstellt wird), führt der Berichtsserver den Bericht erneut aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Verarbeitungsoptionen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Konzepte von Reporting Services (SSRS)](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Vorabladen des Caches (Berichts-Manager)](../../reporting-services/report-server/preload-the-cache-report-manager.md)   
 [Zeitpläne](../../reporting-services/subscriptions/schedules.md)   
 [Zwischenspeichern von freigegebenen Datasets (SSRS)](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)   
 [Optionen zur Cacheaktualisierung &#40;Berichts-Manager&#41;](http://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)  
  
  
