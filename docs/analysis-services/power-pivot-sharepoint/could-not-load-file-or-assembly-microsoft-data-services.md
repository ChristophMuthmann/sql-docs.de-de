---
title: Konnte nicht geladen werden, Datei oder Assembly Microsoft Datendienste | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1de8cd48bcce0b2c66a555358fc7c73182999f0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>Datei oder Assembly Microsoft Datendienste konnte nicht geladen werden
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In SharePoint 2010-Umgebungen mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint tritt dieser Fehler auf, wenn Sie versuchen, einen Datenfeed zu exportieren und das System nicht über die erforderliche Version von Microsoft ADO.NET Data Services verfügt.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Gilt für|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|ADO.NET Data Services 3.5 SP1 wurde nicht gefunden.|  
|Meldungstext|Die Datei oder Assembly "Microsoft.Data.Services, Version=3 .5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" oder eine Abhängigkeit davon wurde nicht gefunden. Die angegebene Datei wurde nicht gefunden.|  
  
## <a name="explanation"></a>Erklärung  
 SharePoint 2010 enthält die Schaltfläche Als Datenfeed exportieren, mit der Sie eine SharePoint-Liste als XML-Datenfeed exportieren können. Außerdem unterstützen sowohl Reporting Services in SharePoint-Modus als auch [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint Datenfeedfunktionen, die ADO.NET Data Services erfordern.  
  
 Wenn ADO.NET Data Services nicht installiert sind, tritt dieser Fehler beim Anfordern eines Datenfeeds auf.  
  
## <a name="user-action"></a>Benutzeraktion  
  
1.  Wechseln Sie zu den Hardware- und softwareanforderungen für SharePoint 2010 [bestimmen von Hardware- und Softwareanforderungen (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  Suchen Sie unter **Installieren der erforderlichen Software**den Link für ADO.NET Data Services 3.5, der dem verwendeten Betriebssystem entspricht.  
  
3.  Klicken Sie auf den Link, und führen Sie das Setupprogramm aus, durch das der Dienst installiert wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen von Power Pivot-Lösungen in SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
