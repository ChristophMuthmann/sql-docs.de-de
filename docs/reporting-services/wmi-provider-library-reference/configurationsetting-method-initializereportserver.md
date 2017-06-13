---
title: 'InitializeReportServer-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs'
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
apiname:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 54b03cf3453777e6d1cc74e27d77686978e2516c
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="configurationsetting-method---initializereportserver"></a>ConfigurationSetting Methode - InitializeReportServer
  Initialisiert die angegebene Berichtsdienstinstanz  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parameter  
 *InstallationID*  
 Eine Zeichenfolge, mit der der Verschlüsselungsschlüssel verschlüsselt wird, bevor er zurückgegeben wird  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
 *ExtendedErrors[]*  
 [out] Ein Zeichenfolgenarray, das zusätzliche Fehler enthält, die durch den Aufruf zurückgegeben werden  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Wenn diese Methode aufgerufen wird, wird der Verschlüsselungsschlüssel, der auf die sicheren Informationen der Berichtsserverdatenbank zugreift, mit dem öffentlichen Schlüssel des Berichtsservers verschlüsselt, der von *InstallationID*angegeben wird.  
  
 Der angegebene öffentliche Schlüssel des Berichtsservers muss zuvor in die Berichtsserver-Datenbank geschrieben worden sein.  
  
 Die *InitializeReportServer* -Methode muss für einen Berichtsserver aufgerufen werden, der bereits Zugriff auf die sicheren Informationen hat, damit der Verschlüsselungsschlüssel entschlüsselt werden kann. Der resultierende verschlüsselte Verschlüsselungsschlüssel wird dann in der Berichtsserver-Datenbank gespeichert.  
  
 Wenn die [IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md) -Eigenschaft des Berichtsservers beim Aufruf der InitializeReportServer-Methode auf **TRUE** festgelegt ist, gibt die Methode einen Erfolgswert zurück, ohne zu versuchen, den Verschlüsselungsschlüssel zu verschlüsseln.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
