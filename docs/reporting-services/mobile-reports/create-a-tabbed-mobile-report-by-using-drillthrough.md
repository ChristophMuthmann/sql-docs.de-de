---
title: Erstellen eines mobilen Berichts im Registerkartenformat mithilfe eines Drillthroughs | Mobile Berichte von Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9824bbc98ac886f8836b73ae8ca49cbdce93afaa
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>Erstellen eines mobilen Berichts im Registerkartenformat mithilfe eines Drillthroughs
Erhalten Sie Informationen zum Erstellen eines mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichts, der wie ein Bericht im Registerkartenformat aussieht und sich entsprechend verhält, indem Sie Drillthrough und Parameter verwenden.

In diesem Bericht Verhalten sich z. B. Messgeräte am oberen Rand wie Registerkarten. Wenn Sie auf das Messgerät „Transport“ klicken, werden die Daten im restlichen Diagramm nach den Transportdaten gefiltert.

![06-mobile-Berichte-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

Im Hintergrund liegt tatsächlich ein Satz von fünf separaten Berichten, die jeweils einen anderen Parameter verwenden, der den Bericht filtert, um dem ausgewählten Messgerät am oberen Rand des Berichts zu entsprechen. Erstellen Sie zunächst alle fünf Berichte, und legen Sie anschließend für jeden der Berichte die jeweils anderen vier Messgeräte als Drillthroughs für die anderen vier Berichte fest.

In diesem Beispiel werden folgende Schritte ausgeführt:

## <a name="create-the-basic-report"></a>Erstellen des einfachen Berichts

1. Erstellen Sie einen Bericht „Umsatz“ mit fünf Messgeräten:

    * Sales
    * Transport
    * Treibstoff
    * Speicherung
    * Verschiedene Ausgaben

   ![01-Umsatz-Publisher-für-mobile-Berichte](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. Legen Sie für das Messgerät „Sales“ (Umsatz) **Accent** (Akzent) **On** (An) fest, damit es einen Kontrast zu dem Rest des Berichts bildet – in diesem Fall weiß auf schwarz.

    ![01a-Umsatz-Akzent-Publisher-für-mobile-Berichte](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. Speichern Sie ihn auf einem [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Berichtsserver.

## <a name="make-copies-of-the-report"></a>Erstellen von Kopien des Berichts

1. Erstellen Sie vier Kopien des Umsatzberichts, und benennen Sie diese: 

    * Transport
    * Treibstoff
    * Speicherung
    * Verschiedene Ausgaben

3. Speichern Sie die Berichte auf dem [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Berichtsserver.

## <a name="set-the-gauge-as-a-drillthrough"></a>Festlegen des Messgeräts als Drillthrough

In diesem Abschnitt legen Sie jedes Messgerät (im Gegensatz zu dem Messgerät „Umsatz“) als Dillthrough zu dem jeweiligen Bericht fest.

1. Klicken Sie im Umsatzbericht auf das Messgerät „Transportation“ (Transport).

    ![02-Umsatz-Drilltrough-erstellen-Publisher-für-mobile-Berichte](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. Klicken Sie zunächst auf die Registerkarte **Layout** und anschließend im Bereich **Eigenschaften visueller Elemente** auf **Ziel für Drillthrough**.

3. Klicken Sie auf **Mobilgerätebericht**.

4. Navigieren Sie zu dem Bericht, der als Ziel für den Drillthrough dienen soll, und wählen Sie ihn aus; in diesem Fall „Financials – Transportation“ (Finanzinformationen – Transport).

    ![03-Verleger-von-mobilen-Verkaufsberichten-zum-Auswählen-von-Dashboards](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. Klicken Sie unter **Zielbericht konfigurieren** auf den Parameter zum Filtern des Berichts und anschließend auf **Übernehmen**.

   ![04-Verleger-von-mobilen-Verkaufsberichten-zum-Übernehmen-von-Parametern](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. Führen Sie diese Schritte für die anderen Messgeräte im Umsatzbericht erneut aus. 

## <a name="set-the-gauges-for-the-other-reports"></a>Festlegen der Messgeräte für die anderen Berichte

1.  Öffnen Sie den Bericht „Transport“, legen Sie das Messgerät „Umsatz“ als Drillthrough zum Umsatzbericht und die anderen drei Messgeräte als Drillthroughs zu ihren jeweiligen Berichten fest.

2. Legen Sie im Bericht „Transport“ die Eigenschaft **Akzent** für das Messgerät „Transport“ auf **On** (An) fest, um einen Kontrast zum Rest des Berichts zu bilden.

3. Wiederholen Sie diese Schritte für die Berichte „Fuel“ (Treibstoff), „Storage“ (Laderaum) und „Misc Expenses“ (Sonst. Ausgaben). 

## <a name="view-the-report-in-the-web-portal"></a>Abrufen des Berichts im Webportal

1. Gehen Sie zum [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Berichtsserver, und öffnen Sie einen der Berichte. 

2. Beachten Sie, dass jedes der Messgeräte ein Drillthroughsymbol in der oberen rechten Ecke aufweist.

    ![Web-Viewer-Drillthroughsymbol-Generator-Mobilgeräteberichte](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. Klicken Sie auf eins der Messgeräte, um zu dem gefilterten Bericht zu den Daten dieses Messgeräts zu gelangen.

   ![06-mobile-Berichte-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>Siehe auch
    
* [Add parameters to a mobile report (Hinzufügen von Parametern zu einem mobilen Bericht)](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Add drillthrough from a mobile report to other mobile reports or URLs (Drillthrough zu anderen mobilen Berichten oder URLs aus einem mobilen Bericht hinzufügen)](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  

