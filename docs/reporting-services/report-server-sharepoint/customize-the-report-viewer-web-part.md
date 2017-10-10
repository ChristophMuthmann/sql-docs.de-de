---
title: Anpassen des Berichts-Viewer-Webparts | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 38f23cf5d75c47be55e1820a4421a507a73df54e
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="customize-the-report-viewer-web-part"></a>Anpassen des Berichts-Viewer-Webparts

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Sie können das Berichts-Viewer-Webpart verwenden, zum Anzeigen von Berichten, die auf einem Berichtsserver ausgeführt werden, die für SharePoint-Integration konfiguriert ist. Sie können u. a. Berichtsdefinitionsdateien (RDL-Dateien) und Berichts-Generator-Berichte anzeigen. Berichte im Berichts-Viewer-Webpart auf einer neuen Seite automatisch, doch Sie können auch einen Berichts-Viewer-Webpart auf einer vorhandenen Webseite oder Website hinzufügen, wenn Sie ein bestimmter Bericht immer auf dieser Seite angezeigt werden soll.

> [!NOTE]
> Obwohl sie identische Namen haben, im Berichts-Viewer Webpart, das über installiert ist die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in unterscheidet sich von der Berichts-Viewer-Webpart, das in der Datei "RSWebParts.cab" enthalten ist. Die Anweisungen in diesem Thema sind speziell für das Berichts-Viewer-Webpart, das über installiert ist die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-in.

 Sie können das Berichts-Viewer-Webpart auf folgende Weise anpassen:  
  
-   Ändern Sie die Darstellung des Webparts durch Festlegen von Eigenschaften.  
  
-   Auswählen der interaktiven Berichterstellungsfunktionen, die auf der Berichtssymbolleiste verfügbar sein sollen  
  
-   Angeben der verfügbaren Anzeigebereiche Der Berichts-Viewer-Webpart ist ein berichtsansichtsbereich, ein Parameterbereich und ein Bereich für Anmeldeinformationen enthalten.  
  
 Sie können nicht den Berichts-Viewer-Webpart Unterstützung unterschiedlicher Dateitypen erweitern, und Sie nicht die Berichtssymbolleiste durch eine benutzerdefinierte Symbolleiste ersetzen oder der vorhandenen Symbolleiste neue Funktionalität hinzufügen. Wenn Sie die Anpassung der Standardfunktionen benötigen, sollten Sie ein benutzerdefiniertes Webpart erstellen.  

## <a name="setting-web-part-properties"></a>Festlegen von Webparteigenschaften

 Ein Webpart weist benutzerdefinierte Eigenschaften, die zum Konfigurieren von bestimmter Funktionalität verwendet werden. Zudem besitzt ein Webpart gemeinsame Eigenschaften, die für alle Webparts eine Standardeinstellung darstellen.  
  
### <a name="change-default-properties"></a>Ändern von Standardeigenschaften

 Der Berichts-Viewer-Webpart hat Standardeigenschaften, die ideal zum Öffnen von Berichten bei Bedarf aus einer Bibliothek oder einem Ordner geeignet sind. Standardmäßig werden alle verfügbaren Steuerelemente auf der Symbolleiste angezeigt, und Höhe und Breite werden festgelegt, können alle verfügbaren Platz auf der Webseite verwenden. Wenn Sie die Standardeigenschaften ändern möchten, können Sie anpassen, dass das Webpart **Standorteinstellungen**.  
  
1.  Klicken Sie im Menü **Websiteaktionen** auf **Siteeinstellungen**.  
  
2.  Klicken Sie unter den Katalogen auf **-Webparts**.  
  
3.  Klicken Sie auf **ReportViewer.dwp**.  
  
