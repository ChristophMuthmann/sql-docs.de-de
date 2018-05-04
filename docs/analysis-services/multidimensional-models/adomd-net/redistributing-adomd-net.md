---
title: Neuverteilen von ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d4d5f06605f68e830aa945d0b502dcb657211f2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="redistributing-adomdnet"></a>Neuverteilen von ADOMD.NET
  Wenn Sie Anwendungen schreiben, die ADOMD.NET verwenden, müssen Sie die entsprechende ADOMD.NET-Version zusammen mit der Anwendung erneut verteilen. Um ADOMD.NET erneut zu verteilen, fügen Sie das ADOMD.NET-Setupprogramm in das Setupprogramm Ihrer Anwendung ein.  
  
 Das ADOMD.NET-Setupprogramm sowie die neueste Version von ADOMD.NET stehen im Microsoft Download Center als Komponente des SQL Server Feature Packs bereit.  
  
 Das ADOMD.NET-Setupprogramm installiert die ADOMD.NET-Dateien im \< *Systemlaufwerk*>: \Program Files\Microsoft.NET\ADOMD.NET\\*Versionsnummer*.  
  
 Nachdem Sie das ADOMD.NET-Setupprogram eingefügt haben, sorgen Sie dafür, dass das Setupprogramm Ihrer Anwendung das ADOMD.NET-Setupprogramm startet und ADOMD.NET installiert. Je nach Umgebung müssen Sie ggf. sicherstellen, dass den verknüpften Assemblys von SQL Server vertraut wird.  
  
 Weitere Informationen:  
  
 [FeaturePack für Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET-Abhängigkeiten](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Clientprogrammierung](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET-Serverprogrammierung](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
