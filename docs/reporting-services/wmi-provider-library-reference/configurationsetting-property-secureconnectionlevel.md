---
title: 'SecureConnectionLevel-Eigenschaft (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
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
apiname: SecureConnectionLevel
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
caps.latest.revision: "19"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cd9ce2573ded50f9ad4fbc834196bfa97ace8257
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>ConfigurationSetting-Eigenschaft: SecureConnectionLevel
  Gibt die in der Datei RSReportServer.config angegebene sichere Verbindungsebene zurück. Schreibgeschützt.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>Eigenschaftswerte  
 Ein **Integer** -Wert, der die sichere Verbindungsebene darstellt. Die Rückgabewerte geben an, dass SSL entweder konfiguriert ist oder nicht. Ein Wert größer oder gleich 1 gibt an, dass SSL aktiviert ist. Der Wert 0 gibt an, dass SSL deaktiviert wird.  
  
## <a name="example-code"></a>Beispielcode  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
