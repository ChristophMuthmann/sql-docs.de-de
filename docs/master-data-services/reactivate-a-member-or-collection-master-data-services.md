---
title: Reaktivieren eines Elements oder einer Auflistung (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], reactivating
- consolidated members [Master Data Services], reactivating
- reactivating members [Master Data Services]
- members [Master Data Services], reactivating
- reactivating collections [Master Data Services]
- leaf members [Master Data Services], reactivating
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d71a78670995d22c03d24e0be9bb4df09c0ac6e
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="reactivate-a-member-or-collection-master-data-services"></a>Reaktivieren eines Elements oder einer Auflistung (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie ein Element erneut aktivieren, auf das Folgendes zutraf:  
  
-   Es wurde per Stagingprozess deaktiviert.  
  
-   Es wurde in MDS- [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]gelöscht.  
  
-   Es wurde in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung gelöscht.  
  
 Wenn Sie ein Element erneut aktivieren, werden dessen Attribute und Mitgliedschaften in Hierarchien und Auflistungen wiederhergestellt.  
  
 Sie können auch Auflistungen erneut aktivieren. In diesem Fall werden die Attribute der Auflistung und die Elemente, die zur Auflistung gehören, wiederhergestellt.  
  
 Wenn eine Auflistung oder ein Element erneut aktiviert wird, werden alle vorherigen Transaktionen wiederhergestellt.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]müssen Sie über die Berechtigung für den Funktionsbereich **Versionsverwaltung** verfügen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-reactivate-a-member-or-collection"></a>So reaktivieren Sie ein Element oder eine Auflistung  
  
1.  Klicken Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite auf **Versionsverwaltung**.  
  
2.  Klicken Sie in der Menüleiste auf **Transaktionen**.  
  
3.  Wählen Sie auf der Seite **Transaktionen** in der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
5.  Klicken Sie im Bereich **Transaktionen** auf die Zeile für das Element oder die Auflistung, das bzw. die Sie erneut aktivieren möchten. Für diese Zeile sollte **Aktiv** in der Spalte **Vorheriger Wert** und **Deaktiviert** in der Spalte **Neuer Wert** angezeigt werden.  
  
6.  Klicken Sie auf **Transaktion umkehren**.  
  
7.  Klicken Sie im Bestätigungsdialogfeld auf **OK**. Eine neue Transaktion wird hinzugefügt, und in der Spalte **Neuer Wert** wird **Aktiv** angezeigt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Löschen eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  
