---
title: "Erstellen eines mobile Berichts im Registerkartenformat mithilfe von Drillthrough | Reporting Services – mobile Berichte | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Erstellen eines mobile Berichts im Registerkartenformat mithilfe von Drillthrough | Reporting Services – mobile Berichte
Erhalten Sie Informationen zum Erstellen eines mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Berichts, der wie ein Bericht im Registerkartenformat aussieht und sich entsprechend verhält, indem Sie Drillthrough und Parameter verwenden.

In diesem Bericht Verhalten sich z. B. Messgeräte am oberen Rand wie Registerkarten. Wenn Sie auf das Messgerät „Transport“ klicken, werden die Daten im restlichen Diagramm nach den Transportdaten gefiltert.

![06-mobile-Berichte-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

Im Hintergrund liegt tatsächlich ein Satz von fünf separaten Berichten, die jeweils einen anderen Parameter verwenden, der den Bericht filtert, um dem ausgewählten Messgerät am oberen Rand des Berichts zu entsprechen. 

In diesem Beispiel erstellen Sie zuerst alle fünf Berichte, danach legen Sie für jeden der fünf Berichte die anderen vier Messgeräte als Drillthroughs zu den anderen vier Berichten fest. 

Hier sehen Sie eine allgemeine Übersicht der Schritte.

1. Erstellen Sie einen Bericht „Umsatz“ mit fünf Messgeräten:
     - Sales
     - Transport
     - Treibstoff
     - Speicherung
     - Verschiedene Ausgaben
2. Machen Sie vier Kopien des Berichts, und nennen Sie sie: 
     - Transport
     - Treibstoff
     - Speicherung
     - Verschiedene Ausgaben
3.  Im Bericht „Umsatz“ legen Sie alle vier Messgeräte (bis auf das Messgerät „Umsatz“) als Drillthrough zu ihren entsprechenden Berichten fest.

4. Während Sie sich im Bericht „Umsatz“ befinden, stellen Sie die Eigenschaft „Akzent“ des Messgeräts „Umsatz“ als Kontrast zum restlichen Bericht ein, damit es sich abhebt.

5.  Jetzt legen Sie im Bericht „Transport“ das Messgerät „Umsatz“ als Drillthrough zum Bericht „Umsatz“ fest und die anderen drei Messgeräte als Drillthroughs zu ihren jeweiligen Berichten.

6. Während Sie sich im Bericht „Transport“ befinden, stellen Sie die Eigenschaft „Akzent“ des Messgeräts „Transport“ als Kontrast zum Rest des Berichts ein.

5. Wiederholen Sie diese Schritte für die Berichte „Treibstoff“, „Speicherung“ und „verschiedene Ausgaben“. 







  
