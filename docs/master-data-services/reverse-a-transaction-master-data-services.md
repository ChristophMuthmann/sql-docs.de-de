---
title: Umkehren einer Transaktion (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c0adfc3f27bf8767f759a67001020cbbdff9f31
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="reverse-a-transaction-master-data-services"></a>Umkehren einer Transaktion (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine Transaktion umkehren, wenn eine Aktion rückgängig gemacht werden muss. Beispiele für Transaktionen sind Attributwertänderungen, Hierarchieverschiebungen oder Elementlöschungen. Dieses Thema gilt für Transaktionen von Entitäten mit dem Transaktionsprotokolltyp „Attribut“. Wechseln Sie auf die Explorer-Seite der Entität, um den Transaktionsverlauf der Entitäten anzuzeigen, die den Transaktionsprotokolltyp „Element“ aufweisen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Versionsverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-reverse-a-transaction"></a>So kehren Sie eine Transaktion um  
  
1.  Klicken Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite auf **Versionsverwaltung**.  
  
2.  Klicken Sie in der Menüleiste auf **Transaktionen**.  
  
3.  Wählen Sie auf der Seite **Transaktionen** in der Liste **Modell** ein Modell aus.  
  
4.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
5.  Klicken Sie auf die Zeile im Raster für die Transaktion, die Sie umkehren möchten.  
  
6.  Klicken Sie auf **Transaktion umkehren**.  
  
7.  Klicken Sie im Bestätigungsdialogfeld auf **OK**. Dem Raster wird eine weitere Transaktion hinzugefügt, um die umgekehrte Transaktion aufzuzeichnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Transaktionen &#40; Master Data Services &#41;](../master-data-services/transactions-master-data-services.md)   
 [Reaktivieren Sie ein Element oder die Collection &#40; Master Data Services &#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
 [Rollback-Elementrevisionsverlauf](../master-data-services/rollback-member-revision-history-master-data-services.md)
  
  
