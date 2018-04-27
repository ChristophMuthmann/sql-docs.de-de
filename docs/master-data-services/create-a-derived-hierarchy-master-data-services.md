---
title: Erstellen einer abgeleiteten Hierarchie (Master Data Services) | Microsoft-Dokumentation
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
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d7cfeb6c25577182f27e5dbc37ec0a9fc31cdc2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-derived-hierarchy-master-data-services"></a>Erstellen einer abgeleiteten Hierarchie (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine abgeleitete Hierarchie, wenn Sie eine ebenenbasierte Hierarchie möchten, die sicherstellt, dass sich die Elemente auf der richtigen Ebene befinden. Abgeleitete Hierarchien basieren auf den domänenbasierten Attributbeziehungen, die in einem Modell vorhanden sind.  
  
> [!NOTE]  
>  Wenn ein domänenbasierter Attributwert für ein Element nicht vorhanden ist, ist das Element nicht in der abgeleiteten Hierarchie enthalten. Gehen Sie auf die Seite [Erfordern von Attributwerten &#40;Master Data Services&#41;](../master-data-services/require-attribute-values-master-data-services.md), um einen domänenbasierten Attributwert für alle Mitglieder anzufordern.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-create-a-derived-hierarchy"></a>So erstellen Sie eine abgeleitete Hierarchie  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Abgeleitete Hierarchien**.  
  
3.  Wählen Sie auf der Seite **Verwaltung abgeleiteter Hierarchien** aus der Liste **Modell** ein Modell aus.  
  
4.  Klicken Sie auf **Hinzufügen**.  
  
5.  Geben Sie auf der Seite **Abgeleitete Hierarchie hinzufügen** im Feld **Name der abgeleiteten Hierarchie** einen Namen für die Hierarchie ein.  
  
    > [!TIP]  
    >  Verwenden Sie einen Namen, der die Ebenen in der Hierarchie beschreibt, z.B. **Produkt-zu-Unterkategorie-zu-Kategorie**.  
  
6.  Klicken Sie auf **Abgeleitete Hierarchie speichern**.  
  
7.  Klicken Sie auf der Seite **Abgeleitete Hierarchie bearbeiten** im Bereich **Verfügbare Entitäten und Hierarchien** auf eine Entität oder eine Hierarchie, und ziehen Sie diese in den Bereich **Aktuelle Ebenen** zu **Übergeordnetes Element hier ablegen** .  
  
8.  Ziehen Sie Entitäten oder Hierarchien in diesen Bereich, bis die Hierarchie vollständig ist.  
  
9. Klicken Sie auf **Zurück**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Abgeleitete Hierarchien &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)   
 [Abgeleitete Hierarchien mit expliziten Abschlüssen &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Domänenbasierte Attribute &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)  
  
  
