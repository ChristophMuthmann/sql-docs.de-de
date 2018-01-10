---
title: IsSharePointIntegrated-Eigenschaft (WMI) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
caps.latest.revision: "11"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b38ade3afeb97d114fd0570d00467b3f9cb1c7ba
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-property---issharepointintegrated"></a>ConfigurationSetting-Eigenschaft: IsSharePointIntegrated
  Gibt an, ob sich der Berichtsserver im integrierten SharePoint-Modus befindet Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]gibt diese Eigenschaft immer **FALSE** zurück, da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanzen im SharePoint-Modus freigegebene SharePoint-Dienste darstellen und nicht von WMI-Anbietern kontrolliert werden.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Eigenschaftswerte  
 Ein **Boolean** -Objekt, das angibt, ob sich der Berichtsserver im integrierten SharePoint-Modus befindet  
  
## <a name="example-code"></a>Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
