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
ms.openlocfilehash: 6587a23e479522453feb01bf7190cebc9fb505df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
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
  
  
