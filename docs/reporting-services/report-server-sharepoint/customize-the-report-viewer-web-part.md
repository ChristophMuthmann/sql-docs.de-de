---
title: Anpassen der Berichts-Viewer-Webpart | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- Report Viewer Web Part [Reporting Services]
ms.assetid: 086d6546-7299-41bc-bca9-083a15a53679
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e5941044afa950ba41e23ce1c3507a51e6121556
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="customize-the-report-viewer-web-part"></a>Anpassen des Berichts-Viewer-Webparts
  Mithilfe des Berichts-Viewer-Webparts können Sie Berichte anzeigen, die auf einem Berichtsserver ausgeführt werden, der für die Ausführung im integrierten SharePoint-Modus konfiguriert ist. Sie können u. a. Berichtsdefinitionsdateien (RDL-Dateien) und Berichts-Generator-Berichte anzeigen. Berichte werden im Berichts-Viewer-Webpart automatisch auf einer neuen Seite angezeigt, doch können Sie auch einer vorhandenen Webseite oder Website ein Berichts-Viewer-Webpart hinzufügen, wenn auf der Seite ein bestimmter Bericht immer angezeigt werden soll.  
  
 Es gibt folgende Möglichkeiten, um das Berichts-Viewer-Webpart anzupassen:  
  
-   Ändern der Darstellung des Webparts durch Festlegen von Eigenschaften  
  
-   Auswählen der interaktiven Berichterstellungsfunktionen, die auf der Berichtssymbolleiste verfügbar sein sollen  
  
-   Angeben der verfügbaren Anzeigebereiche Im Berichts-Viewer-Webpart sind ein Berichtsansichtsbereich sowie ein Parameterbereich und ein Bereich für Anmeldeinformationen enthalten.  
  
 Sie können das Berichts-Viewer-Webpart nicht für die Unterstützung unterschiedlicher Dateitypen erweitern, Sie können auch die Berichtssymbolleiste nicht durch eine benutzerdefinierte Symbolleiste ersetzen oder der vorhandenen Symbolleiste neue Funktionalität hinzufügen. Zum Anpassen der Standardfunktionen müssen Sie ein benutzerdefiniertes Webpart erstellen.  
  
## <a name="setting-web-part-properties"></a>Festlegen von Webparteigenschaften  
 Ein Webpart weist benutzerdefinierte Eigenschaften auf, die zum Konfigurieren von bestimmter Funktionalität verwendet werden. Zudem besitzt ein Webpart gemeinsame Eigenschaften, die für alle Webparts eine Standardeinstellung darstellen.  
  
### <a name="change-default-properties"></a>Ändern von Standardeigenschaften  
 Das Berichts-Viewer-Webpart besitzt Standardeigenschaften, die ideal zum bedarfsgesteuerten Öffnen von Berichten in einer Bibliothek oder einem Ordner geeignet sind. In der Standardeinstellung werden alle verfügbaren Steuerelemente auf der Symbolleiste angezeigt, wobei die Höhe und die Breite so festgelegt sind, dass der gesamte verfügbare Platz auf der Webseite eingenommen wird. Wenn Sie die Standardeigenschaften ändern möchten, können Sie das Webpart unter **Siteeinstellungen**anpassen.  
  
1.  Klicken Sie im Menü **Websiteaktionen** auf **Siteeinstellungen**.  
  
2.  Klicken Sie unter den Katalogen auf **Webparts**.  
  
3.  Klicken Sie auf **ReportViewer.dwp**.  
  
