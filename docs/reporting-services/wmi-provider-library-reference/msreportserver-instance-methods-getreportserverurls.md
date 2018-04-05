---
title: 'GetReportServerUrls-Methode (WMI: MSReportServer_Instance) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fb88837f3c9393c561e65c13656bb0e87a516325
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="msreportserverinstance-methods---getreportserverurls"></a>MSReportServer_Instance-Methoden: GetReportServerUrls
  Gibt eine Liste von URLs zurück, über die Benutzer auf den Berichtsserver und den [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]zugreifen können.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *ApplicationName[]*  
 Ein Array, das die installierten Anwendungen enthält. Werte sind entweder **ReportServerWebService** oder **ReportServerWebApp**.  
  
 *URLs[]*  
 Ein Array, das die erfolgreich registrierten URLs enthält  
  
 *Länge*  
 Ein Integer-Wert, der die Länge der zurückgegebenen Arrays enthält.  
  
 *HRESULT*  
 Ein Wert, der Erfolg oder einen Fehlercode angibt  
  
## <a name="return-values"></a>Rückgabewerte  
  
## <a name="remarks"></a>Remarks  
 Von WMI-Verwaltungsobjekten verfügbar gemachte Methoden werden durch die InvokeMethod-Funktion aufgerufen. Weitere Informationen finden Sie in "Ausführen von Methoden für Verwaltungsobjekte" in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI-Dokumentation.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
