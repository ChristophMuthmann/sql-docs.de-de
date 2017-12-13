---
title: "Hinzufügen von MSOLAP. 5 als vertrauenswürdigen Datenanbieter in Excel Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 146b61a544dfc91585cde88bbdb54d2f43375b0f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Hinzufügen von MSOLAP.5 als vertrauenswürdigen Datenanbieter in Excel Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]MSOLAP. 5 bezieht sich auf die Analysis Services OLE DB-Anbieter für SQL Server 2012. Excel Services muss diesem Anbieter vertrauen, bevor es die Verbindunganforderung ermöglicht, wodurch die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten auf dem Server verfügbar werden.  
  
 Wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint mithilfe des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstools konfiguriert haben, ist MSOLAP.5 möglicherweise ein vertrauenswürdiger Anbieter, da das Tool eine Aktion bietet, die diese Anforderung erfüllt. Wenn Sie jedoch PowerShell oder die Zentraladministration verwenden oder die Aktion für den vertrauenswürdigen Anbieter im Konfigurationstool ausgeschlossen haben, fehlt möglicherweise der Anbieter, und Sie müssen den Anbieter jetzt bei der Konfiguration der Farm für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff hinzufügen.  
  
 Sie müssen diesen Schritt für jede Excel Services-Dienstanwendung nur einmal ausführen.  
  
 Für jeden physischen Server, der eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenanforderung behandelt, z. B. eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server oder ein Excel Services-Server, muss auf dem Computer der OLE DB-Anbieter installiert sein. Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation umfasst immer den OLE DB-Anbieter. Wenn Sie die Excel Services jedoch auf einem Computer ausführen, auf dem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nicht vorhanden ist, müssen Sie den Anbieter manuell installieren. Weitere Informationen finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Hinzufügen eines vertrauenswürdigen Anbieters zu Excel Services  
  
1.  Klicken Sie in der Zentraladministration auf **Dienstanwendungen verwalten**und dann auf die Excel Services-Dienstanwendung.  
  
2.  Klicken Sie auf **Vertrauenswürdige Dienstanbieter**.  
  
3.  Überprüfen Sie, dass MSOLAP.5 in der Liste angezeigt wird. Je nach der Art der Konfiguration von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint wird MSOLAP.5 möglicherweise bereits vertraut.  
  
4.  Falls nicht aufgeführt, klicken Sie auf **Vertrauenswürdigen Datenanbieter hinzufügen**.  
  
5.  Geben Sie unter Anbieter-ID **MSOLAP.5**ein.  
  
6.  Stellen Sie sicher, dass für den Anbietertyp OLE DB ausgewählt ist.  
  
7.  Geben Sie als Anbieterbeschreibung **Microsoft OLE DB-Anbieter für OLAP Services 11.0**ein.  
  
  
