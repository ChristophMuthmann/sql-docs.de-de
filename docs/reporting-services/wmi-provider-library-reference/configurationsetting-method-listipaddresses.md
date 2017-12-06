---
title: 'ListIPAddresses-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
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
helpviewer_keywords: ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ec2238f83d91f881776367798ced2a7091cbbcb4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="configurationsetting-method---listipaddresses"></a>ConfigurationSetting-Methode: ListIPAddresses
  Listet die IP-Adressen für den Berichtsservercomputer auf.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub ListIPAddresses (ByRef IPAddress() as String, _  
    ByRef IPVersion()as String, ByRef IsDhcpEnabled () as Boolean, _   
    ByRef Length as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListIPAddresses (out string[] IPAddress,   
    out string[] IPVersion, out bool[] isDhcpEnabled, out int length,   
    out int HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *IPAddress[]*  
 [out] Die Liste der IP-Adressen für den Computer  
  
 *IPVersion[]*  
 [out] Die Version für die IP-Adressen  
  
 *IsDhcpEnabled[]*  
 [out] Gibt an, ob die IP-Adressen DHCP-aktiviert sind  
  
 *Länge*  
 [out] Die Länge des von der Methode zurückgegebenen Arrays  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## <a name="remarks"></a>Hinweise  
 *IPVersion* -Zeichenfolgen sind V4 und V6.  
  
 Wenn *IsDhcpEnabled* gleich **True**ist, ist die *IPAddress* dynamisch. Eine Verwendung für SSL-Bindungen wird nicht empfohlen.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