4.  Öffnen Sie den Toolbereich, und legen Sie die Eigenschaften fest, die Sie verwenden möchten.  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>Anpassen eines auf einer Webseite eingebetteten Berichts-Viewers  
 Sie können Eigenschaften festlegen, um die Größe des Berichts-Viewers an die einer Webseite anzupassen. Für den Berichts-Viewer können derselbe Stil und dieselbe Farbe wie für die Seite verwendet werden, die diesen enthält. Sie können die Symbolleiste, die Dokumentstruktur und den Parameterbereich ganz oder teilweise ausblenden, um den Berichtsanzeigebereich im zugeordneten Bereich zu maximieren. Für den Bericht werden immer die beim Erstellen definierten Stile verwendet. Sie können die Darstellung eines Berichts nicht mehr anpassen, nachdem dieser in einer SharePoint-Bibliothek veröffentlicht wurde.  
  
 Wenn Sie das Berichts-Viewer-Webpart auf einer Webseite einbetten, sollten Sie die Eigenschaft **Report URL** auf einen bestimmten Bericht festlegen. Andernfalls werden im Berichts-Viewer Anweisungen zum Verknüpfen mit einem Bericht angezeigt. Die Anweisungen können Sie nicht anpassen oder entfernen.  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>Benutzerdefinierte Eigenschaften des Berichts-Viewer-Webparts  
 Wenn Sie benutzerdefinierte Eigenschaften festlegen, beachten Sie, dass einige Eigenschaften nur verwendet werden, wenn das Berichts-Viewer-Webpart auf einer Seite eingebettet ist. Zu diesen zählen Titel, Höhe, Breite, Chromtyp und Zone. Andere Eigenschaften, wie z. B. Symbolleisteneinstellungen und Parametereinstellungen, werden unabhängig davon verwendet, ob der Berichts-Viewer innerhalb einer Seite angezeigt wird oder einen Bericht im Ganzseitenmodus öffnet.  
  
 Die benutzerdefinierten Eigenschaften des Berichts-Viewer-Webparts werden nachfolgend aufgelistet.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|Bericht|Ein vollqualifizierter Pfad für einen Bericht, der sich auf der aktuellen SharePoint-Website oder auf einer Website innerhalb der gleichen Webanwendung oder Farm befindet. Optimale Ergebnisse beim Festlegen zusätzlicher Eigenschaften erzielen Sie, indem Sie nach dem Angeben der Berichts-URLs auf Anwenden klicken.|  
