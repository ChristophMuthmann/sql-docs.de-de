---
title: Auftragseigenschaften (Management Studio) | Microsoft-Dokumentation
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
f1_keywords: sql13.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 83d8aa2129ec916241436e356d47da56fc0ef055
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="job-properties-management-studio"></a>Auftragseigenschaften (Management Studio)
  Verwenden Sie das Fenster **Auftragseigenschaften** , um Informationen zu einem ausgeführten Bericht oder Abonnement anzuzeigen, bevor Sie den Vorgang abbrechen.  
  
 Starten Sie, um diese Seite zu öffnen, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], stellen Sie eine Verbindung mit einem Berichtsserver her, und öffnen Sie den Ordner **Aufträge** . Klicken Sie mit der rechten Maustaste auf einen gerade ausgeführten Auftrag, und klicken Sie dann auf **Eigenschaften**.  
  
> [!NOTE]  
>  Diese Funktion wird in [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services nicht unterstützt. Die Seite wird nicht angezeigt, wenn Sie [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]ausführen.  
  
## <a name="tasks"></a>Aufgaben  
 Bevor Sie Informationen zu einem Auftrag anzeigen können, müssen Sie die Seite aktualisieren, damit die Informationen über die gerade auf dem Berichtsserver ausgeführten Aufträge abgerufen werden:  
  
1.  Öffnen Sie den Berichtsserverordner.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Aufträge**, und klicken Sie dann auf **Aktualisieren**.  
  
3.  Wird ein Auftrag aufgeführt, dann klicken Sie mit der rechten Maustaste auf den Auftrag, und klicken Sie anschließend auf **Eigenschaften**.  
  
## <a name="options"></a>enthalten  
 **Auftrags-ID**  
 Dem Auftrag wird während seiner Verarbeitung ein GUID zugewiesen. Dieser Zufallswert wird jedes Mal generiert, wenn ein Bericht oder Abonnement ausgeführt wird.  
  
 **Auftragsstatus**  
 Gültige Werte sind **Neu** und **Wird ausgeführt**. Bei Beginn des Auftrags ist der Status immer **Neu** . Nach 60 Sekunden ändert sich der Status in **Wird ausgeführt**. Sie müssen die Seite aktualisieren, damit die Änderung übernommen wird.  
  
 **Auftragstyp**  
 Die gültigen Werte sind **Benutzer** und **System**. Als Benutzerauftrag wird ein Auftrag bezeichnet, der durch einen einzelnen Benutzer initiiert wird. Dazu zählt das Ausführen eines Berichts bei Bedarf, die manuelle Generierung einer Momentaufnahme zum Berichtsverlauf oder das manuelle Erstellen einer Momentaufnahme zur Berichtsausführung. Ein ausgeführtes Standardabonnement wird ebenfalls als Benutzerauftrag bezeichnet. Als Systemauftrag wird ein Auftrag bezeichnet, der durch den Berichtsserver initiiert wird. Systemaufträge schließen die Berichtsverarbeitung ein, die von einem Zeitplan ausgelöst wird.  
  
 **Auftragsaktion**  
 Für Berichte zeigt diese Spalte die ausgeführten Berichtsausführungsprozesse an. Dieser Wert ist immer **Rendern**.  
  
 **Auftragsbeschreibung**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt standardmäßig keine Auftragsbeschreibungen bereit.  
  
 **Servername**  
 Zeigt den Namen des Berichtsservers an, der den Auftrag verarbeitet. Wenn Sie eine Bereitstellung für horizontales Skalieren konfiguriert haben, zeigt dieser Wert an, welcher Server den Auftrag verarbeitet.  
  
 **Berichtsname**  
 Zeigt den Berichtsnamen an. Abonnements werden durch ihre Beschreibung identifiziert.  
  
 **Berichtspfad**  
 Zeigt den Pfad des Berichts in der Ordnerhierarchie des Berichtsservers an.  
  
 **Startzeit**  
 Zeigt den Zeitpunkt des Prozessstarts an.  
  
 **Benutzername**  
 Für Prozesse, die durch einen Benutzer initiiert wurden, zeigt diese Spalte den Namen des Benutzers an. Bei Systemaufträgen ist dies der Name des Berichtsservers.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
