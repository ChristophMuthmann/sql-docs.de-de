---
title: Endgültiges Löschen von Versionselementen (Master Data Services) | Microsoft-Dokumentation
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
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26c53b0e050ebdb9682fe8d64dc10f9500d88b46
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="purge-version-members-master-data-services"></a>Endgültiges Löschen von Versionselementen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]führt das Löschen eines Elements lediglich zum Deaktivieren bzw. vorläufigen Löschen des Elements. Die Daten sind weiterhin in der Datenbank vorhanden. In diesem Thema wird beschrieben, wie Sie alle vorläufig gelöschten Elemente in einer Modellversion dauerhaft löschen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Voraussetzungen für dieses Verfahren.  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich „Versionsverwaltung“ verfügen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
## <a name="to-purge-soft-deleted-members"></a>So löschen Sie vorläufig gelöschte Elemente dauerhaft  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Versionsverwaltung**.  
  
2.  Wählen Sie auf der Seite **Versionen verwalten** das Modell mit der Version aus, die Sie löschen möchten. Die Liste der Modellversionen wird angezeigt.  
  
3.  Wählen Sie die Zeile für die Version aus, die Sie löschen möchten.  
  
4.  Klicken Sie auf **Elemente löschen**.  
  
5.  Klicken Sie auf „OK“, wenn die Aufforderung zur Bestätigung angezeigt wird.  
  
## <a name="additional-methods-to-purge-members"></a>Weitere Methoden zum endgültigen Löschen von Elementen  
 Durch das endgültige Löschen von Versionselementen werden vorläufig gelöschte Elemente in allen Entitäten gelöscht, die der ausgewählten Version angehören. Für einen differenzierteren Löschvorgang kann das entitätsbasierte Staging verwendet werden, um nur bestimmte Elemente einer Entität endgültig zu löschen. Entitätsadministratoren mit der Explorer-Funktionsberechtigung können eine Entitätsversion zudem auf der Seite des Entitäts-Explorers löschen.  
  
 Weitere Informationen finden Sie unter [Stagingtabelle für Blattelemente &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
  
