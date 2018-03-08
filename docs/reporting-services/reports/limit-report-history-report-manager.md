---
title: "Einschränken des Berichtsverlaufs (Berichts-Manager) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: "36"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d3ad60e360d2144bd80b8243dd154941d9072bae
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="limit-report-history-report-manager"></a>Einschränken des Berichtsverlaufs (Berichts-Manager)
  Der Berichtsverlauf stellt eine Auflistung von Berichtsmomentaufnahmen dar, die Sie im Laufe der Zeit erstellen. Sie können den Berichtsverlauf nach Bedarf erstellen oder aber anhand eines Zeitplans festlegen, wie oft eine Momentaufnahme erstellt und dem Berichtsverlauf hinzugefügt wird.  
  
 Der Berichtsverlauf wird in der Berichtsserverdatenbank gespeichert. Wenn Berichtsmomentaufnahmen eine große Datenmenge enthalten, können Sie den Berichtsverlauf einschränken, um die Auswirkungen der Beibehaltung der Momentaufnahmen auf die Datenbankgröße zu minimieren.  
  
### <a name="to-configure-report-history-for-a-report-server"></a>So konfigurieren Sie den Berichtsverlauf für einen Berichtsserver  
  
1.  Klicken Sie im Berichts-Manager auf der globalen Symbolleiste auf **Siteeinstellungen** .  
  
2.  Wählen Sie **Beliebig viele Momentaufnahmen im Berichtsverlauf speichern** aus, wenn Sie alle Berichtsverläufe unbegrenzt lange aufbewahren möchten. Wählen Sie andernfalls **Max. Anzahl von Kopien des Berichtsverlaufs** aus, um die maximale Anzahl von Momentaufnahmen anzugeben, die für einen bestimmten Bericht aufbewahrt werden können.  
  
3.  Klicken Sie auf **Anwenden**.  
  
### <a name="to-configure-report-history-for-a-specific-report"></a>So konfigurieren Sie den Berichtsverlauf für einen bestimmten Bericht  
  
1.  Navigieren Sie im Berichts-Manager zu dem Bericht, dessen Verlauf Sie konfigurieren möchten, und öffnen Sie ihn, indem Sie auf ihn klicken.  
  
2.  Klicken Sie auf die Registerkarte **Eigenschaften** .  
  
3.  Klicken Sie auf die Registerkarte **Verlauf** .  
  
4.  Wählen Sie die Optionen für Ihren Bericht aus, und klicken Sie auf **Anwenden**. Weitere Informationen zu den einzelnen Optionen finden Sie unter [Momentaufnahmeoptionen Eigenschaftenseite (Berichts-Manager)](http://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hinzufügen einer Momentaufnahme zum Berichtsverlauf &#40;Berichts-Manager&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Berichts-Manager (einheitlicher SSRS-Modus)](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
