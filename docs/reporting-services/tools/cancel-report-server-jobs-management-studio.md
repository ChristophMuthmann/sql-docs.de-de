---
title: Berichtsserveraufträge abbrechen (Management Studio) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d0ea49d4e9d399f5027f235bce8b895d063ed4e7
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="cancel-report-server-jobs-management-studio"></a>Berichtsserveraufträge abbrechen (Management Studio)
  Verwenden Sie das Dialogfeld **Berichtsserveraufträge abbrechen** , um ausgeführte Berichte anzuzeigen oder abzubrechen. Dieses Dialogfeld zeigt alle Aufträge an, die gerade auf dem Berichtsserver ausgeführt werden. Zwar können Sie gerade bearbeitete Aufträge nicht anhalten oder neu starten, jedoch können Sie alle oder einzelne Aufträge abbrechen, wenn ihr Abschluss zu lange dauert.  
  
 Sie können sowohl Benutzer- als auch Systemaufträge abbrechen.  
  
-   Als Benutzerauftrag wird ein Auftrag bezeichnet, der durch einen einzelnen Benutzer initiiert wird. Dazu zählt das Ausführen eines Berichts bei Bedarf, das manuelle Erstellen einer Momentaufnahme zum Berichtsverlauf oder das manuelle Erstellen einer Momentaufnahme zur Berichtsausführung. Ein ausgeführtes Standardabonnement wird ebenfalls als Benutzerauftrag bezeichnet.  
  
-   Als Systemauftrag wird ein Auftrag bezeichnet, der durch den Berichtsserver initiiert wird. Systemaufträge schließen die geplante Berichtsverarbeitung ein.  
  
 Öffnen Sie diese Seite, indem Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]starten und eine Verbindung mit einem Berichtsserver herstellen. Klicken Sie mit der rechten Maustaste auf **Aufträge**, und klicken Sie anschließend auf **Alle Aufträge abbrechen**. Sie können auch **Aufträge**öffnen und mit der rechten Maustaste auf einen auf dem Berichtsserver ausgeführten Auftrag klicken. Klicken Sie anschließend auf **Aufträge abbrechen**.  
  
 Vor dem Abbrechen eines Auftrags können Sie seine Eigenschaften anzeigen, um zu bestimmen, wann der Auftrag gestartet wurde. Weitere Informationen finden Sie unter [Auftragseigenschaften (Management Studio)](../../reporting-services/tools/job-properties-management-studio.md).  
  
> [!NOTE]  
>  Diese Funktion wird in [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services nicht unterstützt. Die Seite wird nicht angezeigt, wenn Sie [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]ausführen.  
  
## <a name="options"></a>Tastatur  
 **Name**  
 Zeigt den Berichtsnamen an. Abonnements werden durch ihre Beschreibung identifiziert.  
  
 **Typ**  
 Die gültigen Werte sind **Benutzer** und **System**.  
  
 **Startzeit**  
 Zeigt an, wann der Auftrag gestartet wurde.  
  
 **Benutzername**  
 Bei Aufträgen, die von einem Benutzer initiiert wurden, zeigt diese Spalte den Namen des Benutzers an.  
  
 **Status**  
 Zeigt den Status des Auftrags an. Gültige Werte sind **Neu** und **Wird ausgeführt**. Bei Beginn des Auftrags ist der Status immer **Neu** . Nach 60 Sekunden ändert sich der Status in **Wird ausgeführt**. Sie müssen die Seite aktualisieren, damit die Änderung übernommen wird.  
  
 **OK**  
 Brechen Sie einen einzelnen Auftrag oder mehrere Aufträge ab. Die Aufträge werden sofort abgebrochen und können nicht wiederaufgenommen werden. Wenn Sie versehentlich einen Auftrag abgebrochen haben, müssen sie den Bericht oder das Abonnement erneut anfordern, um einen neuen Auftrag zu starten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
