---
title: Erstellen Sie einen im Registerkartenformat mobilen Bericht mithilfe von Drillthrough | Reporting Services-mobile-Berichte | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6554f808c19540d2a3b7cbe3fdf4e86c5fe7a357
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>Erstellen Sie einen im Registerkartenformat mobilen Bericht mithilfe von drillthrough
Erhalten Sie Informationen zum Erstellen eines mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichts, der wie ein Bericht im Registerkartenformat aussieht und sich entsprechend verhält, indem Sie Drillthrough und Parameter verwenden.

In diesem Bericht Verhalten sich z. B. Messgeräte am oberen Rand wie Registerkarten. Wenn Sie auf das Messgerät „Transport“ klicken, werden die Daten im restlichen Diagramm nach den Transportdaten gefiltert.

![06-mobile-Berichte-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

Im Hintergrund liegt tatsächlich ein Satz von fünf separaten Berichten, die jeweils einen anderen Parameter verwenden, der den Bericht filtert, um dem ausgewählten Messgerät am oberen Rand des Berichts zu entsprechen. Erstellen Sie zuerst alle fünf Berichte, und jeder der fünf Berichte, nehmen Sie die anderen vier Monitore in Drillthroughs für die anderen vier Berichte.

Es folgen die Schritte in diesem Beispiel.

## <a name="create-the-basic-report"></a>Erstellen eines einfachen Berichts

1. Erstellen Sie einen Bericht „Umsatz“ mit fünf Messgeräten:

    * Sales
    * Transport
    * Treibstoff
    * Speicherung
    * Verschiedene Ausgaben

   ![01 – Sales –--Publisher für Mobile Berichte](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. Festgelegt **Akzent** auf **auf** für das Messgerät Sales daher es wird im Gegensatz dazu der Rest des Berichts – in diesem Fall weiß auf Schwarz.

    ![01a-Sales-ACCENT-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. Speichern Sie es ein [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Berichtsserver.

## <a name="make-copies-of-the-report"></a>Erstellen Sie Kopien des Berichts

1. Erstellen Sie vier Kopien der Sales-Bericht, und nennen Sie diese: 

    * Transport
    * Treibstoff
    * Speicherung
    * Verschiedene Ausgaben

3. Speichern sie die [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Berichtsserver.

## <a name="set-the-gauge-as-a-drillthrough"></a>Legen Sie das Messgerät als ein drillthrough

In diesem Abschnitt werden die jedes Messgeräts (mit Ausnahme der Monitor "Sales") als einen Drillthrough zu den jeweiligen Bericht festlegen.

1. Wählen Sie in der Sales-Bericht den Monitor "Transport" ein.

    ![02-Sales-Create-Drillthrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. Mit der **Layout** Registerkarte ausgewählt, in der **Eigenschaften visueller Elemente** auf **Drillthrough Ziel**.

3. Wählen Sie **mobilen Bericht**.

4. Navigieren Sie zu, und wählen Sie den Bericht, die das Ziel für den Drillthrough – in diesem Fall werden "Finanz - Transport."

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. In **konfigurieren Zielbericht**, wählen Sie den Parameter, um den Bericht filtern, und wählen **übernehmen**.

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. Wiederholen Sie diese Schritte für jeden der Monitore in der Sales-Bericht aus. 

## <a name="set-the-gauges-for-the-other-reports"></a>Legen Sie die Monitore für die anderen Berichte

1.  Öffnen Sie den Transport-Bericht, den Monitor "Sales" festgelegt werden, da ein Drillthrough für die Sales-Bericht und die anderen drei als Drillthroughs ihren jeweiligen Berichten Messgeräte.

2. Immer noch im Bericht Transport festgelegt **Akzent** für der Zeitachse Transportation **auf**, Vergleiche mit der der Rest des Berichts.

3. Wiederholen Sie diese Schritte für die Berichte Treibstoff, Speicher- und sonstige Ausgaben. 

## <a name="view-the-report-in-the-web-portal"></a>Zeigt den Bericht im Web-portal

1. Wechseln Sie zu der [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Berichtsserver und einen Bericht zu öffnen. 

2. Beachten Sie, dass jede der Monitore ein Drillthrough-Symbol in der oberen rechten Ecke.

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. Wählen Sie eine der Monitore, um den Bericht auf Daten des Messgeräts gefiltert aufzurufen.

   ![06-mobile-Berichte-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>Siehe auch
    
* [Hinzufügen von Parametern zu einem mobilen Bericht](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Drillthrough zu anderen mobilen Berichten oder URLs aus einem mobilen Bericht hinzufügen](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  


