---
title: Arbeiten mit KPIs in Reporting Services | Microsoft Docs
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b451b1773d97d490c0021cdf8cfcfb14c07117b4
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="working-with-kpis-in-reporting-services"></a>Arbeiten mit KPIs in Reporting Services

[!INCLUDE[ssrs-appliesto-sql2016-preview](../includes/ssrs-appliesto-sql2016-preview.md)]

Ein Key Performance Indicator (KPI) ist ein sichtbarer Hinweis, der Auskunft über den Fortschritt im Hinblick auf das Erreichen eines Ziels gibt.  Key Performance Indicators sind wertvoll für Teams, Manager und Unternehmen, um schnell den bei messbaren Zielen erzielten Fortschritt zu evaluieren.   
  
Mit KPIs in SQL Server 2016 Reporting Services können Sie einfach Antworten für die folgenden Fragen visualisieren:  
  
-   Womit bin ich weit vorangekommen, oder womit hänge ich hinterher?  
  
-   Wie weit habe ich vorausgearbeitet, oder wie weit hänge ich hinterher?  
  
-   Was ist das Minimum, das ich abgeschlossen habe?  
  
## <a name="creating-a-dataset"></a>Erstellen eines Dataset  
Eine KPI wird nur die erste Zeile der Daten aus einem freigegebenen Dataset verwenden. Stellen Sie sicher, dass sich die Daten, die Sie verwenden möchten, in dieser ersten Zeile befinden. Um ein freigegebenes Dataset zu erstellen, können Sie entweder den Berichts-Generator oder SQL Server Data Tools verwenden.  
  
> **Hinweis**: Das Dataset muss sich nicht im selben Ordner wie die KPI befinden.  
  
## <a name="placement-of-kpis"></a>Platzierung von KPIs  
  
KPIs können in einem beliebigen Ordner auf Ihrem Berichtsserver erstellt werden.  Bevor Sie eine KPI erstellen, sollten Sie überlegen, wo der richtige Speicherort dafür wäre. Sie sollten sie in einem Ordner ablegen, der für Benutzer sichtbar ist. Gleichzeitig sollte der Ordner auch relevant für andere Berichte sowie KPIs in der Umgebung sein.  
  
## <a name="adding-a-kpi"></a>Hinzufügen einer KPI  
  
Nachdem Sie den Speicherort der KPI bestimmt haben, wechseln Sie zu dem Ordner, und wählen Sie **Neu** > **KPI** im oberen Menü aus.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
Dies zeigt Ihnen den Bildschirm **Neue KPI** an.  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Sie können entweder statische Werte zuweisen oder Daten aus einem freigegebenen Dataset verwenden. Wenn Sie eine neue KPI erstellen, wird diese mit zufälligen manuellen Daten aufgefüllt.  
  
|Feld|Description|  
|---|---|  
|Wertformat|  Wird verwendet, um das Format des angezeigten Werts zu ändern.|   
|Wert|Der für die KPI anzuzeigender Wert.|  
|Ziel|Wird als Vergleich mit einem numerischen Wert verwendet und als prozentuale Differenz angezeigt.|  
|Status|Zum Bestimmen der KPI-Kachelfarbe verwendete und durch Komma getrennte numerische Werte. Gültige Werte sind 1 (Grün), 0 (gelb) und-1 (Rot).|  
|Trendsatz|Für Diagrammvisualisierungen verwendete durch Komma getrennte numerische Werte. Dies kann auch für eine Spalte eines Dataset mit Werten festgelegt werden, die den Trend darstellen.|  
  
> **Warnung**: Bei der Verwendung des Wordwerts für das **Status** -Feld zur Entwurfszeit, sollten Sie den Zahlenwert verwenden, wenn Sie ein Dataset aktualisieren. Wenn Sie ein Dataset mit dem Wortwert anstelle des Zahlenwerts aktualisieren, könnten die KPIs auf Ihrem Server beschädigt werden.  
  
> **Hinweis:**: Die Felder **Wert**, **Ziel** und **Status** können nur einen Wert aus der ersten Zeile des Ergebnisses eines Datasets auswählen. Das Feld **Trendsatz** kann jedoch wählen, welche Spalte den Trend widerspiegelt.  
  
Um Daten aus einem freigegebenen Dataset zu verwenden, können Sie Folgendes tun.  
  
1.  Ändern Sie das Dropdownfeld des Felds von **Manuell festlegen**oder **Nicht festgelegt**auf **Datasetfeld**.  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2.  Wählen Sie die **mit den Auslassungszeichen (...)**  im Datenfeld. Hierdurch erscheint der Bildschirm **Wählen Sie ein Dataset** .  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3.  Wählen Sie das Dataset aus, das die Daten enthält, die Sie anzeigen möchten.  
  
4.  Wählen Sie das Feld aus, das Sie verwenden möchten. Wählen Sie **OK**.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5.  Ändern Sie das **Wertformat** , damit es mit dem Format Ihres Werts übereinstimmt. In diesem Beispiel ist der Wert einer Währung.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6.  Wählen Sie **Anwenden**aus.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)  
  
## <a name="removing-a-kpi"></a>Entfernen einer KPI  
  
Um eine KPI zu entfernen, können Sie Folgendes tun.  
  
1.  Wählen Sie die **mit den Auslassungszeichen (...)**  des KPIS, die Sie entfernen möchten. Wählen Sie **Verwalten**aus.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  Wählen Sie **Löschen**aus. Wählen Sie **Löschen** erneut im Bestätigungsdialogfeld aus.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>Aktualisieren einer KPI  
  
Um den KPI zu aktualisieren, müssen Sie das Zwischenspeichern für das freigegebene Dataset konfigurieren. Weitere Informationen zu cacheaktualisierungsplänen, finden Sie unter [arbeiten mit freigegebenen Datasets](../reporting-services/work-with-shared-datasets-web-portal.md).  
  
## <a name="next-steps"></a>Nächste Schritte
  
[Webportal](../reporting-services/web-portal-ssrs-native-mode.md)  
[Arbeiten mit freigegebenen Datasets](../reporting-services/work-with-shared-datasets-web-portal.md)

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
