---
title: 'DeleteEncryptionKey-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
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
apiname: DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 68db6215f4101f0ec6f9a5557e2dd00ee3dc696e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="configurationsetting-method---deleteencryptionkey"></a>ConfigurationSetting-Methode: DeleteEncryptionKey
  Löscht die Verschlüsselungsschlüssel aus der Berichtsserver-Datenbank  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub DeleteEncryptionKeys(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptionKeys(string InstallationID, out Int32 HRESULT,   
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parameter  
 *InstallationID*  
 Die Installations-ID eines Berichtsservers, die sich in der Schlüsseltabelle der Berichtsserver-Datenbank befindet  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
 *ExtendedErrors[]*  
 [out] Ein Zeichenfolgenarray, das zusätzliche Fehler enthält, die durch den Aufruf zurückgegeben werden  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt HRESULT zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Durch die *DeleteEncryptionKey* -Methode werden für alle Berichtsserver mit Zugriff auf die sicheren Informationen in der Berichtsserver-Datenbank Einträge aus der Schlüsseltabelle gelöscht. Wenn der angegebene *InstallationID* -Parameter keiner Installations-ID in der Datenbank entspricht, gibt die Methode einen Fehler zurück.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
