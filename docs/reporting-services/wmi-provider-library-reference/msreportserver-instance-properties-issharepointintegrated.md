---
title: 'IsSharePointIntegrated-Eigenschaft (WMI: MSReportServer_Instance) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6352e7e78cd2ad51774729256b71290fa06d7285
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="msreportserverinstance-properties---issharepointintegrated"></a>MSReportServer_Instance-Eigenschaften: IsSharePointIntegrated
  Gibt an, ob sich der Berichtsserver im integrierten SharePoint-Modus befindet Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]gibt diese Eigenschaft immer **FALSE** zurück, da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanzen im SharePoint-Modus freigegebene SharePoint-Dienste darstellen und nicht von WMI-Anbietern kontrolliert werden.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Eigenschaftswerte  
 Ein **Boolean** -Wert, der angibt, ob sich der Berichtsserver im integrierten SharePoint-Modus befindet  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_Instance-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting Class (MSReportServer_ConfigurationSetting-Klasse)](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
