---
title: Automatisches Generieren von anderen Attributwerten als Code (Master Data Services) | Microsoft-Dokumentation
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
ms.assetid: b82f6f81-6e9c-4918-9ea9-4ab5f5d11b15
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 2709d8389e92b9688e18fba0a055263fa67e33e7
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="automatically-generate-attribute-values-other-than-code-master-data-services"></a>Automatisches Generieren von anderen Attributwerten als Code (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie Werte für die Attributwerte einer Entität automatisch generieren, wenn Sie möchten, dass eine ganze Zahl jedes Mal automatisch als Wert zugewiesen werden soll, wenn Geschäftsregeln angewendet werden.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Ein numerisches Attribut muss vorhanden sein. Weitere Informationen finden Sie unter [Erstellen eines numerischen Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md).  
  
### <a name="to-automatically-generate-an-attribute-value"></a>So generieren Sie automatisch einen Attributwert  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie auf der Seite **Verwaltung von Geschäftsregeln** aus der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie aus der Liste **Entität** eine Entität aus.  
  
5.  Wählen Sie aus der Liste **Elementtyp** einen Typ des Elements aus, auf das die Geschäftsregel angewendet werden soll.  
  
6.  Behalten Sie in der Liste **Attribut** die Standardeinstellung **Alle**bei.  
  
7.  Klicken Sie auf **Geschäftsregel hinzufügen**.  
  
8.  Klicken Sie auf **Ausgewählte Geschäftsregel bearbeiten**.  
  
9. Erweitern Sie im Bereich **Komponenten** den Knoten **Aktionen** .  
  
10. Klicken Sie im Knoten "Standardwert" auf **entspricht standardmäßig generiertem Wert** , und ziehen Sie es auf die Beschriftung **Aktionen** des Bereichs **THEN** .  
  
11. Klicken Sie im Bereich **Attribute** auf das Attribut mit dem zu generierenden Wert, und ziehen Sie es in die Beschriftung **Attribut auswählen** des Bereichs **Aktion bearbeiten** .  
  
12. Geben Sie in den Feldern **Start bei** und **Erhöhen um** einen Wert ein. Wenn Elemente bereits vorhanden sind, wird der Wert auf Grundlage des höchsten vorhandenen Werts festgelegt. Wenn der höchste vorhandene Wert zum Beispiel 299 beträgt und Sie **Erhöhen um** auf **1**festgelegt haben, wird der Wert des nächsten Elements auf 300 festgelegt.  
  
13. Klicken Sie im Bereich **Aktion bearbeiten** auf **Element speichern**.  
  
14. Klicken Sie auf **Zurück**.  
  
15. Optional können Sie auf der Seite **Verwaltung von Geschäftsregeln** für die Zeile, die die Geschäftsregel enthält, auf eine Zelle in den Spalten **Name**, **Beschreibung**oder **Benachrichtigung** doppelklicken, um den Wert zu aktualisieren.  
  
16. Klicken Sie auf **Geschäftsregeln veröffentlichen**.  
  
17. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Der Status der Regel ändert sich zu **Aktiv**.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   [Überprüfen von bestimmten Elementen auf Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
-   [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Automatische Codeerstellung &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Überprüfung &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
  

