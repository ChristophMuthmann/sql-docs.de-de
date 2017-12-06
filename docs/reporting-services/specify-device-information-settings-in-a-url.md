---
title: "Angeben von Geräteinformationseinstellungen in einer URL | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: "32"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c091904698d3a513eb2ff09068ab515a3e7d6ea3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="specify-device-information-settings-in-a-url"></a>Angeben von Geräteinformationseinstellungen in einer URL
  Geräteinformationseinstellungen sind Parameter, die an eine Renderingerweiterung übergeben werden. Wenn Sie einen Bericht mit den Methoden des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Berichtsserver-Webdiensts rendern, wird ein **DeviceInfo** -XML-Element als ein Eingabeparameter übergeben. Untergeordnete Elemente des **DeviceInfo** -Elements sind für die Geräteinformationseinstellungen anderer Renderingerweiterungen spezifisch. Sie können die Geräteinformationseinstellungen in einer URL angeben, indem Sie die *rc:tag=value* -Parameterzeichenfolge verwenden, wobei *tag* der Name des Elements für die Geräteinformationseinstellungen ist. Weitere Informationen zu den Geräteinformationseinstellungen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]finden Sie im Artikel [Übergeben von Geräteinformationseinstellungen an Renderingerweiterungen](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Format des angegebenen Berichts auf JPEG eingestellt, indem die Geräteinformationseinstellung *OutputFormat* der Bild-Renderingerweiterung verwendet wird (die Zeilenumbrüche wurden aus Gründen der Lesbarkeit eingefügt):  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>Siehe auch  
 [URL-Zugriff &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL Access Parameter Reference (URL-Zugriffsparameterverweis)](../reporting-services/url-access-parameter-reference.md)  
  
  
