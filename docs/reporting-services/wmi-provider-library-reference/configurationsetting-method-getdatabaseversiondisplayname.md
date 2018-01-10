---
title: GetDatabaseVersionDisplayName-Methode (WMI) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: GetDatabaseVersionDisplayName method
ms.assetid: e1286424-7043-4f12-a7ad-1cf69e81baa4
caps.latest.revision: "15"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34369ec94a9370b01886f0ff5516caa27a01f556
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---getdatabaseversiondisplayname"></a>ConfigurationSetting-Methode: GetDatabaseVersionDisplayName
  Ruft den Anzeigenamen für eine gegebene Versionszeichenfolge in der Berichtsserver-Datenbank ab  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub GetDatabaseVersionDisplayName(Version As String, DisplayName As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetDatabaseVersionDisplayName(string Version, string DisplayName, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *Version*  
 Eine Zeichenfolge, die die Versionszeichenfolge für eine Berichtsserver-Datenbank enthält  
  
 *DisplayName*  
 [out] Eine Zeichenfolge, die den Anzeigenamen enthält, welcher der angegebenen Version entspricht  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="remarks"></a>Remarks  
 In der folgenden Tabelle ist die Zuordnung der Datenbankversion zur Anzeigezeichenfolge dargestellt.  
  
|**Release**|**Version**|**Anzeigename**|  
|-----------------|-----------------|----------------------|  
|RS 2005 SP2|@DBVersion = 'C.0.8.54'|SQL Server 2005 SP2|  
|RS 2005 SP1|@DBVersion = 'C.0.8.43'|SQL Server 2005 SP1|  
|RS 2005 RTM|@DBVersion = 'C.0.8.40'|SQL Server 2005|  
|RS 2000 SP2|@DBVersion = 'C.0.6.54'|SQL Server 2000 SP2|  
|RS 2000 SP1|@DBVersion = 'C.0.6.51'|SQL Server 2000 SP1|  
|RS 2000 RTM|@DBVersion = 'C.0.6.43'|SQL Server 2000|  
|Hotfix||Nächste geeignete Version|  
  
 Für eine *Version* vor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 wird HRESULT = ACT_E_BAD_VERSION zurückgegeben.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
