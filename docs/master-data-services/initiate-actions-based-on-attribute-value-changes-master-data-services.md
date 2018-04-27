---
title: Initiieren von Aktionen auf der Grundlage von Attributwertänderungen (Master Data Services) | Microsoft-Dokumentation
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
helpviewer_keywords:
- business rules [Master Data Services], tracking attribute changes
- change tracking groups [Master Data Services], initiating actions
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79ab82752842176e632bd6960b5f445bcb581702
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="initiate-actions-based-on-attribute-value-changes-master-data-services"></a>Initiieren von Aktionen auf der Grundlage von Attributwertänderungen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Geschäftsregel, um Aktionen auf der Grundlage von Änderungen an Attributwerten zu initiieren. Wenn beispielsweise ein bestimmter Attributwert geändert wird, können Sie einen Wert ändern, eine Benachrichtigung, senden oder einen externen Workflow starten.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Die Attribute müssen in einer Änderungsnachverfolgungsgruppe sein. Weitere Informationen finden Sie unter [Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) .  
  
### <a name="to-create-a-business-rule-to-initiate-actions-based-on-attribute-value-changes"></a>So erstellen Sie eine Geschäftsregel, um Aktionen auf der Grundlage von Änderungen an Attributwerten zu initiieren  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie auf der Seite **Verwaltung von Geschäftsregeln** aus der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie aus der Liste **Entität** eine Entität aus.  
  
5.  Wählen Sie aus der Liste **Elementtyp** einen Typ des Elements aus, auf das die Geschäftsregel angewendet werden soll.  
  
6.  Wählen Sie aus der Liste **Attribut** ein Attribut aus, oder behalten Sie die Standardeinstellung **Alle**bei.  
  
7.  Klicken Sie auf **Geschäftsregel hinzufügen**.  
  
8.  Klicken Sie auf **Ausgewählte Geschäftsregel bearbeiten**.  
  
9. Erweitern Sie im Bereich **Komponenten** den Knoten **Bedingungen** .  
  
10. Ziehen Sie unter dem Knoten **Wertvergleich** **Wurde geändert in** zur Bezeichnung **Bedingungen** des Bereichs **IF** .  
  
11. Geben Sie im Bereich **Bedingung bearbeiten** im Feld **Änderungsnachverfolgungsgruppe** die Nummer der Änderungsnachverfolgungsgruppe ein, die Sie als Teil der erforderlichen Komponenten zugewiesen haben.  
  
12. Klicken Sie im Bereich **Bedingung bearbeiten** auf **Element speichern**.  
  
13. Erweitern Sie im Bereich **Komponenten** den Knoten **Aktionen** .  
  
14. Klicken Sie auf eine Aktion, und ziehen Sie sie auf die Bezeichnung **Aktion** des Bereichs **THEN** .  
  
15. Klicken Sie im Bereich **Attribute** auf ein Attribut, und ziehen Sie es im Bereich **Aktion bearbeiten** auf die Bezeichnung **Attribut auswählen** .  
  
16. Vervollständigen Sie im Bereich **Aktion bearbeiten** alle Pflichtfelder.  
  
17. Klicken Sie im Bereich **Aktion bearbeiten** auf **Element speichern**.  
  
18. Klicken Sie auf **Zurück**.  
  
19. Optional können Sie auf der Seite **Verwaltung von Geschäftsregeln** für die Zeile, die die Geschäftsregel enthält, auf eine Zelle in den Spalten **Name**, **Beschreibung**oder **Benachrichtigung** doppelklicken, um den Wert zu aktualisieren.  
  
    > [!NOTE]  
    >  Benachrichtigungen werden nur für Regeln gesendet, die eine Überprüfungsaktion einschließen.  
  
20. Klicken Sie auf **Geschäftsregeln veröffentlichen**.  
  
21. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Der Status der Regel ändert sich zu **Aktiv**.  
  
## <a name="next-steps"></a>Next Steps  
  
-   Führen Sie zum Anwenden von Geschäftsregeln auf Daten eine der folgenden Prozeduren aus:  
  
    -   [Überprüfen von bestimmten Elementen auf Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
