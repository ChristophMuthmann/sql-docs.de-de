---
title: "Endgültiges Löschen von Versionselementen (Master Data Services) | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 56cccc3f368f17118dece215275fbe23822e9040
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="purge-version-members-master-data-services"></a>Endgültiges Löschen von Versionselementen (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]führt das Löschen eines Elements lediglich zum Deaktivieren bzw. vorläufigen Löschen des Elements. Die Daten sind weiterhin in der Datenbank vorhanden. In diesem Thema wird beschrieben, wie Sie alle vorläufig gelöschten Elemente in einer Modellversion dauerhaft löschen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Voraussetzungen für dieses Verfahren.  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich „Versionsverwaltung“ verfügen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
## <a name="to-purge-soft-deleted-members"></a>So löschen Sie vorläufig gelöschte Elemente dauerhaft  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Versionsverwaltung**.  
  
2.  Wählen Sie auf der Seite **Versionen verwalten** das Modell mit der Version aus, die Sie löschen möchten. Die Liste der Modellversionen wird angezeigt.  
  
3.  Wählen Sie die Zeile für die Version aus, die Sie löschen möchten.  
  
4.  Klicken Sie auf **Elemente löschen**.  
  
5.  Klicken Sie auf „OK“, wenn die Aufforderung zur Bestätigung angezeigt wird.  
  
## <a name="additional-methods-to-purge-members"></a>Weitere Methoden zum endgültigen Löschen von Elementen  
 Durch das endgültige Löschen von Versionselementen werden vorläufig gelöschte Elemente in allen Entitäten gelöscht, die der ausgewählten Version angehören. Für einen differenzierteren Löschvorgang kann das entitätsbasierte Staging verwendet werden, um nur bestimmte Elemente einer Entität endgültig zu löschen. Entitätsadministratoren mit der Explorer-Funktionsberechtigung können eine Entitätsversion zudem auf der Seite des Entitäts-Explorers löschen.  
  
 Weitere Informationen finden Sie unter [Stagingtabelle für Blattelemente &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
  
