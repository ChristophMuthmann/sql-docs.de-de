---
title: Neuverteilen von ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c87db9dd22e53f8335dcbbb4994cd0835dfafcb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="redistributing-adomdnet"></a>Neuverteilen von ADOMD.NET
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Wenn Sie Anwendungen, die ADOMD.NET verwenden schreiben, müssen Sie die entsprechende Version von ADOMD.NET zusammen mit der Anwendung verteilen. Um ADOMD.NET erneut zu verteilen, fügen Sie das ADOMD.NET-Setupprogramm in das Setupprogramm Ihrer Anwendung ein.  
  
 Das ADOMD.NET-Setupprogramm sowie die neueste Version von ADOMD.NET stehen im Microsoft Download Center als Komponente des SQL Server Feature Packs bereit.  
  
 Das ADOMD.NET-Setupprogramm installiert die ADOMD.NET-Dateien im \< *Systemlaufwerk*>: \Program Files\Microsoft.NET\ADOMD.NET\\*Versionsnummer*.  
  
 Nachdem Sie das ADOMD.NET-Setupprogram eingefügt haben, sorgen Sie dafür, dass das Setupprogramm Ihrer Anwendung das ADOMD.NET-Setupprogramm startet und ADOMD.NET installiert. Je nach Umgebung müssen Sie ggf. sicherstellen, dass den verknüpften Assemblys von SQL Server vertraut wird.  
  
 Weitere Informationen:  
  
 [FeaturePack für Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET-Abhängigkeiten](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Clientprogrammierung](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET-Serverprogrammierung](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
