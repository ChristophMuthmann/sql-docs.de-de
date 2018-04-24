---
title: Umkehren einer Transaktion (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
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
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e7a5e145d8172480eb13fdffdc4682651383478
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="reverse-a-transaction-master-data-services"></a>Umkehren einer Transaktion (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine Transaktion umkehren, wenn eine Aktion rückgängig gemacht werden muss. Beispiele für Transaktionen sind Attributwertänderungen, Hierarchieverschiebungen oder Elementlöschungen. Dieses Thema gilt für Transaktionen von Entitäten mit dem Transaktionsprotokolltyp „Attribut“. Wechseln Sie auf die Explorer-Seite der Entität, um den Transaktionsverlauf der Entitäten anzuzeigen, die den Transaktionsprotokolltyp „Element“ aufweisen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Versionsverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-reverse-a-transaction"></a>So kehren Sie eine Transaktion um  
  
1.  Klicken Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite auf **Versionsverwaltung**.  
  
2.  Klicken Sie in der Menüleiste auf **Transaktionen**.  
  
3.  Wählen Sie auf der Seite **Transaktionen** in der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
5.  Klicken Sie auf die Zeile im Raster für die Transaktion, die Sie umkehren möchten.  
  
6.  Klicken Sie auf **Transaktion umkehren**.  
  
7.  Klicken Sie im Bestätigungsdialogfeld auf **OK**. Dem Raster wird eine weitere Transaktion hinzugefügt, um die umgekehrte Transaktion aufzuzeichnen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)   
 [Reaktivieren eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
 [Zurücksetzen des Elementrevisionsverlaufs](../master-data-services/rollback-member-revision-history-master-data-services.md)
  
  
