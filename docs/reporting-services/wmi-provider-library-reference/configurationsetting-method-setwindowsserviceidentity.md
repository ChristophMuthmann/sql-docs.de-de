---
title: 'SetWindowsServiceIdentity-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
caps.latest.revision: 19
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c7c0887b3049f935b5a8cab7649acb7ce8a9f000
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---setwindowsserviceidentity"></a>ConfigurationSetting-Methode: SetWindowsServiceIdentity
  Lässt den Report Server-Windows-Dienst als einen angegebenen Windows-Benutzer ausführen und gibt diesem Konto die erforderlichen Dateisystemberechtigungen, damit der Berichtsserver ausgeführt werden kann  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *UseBuiltInAccount*  
 Gibt an, ob das angegebene Konto ein integriertes Windows-Konto ist  
  
 *Konto*  
 Das Windows-Konto, das verwendet werden soll, um den Windows-Dienst auszuführen (im Format "DOMAIN\alias")  
  
 *Kennwort*  
 Das Kennwort für das Konto  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Remarks  
 Wenn der *UseBuiltInAccount* -Parameter auf **TRUE** festgelegt ist und der Berichtsserver unter Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] oder Windows XP ausgeführt wird, werden die Werte der Parameter *Name*, *Domäne*und *Kennwort* ignoriert, und das lokale Systemkonto wird verwendet.  
  
 Wenn der *UseBuiltInAccount* -Parameter auf **TRUE** festgelegt ist und der Berichtsserver unter Windows Server 2003 ausgeführt wird, werden die Eigenschaft *Domäne* und die Eigenschaft *Kennwort* ignoriert, und das Namensfeld muss den Namen „Builtin\NetworkService“, „Builtin\System“ oder „Builtin\LocalService“ enthalten.  
  
 Die SetWindowsServiceIdentity-Methode legt Dateiberechtigungen für Dateien und Ordner im Installationsverzeichnis des Berichtsservers fest.  
  
 Das im *Account* -Parameter angegebene Konto erfordert **LogonAsService** -Rechte in Windows. Die Methode gewährt dem angegebenen Konto dieses Recht.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