|Linkziel|Standard-HTML, die den Zielrahmen für die Anzeige von verknüpftem Inhalt im aktuellen Dokument angibt. Für Berichte, die Links zu externen Websites enthalten, können Sie angeben, ob ein Zieldokument den vorhandenen Bericht im aktuellen Fenster ersetzt oder in einem neuen Browserfenster geöffnet wird. Gültige Werte sind **_Top**, **_Blank**und **_Self**. Mit**_Top** wird das aktuelle Fenster verwendet, mit **_Blank** wird das Dokument in einem neuen Browserfenster geladen, und mit **_Self** wird das Dokument im aktuellen Frame geöffnet. Obwohl **_Parent** ein gültiger Wert für das Target-Attribut in HTML ist, sollten Sie ihn nicht für ein in eine Seite eingebettetes Berichts-Viewer-Webpart verwenden.|  
|Automatisches Generieren von Webparttiteln|Ein generierter Titel , der den Namen des Berichts-Viewer-Webparts und den Namen des Berichts enthält, abgetrennt durch einen Bindestrich. Wenn der Bericht über keinen Titel verfügt, wird der Berichtsdateiname verwendet. Der Titel ist sichtbar, wenn Sie ein Webpart zu einer Seite hinzufügen. Wenn dieses Kontrollkästchen aktiviert ist, wird der Titel bei jeder Aktualisierung der Seite generiert.|  
|Automatisches Generieren von Detaillinks für Webparts|Ein generierter Link, der über dem Webpart angezeigt wird. Sie können auf den Link klicken, um den Bericht auf einer neuen Seite im Ganzseitenmodus anzuzeigen.|  
|Anzeigen des Menüelements Berichts-Generator|Zeigt die Option des Menüs **Aktionen** an, mit der der Berichts-Generator geöffnet oder ausgeblendet wird.|  
|Anzeigen des Menüelements Abonnement.|Zeigt die Option des Menüs **Aktionen** an, mit der ein Abonnement für den Bericht erstellt wird, oder blendet sie aus.|  
|Anzeigen des Menüelements Druck|Zeigt die Option des Menüs **Aktionen** an, mit der der Bericht gedruckt wird, oder blendet sie aus.|  
|Anzeigen des Menüelements Export|Zeigt die Option des Menüs **Aktionen** an, mit der der Bericht exportiert wird, oder blendet sie aus.|  
|Anzeigen der Aktualisierungsschaltfläche|Zeigt die Aktualisierungsschaltfläche auf der Symbolleiste an oder blendet sie aus.|  
|Anzeigen der Steuerelemente für die Seitennavigation|Zeigt die Berichtsnavigationsschaltflächen auf der Symbolleiste an oder blendet sie aus. Diese Option ändert die Sichtbarkeit aller Navigationssteuerelemente.|  
|Anzeigen der Schaltfläche Zurück|Zeigt die Schaltfläche "Zurück" auf der Symbolleiste an oder blendet sie aus.|  
|Anzeigen der Suchsteuerelemente|Zeigt die Suchsteuerelemente auf der Symbolleiste an oder blendet sie aus. Die Suchsteuerelemente ermöglichen einem Benutzer, im gerenderten Bericht nach Text zu suchen. Diese Option ändert die Sichtbarkeit aller Suchsteuerelemente.|  
|Anzeigen des Zoomsteuerelement|Zeigt das Zoomsteuerelement auf der Symbolleiste an oder blendet es aus.|  
|Anzeigen der ATOM-Feed-Schaltfläche|Zeigt die ATOM-Feed-Schaltfläche auf der Symbolleiste an oder blendet sie aus.<br /><br /> ![Htmlviewer_datafeed](../../reporting-services/media/htmlviewer-datafeed.gif "Htmlviewer_datafeed")|  
|Symbolleistenspeicherort|Bestimmt die Position der Symbolleiste innerhalb des Berichts-Viewers. Gültige Werte sind **Top** und **Bottom**.|  
|Bereich Eingabeaufforderung|Gültige Werte sind unter anderem **Displayed**, **Collapsed**und **Hidden**. Mit**Displayed** wird der Parameterbereich für Berichte angezeigt, die parametrisierte Werte enthalten und für die eine Benutzereingabe erforderlich ist, bevor der Bericht ausgeführt werden kann. Verwenden Sie **Hidden** , wenn alle Berichtsparameter angegeben wurden und Sie nicht möchten, dass der Parameterbereich für Benutzer sichtbar ist.|  
|Breite des Parameterbereichs|Sie können die Maßeinheit und den Wert auswählen. Der Standardwert ist 200 Pixel. Die einzige Anforderung für diese Eigenschaft lautet, dass sie größer als 0 sein muss.|  
|Dokumentstruktur|Ein Steuerelement für die Berichtsnavigation, das im Bericht definiert und zum Bereitstellen eines Zugriffs auf bestimmte Abschnitte eines Berichts mit einem Klick verwendet wird. Es ist in HTML-Berichten verfügbar. Die Dokumentstruktur wird in einem reduzierbaren Bereich neben dem Berichtsansichtsbereich angezeigt. Gültige Werte sind unter anderem **Displayed**, **Collapsed**und **Hidden**. Wenn für einen Bericht eine Dokumentstruktur definiert ist, ist der Bereich standardmäßig erweitert, sofern er nicht in den Webparteigenschaften als ausgeblendet oder reduziert markiert ist. Wenn die Dokumentstruktur reduziert ist, können Sie auf den Pfeil klicken, um sie zu erweitern.|  
|Breite des Dokumentstrukturbereichs|Sie können die Maßeinheit und den Wert auswählen. Der Standardwert ist 200 Pixel. Die einzige Anforderung für diese Eigenschaft lautet, dass sie größer als 0 sein muss.|  
|Parameter laden|Abrufen von Parametereigenschaften für den Bericht. Nicht alle Berichte verfügen über Parameter. Wenn der Bericht nicht über Parameter verfügt, werden keine Werte zurückgegeben. Wenn Sie Eigenschaften für einen soeben hochgeladenen Bericht festlegen, erhalten Sie möglicherweise eine Fehlermeldung, die angibt, dass die Datenquellenverbindung gelöscht wurde. Wenn dies auftritt, setzen Sie die Verbindung zurück, und stellen Sie das Festlegen der Parametereigenschaften fertig, nachdem die Verbindung angegeben wurde. Weitere Informationen zum Einrichten der Verbindung finden Sie unter [Erstellen und Verwalten von freigegebenen Datenquellen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).<br /><br /> Optimale Ergebnisse erzielen Sie, indem Sie auf **Anwenden** klicken, bevor Sie auf Parameter laden klicken.<br /><br /> Nach dem Laden von Parametereigenschaften können Sie sie auf die gleiche Weise festlegen, wie Sie dies auf den Parametereigenschaftenseiten des Berichts tun würden. Weitere Informationen zum Festlegen von Parametern finden Sie unter [Festlegen von Parametern für einen veröffentlichten Bericht &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  
  
## <a name="customizing-the-toolbar"></a>Anpassen der Symbolleiste  
 Die Symbolleiste wird unterhalb des Titels angezeigt und erstreckt sich über den oberen Rand des Berichts. Die Symbolleiste stellt ein Menü **Aktionen** , eine Seitennavigation für paginierte Berichte, eine Aktualisierung und einen Zoom bereit. Sie enthält ein Dokumentstruktur-Steuerelement für Berichte, die über eine Dokumentstruktur verfügen. Das Menü **Aktionen** enthält Befehle zum Exportieren des Berichts, zum Suchen nach Text oder Zahlen in einem Bericht, zum Drucken des Berichts und zum Öffnen des Berichts im Berichts-Generator.  
  
 Sie können dem Menü  **Aktionen** keine neuen Befehle hinzufügen, aber Sie können es anpassen, indem Sie die Optionen ändern, die Benutzern sichtbar sind. Um die Sichtbarkeit von Symbolleistenschaltflächen und Steuerelementen zu ändern, ändern Sie Optionen im Abschnitt **Sichtbarkeit von ToolBar-Elementen** des Webparts. Sie können auch den Befehl **Drucken** oder bestimmte Exportformate entfernen, indem Sie die Verfügbarkeit dieser Funktionen auf dem Berichtsserver aufheben. Für Berichte mit Seitenumbrüchen sind Steuerelemente für die Seitennavigation verfügbar. Andernfalls besteht der Bericht aus einer einzelnen Seite unterschiedlicher Länge. Mit**Aktualisieren** wird der Bericht erneut verarbeitet, wobei die für den Bericht aktuellen Parameter verwendet werden. Wenn Sie alle Steuerelemente auf einer Zeile anzeigen möchten, legen Sie die Gesamtbreite des Webparts auf mindestens 400 Pixel fest.  
  
## <a name="customizing-the-viewing-area"></a>Anpassen des Ansichtsbereichs  
 Der Ansichtsbereich wird für das Anzeigen von Berichten verwendet. Der Berichtsansichtsbereich wird ggf. mit den Bereichen Parameter und Anmeldeinformationen gemeinsam verwendet. Wenn Anmeldeinformationen erforderlich sind, wird der Bereich Anmeldeinformationen neben einem leeren Berichtsansichtsbereich angezeigt. Der Bereich Anmeldeinformationen wird geschlossen, nachdem der Benutzer Anmeldeinformationen eingegeben und den Bericht ausgeführt hat. Wenn Sie den Text anpassen möchten, mit dem Benutzer zum Festlegen von Anmeldeinformationen aufgefordert werden, ändern Sie die Datenquellen-Verbindungseigenschaften. Weitere Informationen finden Sie unter [Erstellen und Verwalten von freigegebenen Datenquellen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Im Parameterbereich werden Felder zum Eingeben von Werten vor dem Ausführen des Berichts bereitgestellt. Er wird nur verwendet, wenn eine Berichtsdefinition Parameter enthält. Bei Anzeige des Parameterbereichs oder des Bereichs für Anmeldeinformationen wird die Berichtsansicht so angepasst, dass die verbleibende Breite des Webparts verwendet wird. Sie können Eigenschaften für das Webpart festlegen, um die Breite des Parameterbereichs anzupassen. Sie können auch die Bezeichnungen festlegen, die neben den einzelnen Parametern auf der Seite angezeigt werden. Weitere Informationen zum Bearbeiten von Parameterbezeichnungen finden Sie unter [Festlegen von Parametern für einen veröffentlichten Bericht &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Fügen Sie den Berichts-Viewer-Webpart auf einer Webseite &#40; Reporting Services in SharePoint integrierten Modus &#41;](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  
  
  
