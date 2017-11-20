---
title: Elementrevisionsverlauf (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 113069c5-12e6-48ec-b443-b42e14f77308
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 665a5978f516520c397bdbfe01be84ab93df028c
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="member-revision-history-master-data-services"></a>Elementrevisionsverlauf (Master Data Services)
  Ein Elementrevisionsverlauf wird jedes Mal aufgezeichnet, wenn ein Element geändert wird, falls der Protokolltyp der Entitätsbuchung „Member“ ist.  
  
 Weitere Informationen zu Transaktionsprotokolltypen finden Sie unter [Ändern des Transaktionsprotokolltyps von Entitäten &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md).  
  
 Elementrevisionsverläufe werden aufgezeichnet, wenn die folgenden Änderungen auftreten.  
  
-   Elemente werden erstellt, gelöscht, erneut aktiviert oder bereinigt.  
  
-   Attributwerte werden geändert.  
  
-   Elemente werden in eine Hierarchie oder Sammlung verschoben.  
  
## <a name="view-and-manage-revision-history-by-entity"></a>Anzeigen und Verwalten des Revisionsverlaufs je Entität  
 Im Funktionsbereich des Explorers können Sie die Revision für alle Elemente in der Entität anzeigen. Wenn Sie über Aktualisierungsberechtigungen verfügen, können Sie das Element auf eine frühere Version zurücksetzen.  
  
 **So zeigen Sie den Revisionsverlauf an und verwalten ihn**  
  
1.  Wählen Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]das Modell und die Version und klicken Sie anschließend auf **Explorer**.  
  
2.  Wählen Sie die Entität aus dem Menü **Entitäten** aus.  
  
3.  Klicken Sie auf **Verlauf anzeigen** , um alle Verlaufsdaten der Entität anzuzeigen.  
  
4.  Klicken Sie auf **Filter** , um die Daten zu filtern.  
  
5.  Klicken Sie auf die Spaltenüberschrift, um die Daten zu sortieren.  
  
6.  Wenn Sie über Aktualisierungsberechtigungen verfügen, klicken Sie auf **Element wiederherstellen** , um die gewählte Version zurückzusetzen.  
  
## <a name="view-and-manage-revision-history-by-member"></a>Anzeigen und Verwalten des Revisionsverlaufs durch Element  
 Im Funktionsbereich des Explorers können Sie die Überarbeitungen für ein Element anzeigen, wenn Sie über Leseberechtigungen für das Element verfügen. Wenn Sie über Aktualisierungsberechtigungen verfügen, können Sie das Element auf eine frühere Überarbeitung zurücksetzen oder Anmerkungen zur Überarbeitung hinzufügen.  
  
1.  Wählen Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]das Modell und die Version und klicken Sie anschließend auf **Explorer**.  
  
2.  Wählen Sie die Entität aus dem Menü **Entitäten** aus.  
  
3.  Wählen Sie das Element aus.  
  
4.  Klicken Sie auf **Verlauf anzeigen** im rechten Bereich.  
  
## <a name="log-retention-setting"></a>Einstellung für Protokollbeibehaltung  
 Sie können konfigurieren, wie lange Verlaufsdaten beibehalten werden, indem Sie die Eigenschaft **Protokollaufbewahrung in Tagen[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] in den Systemeinstellungen für die** -Datenbank festlegen, und durch Festlegen von **Protokollaufbewahrung in Tagen**, wenn Sie ein Modell erstellen oder bearbeiten.  
  
## <a name="related-task"></a>Verwandte Aufgabe  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Zurücksetzen des Elementrevisionsverlaufs|[Zurücksetzen des Elementrevisionsverlaufs &#40;Master Data Services&#41;](../master-data-services/rollback-member-revision-history-master-data-services.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)  
  
  

