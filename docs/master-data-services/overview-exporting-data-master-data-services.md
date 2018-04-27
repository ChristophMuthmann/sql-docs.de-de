---
title: 'Übersicht: Exportieren von Daten (Master Data Services) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
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
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
caps.latest.revision: 12
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77a7bb3d50b30dabff3346604496d7e42392f154
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="overview-exporting-data-master-data-services"></a>Übersicht: Exportieren von Daten (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Artikel werden die Abonnementsichtformate vorgestellt und erläutert, wann die Sichten aufgrund von Änderungen an Modellobjekten bearbeitet werden müssen.  
  
 Sie werden eine Abonnementsicht erstellen, um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Daten in ein abonnierendes System wie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]zu exportieren. Sie nutzen das abonnierende System dazu, die Daten in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank anzuzeigen.  Informationen zum Erstellen der Abonnementsicht finden Sie unter [Erstellen einer Abonnementsicht zum Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
 Weitere Informationen zu Sichten finden Sie unter [Sichten](../relational-databases/views/views.md).  
  
## <a name="subscription-view-formats"></a>Abonnementsichtformate  
 Wenn Sie eine Sicht in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]erstellen, steht Ihnen eine Reihe von Standardsichtformaten in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] zur Auswahl. Mithilfe dieser Formate können Sie Sichten mit folgendem Inhalt erstellen:  
  
-   Alle Blattelemente und deren Attribute  
  
-   Alle konsolidierten Elemente und deren Attribute  
  
-   Alle Auflistungen und deren Attribute  
  
-   Die Elemente, die der Auflistung explizit hinzugefügt wurden  
  
-   Elemente in einer abgeleiteten Hierarchie in einem Format mit über- und untergeordneten Elementen oder Ebenen  
  
-   Elemente in allen expliziten Hierarchien für eine Entität in einem Format mit über- und untergeordneten Elementen oder Ebenen  
  
## <a name="subscription-views-can-become-out-of-date"></a>Abonnementsichten können ihre Aktualität verlieren  
 Nachdem Sie für eine Entität oder eine Hierarchie eine Abonnementsicht erstellt haben, werden Änderungen an den zugeordneten Modellobjekten nicht automatisch in der Sicht widergespiegelt. Sie müssen eine Abonnementsicht in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ggf. erneut generieren, um Änderungen an den Modellobjekten widerzuspiegeln. Die Spalte **Geändert** auf der Seite **Exportieren** wird bei einer Änderung der Modellobjekte in **True** geändert. Der Wert**True** gibt an, dass Sie die Abonnementsicht bearbeiten und speichern sollten, um die Sicht erneut zu generieren.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie eine Abonnementsicht der Masterdaten.|[Erstellen einer Abonnementsicht zum Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Löschen Sie eine vorhandene Abonnementsicht.|[Löschen einer Abonnementsicht &#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Abonnementsichtformate &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [Sichten](../relational-databases/views/views.md)  
  
  
