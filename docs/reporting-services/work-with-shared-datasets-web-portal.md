---
title: Arbeiten mit freigegebenen Datasets (Webportal) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2641ea84-9343-4e6f-aec1-25339031b163
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6dfbc134c0f0e351648d19cf8c485fe25a58eb99
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="work-with-shared-datasets---web-portal"></a>Arbeiten Sie mit freigegebenen Datasets - Webportal

[!INCLUDE[ssrs-appliesto-sql2016-preview](../includes/ssrs-appliesto-sql2016-preview.md)]

Mit einem freigegebenen Dataset können Sie die Einstellungen für ein Dataset getrennt von Berichten und anderen Katalogelementen verwalten, von denen es verwendet wird. Freigegebene Datasets können mit paginierten und mobilen Berichten verwendet werden, zusammen mit KPIs.

Sie können die Eigenschaften eines freigegebenen Datasets innerhalb des Webportals anzeigen und verwalten. Über das Webportal erhalten Sie Zugriff auf den Berichts-Generator, um freigegebene Datasets zu erstellen oder zu bearbeiten.

## <a name="create-a-shared-dataset"></a>Erstellen eines freigegebenen Datasets
  
Sie können Folgendes tun, um ein neues freigegebenes Dataset zu erstellen.  
  
1.  Wählen Sie in der Menüleiste „Neu“ aus.  
  
2.  Wählen Sie **Dataset**aus.  
  
    ![SSRS-Dataset-NeuesDataset](../reporting-services/media/ssrsdataset-newdataset.png)  
  
3.  Entweder wird jetzt der Berichts-Generator gestartet, oder Sie werden aufgefordert, ihn herunterzuladen.  
  
4.  Wählen Sie im Dialog **Neuer Bericht oder neues Dataset** eine Datenquellenverbindung aus, die für dieses Dataset verwendet werden soll. Möglicherweise ist es erforderlich, dass Sie an den Speicherort der freigegebenen Datenquelle navigieren.  
  
5.  Wählen Sie **Erstellen**aus.  
  
6.  Erstellen Sie Ihr Dataset, und wählen Sie dann das **Speichern** -Symbol in der oberen linken Ecke aus, um das Dataset zurück an den Berichtsserver zu speichern.  
  
## <a name="manage-an-existing-shared-dataset"></a>Verwalten eines vorhandenen freigegebenen Datasets
  
Sie können Sie Folgendes tun, um ein vorhandenes freigegebenes Dataset zu verwalten.  
  
> [!NOTE]
> Falls Sie das freigegebene Dataset nicht im Ordner sehen, stellen Sie sicher, dass Sie Datasets anzeigen. Sie können **Ansicht** aus der Menüleiste in der oberen rechten Ecke des Webportals auswählen. Stellen Sie sicher, dass **Datasets** aktiviert ist.  
  
1.  Wählen Sie die **mit den Auslassungszeichen (...)**  für das Dataset, die Sie verwalten möchten.  
  
    ![SSRS-Dataset-Auslassungspunkte](../reporting-services/media/ssrsdataset-ellipse.png)  
  
2.  Wählen Sie **Verwalten** aus, womit Sie auf den Bearbeitungsbildschirm gelangen.  
  
    ![SSRS-Dataset-Verwalten](../reporting-services/media/ssrsdataset-manage.png)  
  
## <a name="properties"></a>Eigenschaften
  
Im Eigenschaftenbildschirm können Sie den **Namen** und die **Beschreibung** des Datasets ändern. Sie können es auch **Löschen**, **Verschieben**, **Im Berichts-Generator bearbeiten**, **Herunterladen** oder **Ersetzen**.  
  
![SSRS-Dataset-Eigenschaften](../reporting-services/media/ssrsdataset-properties.png)  
  
## <a name="caching"></a>Caching
  
Wenn es um das Zwischenspeichern von Daten für ein Dataset geht, stehen Ihnen Optionen zur Verfügung. Sie beginnen mit einer einfachen Auswahl.  
  
1.  **Always run this report with the most recent data** (Diesen Bericht immer mit den neusten Daten ausführen), gibt wenn angefordert Abfragen an die Datenquelle aus.  
  
