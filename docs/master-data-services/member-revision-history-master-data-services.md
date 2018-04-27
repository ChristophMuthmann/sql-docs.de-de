---
title: Elementrevisionsverlauf (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 113069c5-12e6-48ec-b443-b42e14f77308
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b241a2819c61b4c671c06d5622b9e30ed3f51f2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="member-revision-history-master-data-services"></a>Elementrevisionsverlauf (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)  
  
  
