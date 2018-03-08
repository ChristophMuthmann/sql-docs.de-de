---
title: Mehrsprachige und globale Bereitstellungen (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dab26bd1f9308c4d2c5814e054b9d4c882527a44
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>Mehrsprachige und globale Bereitstellungen (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] unterstützt die Bereitstellung von Komponenten und Tools in allen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützten Sprachen. Weitere Informationen finden Sie unter [Local Language Versions in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
## <a name="how-languages-are-used"></a>Vorgehensweise bei der Verwendung von Sprachen  
 In der folgenden Tabelle wird die Sprachunterstützung für die Komponenten und Tools von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] beschrieben.  
  
|Komponente oder Tool|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Setup|Wählen Sie das englische Setupprogramm aus, wenn die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung in anderen Sprachen als der Setupsprache verfügbar sein und unterstützt werden soll. Weitere Informationen finden Sie in der Beschreibung zu [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] unten.|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|Die Setupsprache bestimmt die Sprache von [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] . Wenn Sie Deutsch als Setupsprache auswählen, ist [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] auf dem betreffenden Computer z. B. in Deutsch verfügbar.|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Wenn Sie das Setup auf Englisch ausführen, wird die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung in allen Anwendungssprachen bereitgestellt und unterstützt. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] kann in jeder dieser Anwendungssprachen angezeigt werden und akzeptiert gebietsschemaspezifische Eingaben auf Grundlage der Spracheinstellungen des Clientwebbrowsers. Wenn die Spracheinstellungen für eine nicht unterstützte Anwendungssprache konfiguriert werden, verwendet [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] standardmäßig Englisch.<br /><br /> Wenn Sie das Setup in einer anderen Sprache als Englisch ausführen, sind Ressourcen für alle anderen Anwendungssprachen enthalten. Bei diesem Szenario kann [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] von den Clients jedoch nicht in einer anderen Sprache als der ausgewählten Setupsprache verwendet werden. Wenn Sie versuchen, in einer anderen Sprache als der Setupsprache auf [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] zuzugreifen, könnten Probleme bei der Anzeige und Eingabe von Daten in die Anwendung auftreten.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Datenbank|Die Informationen in der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Datenbank sind nicht spezifisch für ein bestimmtes Gebietsschema. Dadurch kann [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] selbst bestimmen, wie Informationen, z. B. Datumsangaben und Zahlen, in dem durch die Spracheinstellungen im Clientwebbrowser festgelegten Format angezeigt werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Installieren von Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