2.  **Cache copies of this report and use them when available** (Kopien dieses Berichts zwischenspeichern und wenn verfügbar verwenden), platzierte eine temporäre Kopie der Daten in einen Cache für die Verwendung mit Elementen, die dieses Dataset verwenden. Die Zwischenspeicherung erhöht in der Regel die Leistung, da die Daten aus dem Cache zurückgegeben werden und die Datasetabfrage nicht erneut ausgeführt werden muss.  
  
![SSRS-Dataset-Zwischenspeichern1](../reporting-services/media/ssrsdataset-caching1.png)  
  
Die Wahl von **Kopien dieses Berichts zwischenspeichern und wenn verfügbar verwenden** bieten Ihnen einige zusätzliche Optionen.  
  
![SSRS-Dataset-Zwischenspeichern2](../reporting-services/media/ssrsdataset-caching2.png)  
  
### <a name="cache-expiration"></a>Cacheablauf  
  
Sie können steuern, ob der Cache für das freigegebene Dataset nach einer bestimmten Zeitspanne ablaufen soll, oder ob Sie es bevorzugen würden, dies laut einem Zeitplan zu tun. Sie können einen freigegebenen Zeitplan verwenden  
  
![SSRS-Dataset-Zwischenspeichern3](../reporting-services/media/ssrsdataset-caching3.png)  
  
> [!NOTE]
> Das Festlegen einer Ablaufzeit aktualisiert nicht den Cache. Ohne einen Cacheaktualisierungsplan werden die Daten bei der nächsten Ausführung des Datasets aktualisiert.  
  
### <a name="cache-refresh-plans"></a>Cacheaktualisierungspläne  
  
Sie können Cacheaktualisierungspläne verwenden, um Zeitpläne für das Vorabladen des Caches mit temporären Kopien der Daten für ein freigegebenes Dataset zu erstellen. Ein Aktualisierungsplan enthält einen Zeitplan und bietet die Möglichkeit, Werte für Parameter anzugeben oder zu überschreiben. Sie können keine Werte für Parameter überschreiben, die als schreibgeschützt gekennzeichnet sind. Sie können mehr als einen Aktualisierungsplan erstellen und verwenden.   
  
Die Standardrollenzuweisungen, mit denen Sie freigegebene Datasets für Cacheaktualisierungspläne hinzufügen, löschen und ändern können, lauten „Inhalts-Manager“, „Meine Berichte“ und „Verleger“.  
  
Nachdem Sie die obenstehende Option zum Zwischenspeichern angewendet haben, können Sie einen Cacheaktualisierungsplan definieren. Wählen Sie den Link **Aktualisierungspläne verwalten** , der angezeigt wird, nachdem Sie die Cacheeinstellungen anwenden. Dadurch gelangen Sie auf die Seite „Cacheaktualisierungsplan“.   
  
Wählen Sie **Neuer Cacheaktualisierungsplan**, um einen neuen Cacheplan zu erstellen. Sie können einen Namen für den Plan eingeben und einen Zeitplan angeben. Falls das Dataset über definierte Parameter verfügt, werden Ihnen diese aufgelistet angezeigt, und es wird Ihnen möglich sein, Werte bereitzustellen, sofern sie nicht als schreibgeschützt gekennzeichnet sind.  
  
Sobald Sie fertig sind, können Sie **Cacheaktualisierungsplan erstellen**auswählen.  
  
![SSRS-Dataset-Zwischenspeichern4](../reporting-services/media/ssrsdataset-caching4.png)  
  
> [!NOTE]
> SQL Server-Agent muss ausgeführt werden, um einen Cacheaktualisierungsplan zu erstellen.  
  
Sie können gelistete Pläne **Bearbeiten** oder **Löschen** . Die Option **Neu aus vorhandenem** wird nur aktiviert, wenn genau ein Cacheaktualisierungsplan ausgewählt ist. Durch diese Option wird ein neuer Aktualisierungsplan erstellt, der vom ursprünglichen Plan kopiert wird. Die Seite Cacheaktualisierungsplan wird geöffnet und enthält bereits die Details des ausgewählten Plans. Anschließend können Sie die Optionen für den Aktualisierungsplan ändern und den Plan mit einer neuen Beschreibung speichern.  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
