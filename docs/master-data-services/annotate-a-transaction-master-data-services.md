---
title: Hinzufügen einer Anmerkung zu einer Transaktion (Master Data Services) | Microsoft-Dokumentation
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
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b050b8aaeb0629e40f61e64ad0222bf5f725c70
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="annotate-a-transaction-master-data-services"></a>Hinzufügen einer Anmerkung zu einer Transaktion (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Versehen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Transaktion mit einer Anmerkung, wenn Sie unterstützende Details zur Transaktion zu historischen Zwecken bereitstellen möchten.  
  
> [!NOTE]  
>  Anmerkungen können nicht gelöscht werden.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Um von Ihnen erstellte Transaktionen mit einer Anmerkung versehen zu können, müssen Sie über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** und mindestens über die Berechtigung **Aktualisieren** für das Modellobjekt verfügen, das Sie mit einer Anmerkung versehen möchten.  
  
-   Um Transaktionen für alle Benutzer mit einer Anmerkung zu versehen, müssen Sie über die Berechtigung für den Zugriff auf den Funktionsbereich **Versionsverwaltung** verfügen und Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>So versehen Sie im Explorer eine Transaktion mit einer Anmerkung  
  
1.  Wählen Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite aus der Liste **Modell** ein Modell aus.  
  
2.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
3.  Klicken Sie auf **Explorer**.  
  
4.  Zeigen Sie in der Menüleiste auf **Entitäten** und klicken Sie auf die Entität mit dem Element mit einer Transaktion, die Sie mit einer Anmerkung versehen möchten.  
  
5.  Klicken Sie im Raster auf die Zeile des Elements.  
  
6.  Klicken Sie auf **Transaktionen anzeigen**.  
  
7.  Klicken Sie im Dialogfeld **Transaktionen anzeigen** auf die Transaktion, die Sie mit einer Anmerkung versehen möchten.  
  
8.  Geben Sie die Anmerkung im Feld am unteren Rand des Dialogfelds ein.  
  
9. Klicken Sie auf **Anmerkung hinzufügen**. Die Anmerkung wird im Bereich **Anmerkungen** angezeigt.  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>So versehen Sie in der Versionsverwaltung eine Transaktion mit einer Anmerkung (nur Administratoren)  
  
1.  Klicken Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite auf **Versionsverwaltung**.  
  
2.  Klicken Sie in der Menüleiste auf **Transaktionen**.  
  
3.  Klicken Sie im Bereich **Transaktionen** auf die Zeile im Raster für die Transaktion, die Sie mit einer Anmerkung versehen möchten.  
  
4.  Geben Sie die Anmerkung im Bereich **Transaktionsanmerkungen** im Feld **Anmerkung** ein.  
  
5.  Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anmerkungen &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)   
 [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  