4.  Öffnen Sie den Toolbereich, und legen Sie die Eigenschaften fest, die Sie verwenden möchten.  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>Anpassen von einem auf einer Webseite eingebetteten Berichts-Viewer

 Sie können Eigenschaften für den Berichts-Viewers in eine Webseite passt festlegen. Für den Berichts-Viewer können derselbe Stil und dieselbe Farbe wie für die Seite verwendet werden, die diesen enthält. Sie können die Symbolleiste, die Dokumentstruktur und den Parameterbereich ganz oder teilweise ausblenden, um den Berichtsanzeigebereich im zugeordneten Bereich zu maximieren. Für den Bericht werden immer die beim Erstellen definierten Stile verwendet. Sie können die Darstellung eines Berichts nicht mehr anpassen, nachdem dieser in einer SharePoint-Bibliothek veröffentlicht wurde.  
  
 Wenn Sie den Berichts-Viewer-Webpart auf einer Webseite einbetten, legen Sie die **Berichts-URL** Eigenschaft auf einen bestimmten Bericht. Andernfalls werden im Berichts-Viewer Anweisungen zum Verknüpfen mit einem Bericht angezeigt. Die Anweisungen können Sie nicht anpassen oder entfernen.  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>Benutzerdefinierte Eigenschaften des Berichts-Viewer-Webparts

 Wenn Sie benutzerdefinierte Eigenschaften festlegen, werden Sie beachten Sie, dass einige Eigenschaften werden nur verwendet, wenn der Berichts-Viewer-Webpart auf einer Seite eingebettet ist. Zu diesen zählen Titel, Höhe, Breite, Chromtyp und Zone. Andere Eigenschaften, wie z. B. Symbolleisteneinstellungen und Parametereinstellungen, werden unabhängig davon verwendet, ob der Berichts-Viewer innerhalb einer Seite angezeigt wird oder einen Bericht im Ganzseitenmodus öffnet.  
  
 Die benutzerdefinierten Eigenschaften des Berichts-Viewer-Webparts sind unten aufgeführt.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|Bericht|Ein vollqualifizierter Pfad für einen Bericht, der sich auf der aktuellen SharePoint-Website oder auf einer Website innerhalb der gleichen Webanwendung oder Farm befindet. Optimale Ergebnisse beim Festlegen zusätzlicher Eigenschaften erzielen Sie, indem Sie nach dem Angeben der Berichts-URLs auf Anwenden klicken.|  
