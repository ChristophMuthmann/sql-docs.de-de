---
title: "Einschränken des Berichtsverlaufs (Berichts-Manager) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e1925f7527202ea251a6949a18e2f03af4f5952
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

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
  
4.  Wählen Sie die Optionen für Ihren Bericht aus, und klicken Sie auf **Anwenden**. Weitere Informationen zu den einzelnen Optionen finden Sie unter [Momentaufnahmeoptionen &#40;Eigenschaftenseite, Berichts-Manager&#41;](http://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen einer Momentaufnahme zum Berichtsverlauf &#40;Berichts-Manager&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
