---
title: 'RemoveURL-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b47933be28aae96673ca6c3b28410874c01394dc
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---removeurl"></a>ConfigurationSetting Methode - RemoveURL
  Entfernt eine für den Berichtsserver reservierte URL Wenn mehrere URLs entfernt werden müssen, muss dies einzeln durch mehrfache Aufrufe dieser API erfolgen.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *Application*  
 Der Name der Anwendung, für die die Reservierung entfernt werden soll  
  
 *URLString*  
 Die URL für die Reservierung  
  
 *lcid*  
 Das Gebietsschema, das für die zurückgegebenen Fehlermeldungen verwendet werden soll  
  
 *Fehler*  
 [out] Die Beschreibung des Fehlers, der aufgetreten ist  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## <a name="remarks"></a>Hinweise  
 *UrlString* beinhaltet nicht den Namen des virtuellen Verzeichnisses – die Methode [SetVirtualDirectory-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) ist für diesen Zweck vorgesehen.  
  
 Vor einem Aufruf der [ReserveURL](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)-Methode müssen Sie einen Wert für die VirtualDirectory-Konfigurationseigenschaft des *Anwendungsparameters* angeben. Verwenden Sie die Methode [SetVirtualDirectory-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md), um die VirtualDirectory-Eigenschaft festzulegen.  
  
 Wenn durch [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ein SSL-Zertifikat bereitgestellt wurde und keine anderen URLs dieses benötigen, wird es entfernt.  
  
 Diese Methode verursacht einen "harten" Wiederverwendungsvorgang und ein Beenden aller Nichtkonfigurationsdomänen für Anwendungen. Die Anwendungsdomänen werden nach dem Abschluss des Vorgangs neu gestartet.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