|Linkziel|Standard-HTML, die den Zielrahmen für die Anzeige von verknüpftem Inhalt im aktuellen Dokument angibt. Für Berichte, die Links zu externen Websites enthalten, können Sie angeben, ob ein Zieldokument den vorhandenen Bericht im aktuellen Fenster ersetzt oder in einem neuen Browserfenster geöffnet wird. Gültige Werte sind **_Top**, **_Blank**und **_Self**. Mit**_Top** wird das aktuelle Fenster verwendet, mit **_Blank** wird das Dokument in einem neuen Browserfenster geladen, und mit **_Self** wird das Dokument im aktuellen Frame geöffnet. Obwohl **_Parent** ist ein gültiger Wert für den Target-Attribut in HTML, verwenden sie nicht für ein Berichts-Viewer-Webpart, das auf einer Seite eingebettet ist.|  
|Titel-Webpart automatisch generieren|Ein generierter Titel, der den Namen des Berichts-Viewer-Webparts und den Namen des Berichts, getrennt durch einen Bindestrich enthält. Wenn der Bericht über keinen Titel verfügt, wird der Berichtsdateiname verwendet. Der Titel ist sichtbar, wenn Sie ein Webpart zu einer Seite hinzufügen. Wenn dieses Kontrollkästchen aktiviert ist, wird der Titel bei jeder Aktualisierung der Seite generiert.|  
|Automatisches Generieren von Detaillinks-Webpart|Ein generierter Link, der über dem Webpart angezeigt wird. Sie können auf den Link klicken, um den Bericht auf einer neuen Seite im Ganzseitenmodus anzuzeigen.|  
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
|Dokumentstruktur|Ein Steuerelement für die Berichtsnavigation, das im Bericht definiert und zum Bereitstellen eines Zugriffs auf bestimmte Abschnitte eines Berichts mit einem Klick verwendet wird. Es ist in HTML-Berichten verfügbar. Die Dokumentstruktur wird in einem reduzierbaren Bereich neben dem Berichtsansichtsbereich angezeigt. Gültige Werte sind unter anderem **Displayed**, **Collapsed**und **Hidden**. Wenn für einen Bericht eine Dokumentstruktur definiert ist, ist der Bereich standardmäßig erweitert, es sei denn, in den Webparteigenschaften als ausgeblendet oder reduziert markiert. Wenn die Dokumentstruktur reduziert ist, können Sie auf den Pfeil klicken, um sie zu erweitern.|  
|Breite des Dokumentstrukturbereichs|Sie können die Maßeinheit und den Wert auswählen. Der Standardwert ist 200 Pixel. Die einzige Anforderung für diese Eigenschaft lautet, dass sie größer als 0 sein muss.|  
|Parameter laden|Abrufen von Parametereigenschaften für den Bericht. Nicht alle Berichte verfügen über Parameter. Wenn der Bericht nicht über Parameter verfügt, werden keine Werte zurückgegeben. Wenn Sie Eigenschaften für einen soeben hochgeladenen Bericht festlegen, erhalten Sie möglicherweise eine Fehlermeldung, die angibt, dass die Datenquellenverbindung gelöscht wurde. Wenn dies auftritt, setzen Sie die Verbindung zurück, und stellen Sie das Festlegen der Parametereigenschaften fertig, nachdem die Verbindung angegeben wurde. Weitere Informationen zum Festlegen der Verbindung finden Sie unter [erstellen und verwalten freigegebene Datenquellen &#40; Reporting Services in SharePoint integrierten Modus &#41; ](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).<br /><br /> Optimale Ergebnisse erzielen Sie, indem Sie auf **Anwenden** klicken, bevor Sie auf Parameter laden klicken.<br /><br /> Nach dem Laden von Parametereigenschaften können Sie sie auf die gleiche Weise festlegen, wie Sie dies auf den Parametereigenschaftenseiten des Berichts tun würden. Weitere Informationen dazu, wie die Dienstparameter festlegen können, finden Sie unter [legen Sie Parameter für einen publizierten Bericht &#40; Reporting Services in SharePoint integrierten Modus &#41; ](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  

## <a name="customizing-the-toolbar"></a>Anpassen der Symbolleiste

 Die Symbolleiste wird unterhalb des Titels angezeigt und erstreckt sich über den oberen Rand des Berichts. Die Symbolleiste stellt ein Menü **Aktionen** , eine Seitennavigation für paginierte Berichte, eine Aktualisierung und einen Zoom bereit. Sie enthält ein Dokumentstruktur-Steuerelement für Berichte, die über eine Dokumentstruktur verfügen. Das Menü **Aktionen** enthält Befehle zum Exportieren des Berichts, zum Suchen nach Text oder Zahlen in einem Bericht, zum Drucken des Berichts und zum Öffnen des Berichts im Berichts-Generator.  
  
 Sie können dem Menü  **Aktionen** keine neuen Befehle hinzufügen, aber Sie können es anpassen, indem Sie die Optionen ändern, die Benutzern sichtbar sind. Um die Sichtbarkeit von Symbolleistenschaltflächen und Steuerelementen zu ändern, ändern Sie die Optionen in der **Symbolleiste Elemente Sichtbarkeit** Abschnitt des Webparts. Sie können auch den Befehl **Drucken** oder bestimmte Exportformate entfernen, indem Sie die Verfügbarkeit dieser Funktionen auf dem Berichtsserver aufheben. Für Berichte mit Seitenumbrüchen sind Steuerelemente für die Seitennavigation verfügbar. Andernfalls besteht der Bericht aus einer einzelnen Seite unterschiedlicher Länge. Mit**Aktualisieren** wird der Bericht erneut verarbeitet, wobei die für den Bericht aktuellen Parameter verwendet werden. Um alle Steuerelemente in einer Zeile anzeigen möchten, legen Sie die Gesamtbreite des Webparts auf mindestens 400 Pixel fest.  

## <a name="customizing-the-viewing-area"></a>Anpassen des Ansichtsbereichs

 Der Ansichtsbereich wird für das Anzeigen von Berichten verwendet. Der Berichtsansichtsbereich wird ggf. mit den Bereichen Parameter und Anmeldeinformationen gemeinsam verwendet. Wenn Anmeldeinformationen erforderlich sind, wird der Bereich Anmeldeinformationen neben einem leeren Berichtsansichtsbereich angezeigt. Der Bereich Anmeldeinformationen wird geschlossen, nachdem der Benutzer Anmeldeinformationen eingegeben und den Bericht ausgeführt hat. Wenn Sie den Text anpassen möchten, mit dem Benutzer zum Festlegen von Anmeldeinformationen aufgefordert werden, ändern Sie die Datenquellen-Verbindungseigenschaften. Weitere Informationen finden Sie unter [erstellen und verwalten freigegebene Datenquellen &#40; Reporting Services in SharePoint integrierten Modus &#41; ](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Im Parameterbereich werden Felder zum Eingeben von Werten vor dem Ausführen des Berichts bereitgestellt. Er wird nur verwendet, wenn eine Berichtsdefinition Parameter enthält. Bei Anzeige des Parameterbereichs oder die Anmeldeinformationen die Berichtsansicht angepasst, dass die verbleibende Breite des Webparts verwendet. Sie können Eigenschaften festlegen, für das Webpart, um die Breite des Parameterbereichs anzupassen. Sie können auch die Bezeichnungen festlegen, die neben den einzelnen Parametern auf der Seite angezeigt werden. Weitere Informationen zum Ändern von parameterbezeichnungen finden Sie unter [legen Sie Parameter für einen publizierten Bericht &#40; Reporting Services in SharePoint integrierten Modus &#41; ](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Siehe auch

 [Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Der Berichts-Viewer-Webpart zu einer Webseite hinzufügen](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
