---
title: "ListSSLCertificates-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ListSSLCertificates-Methode"
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ListSSLCertificates-Methode (WMI: MSReportServer_ConfigurationSetting)
  Gibt eine Liste der Zertifikate auf dem Berichtsservercomputer zurück  
  
## Syntax  
  
```vb  
Public Sub CreateSSLCertificateBinding (ByRef CertificateHash() as String, _  
    ByRef CertName() as String, ByRef HostName() as String, ByRef Length as Int32, _   
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListSSLCertificates(out string[] CertificateHash,   
    out string[] CertName, out string[] Hostname, out Int32 length,   
    out Int32 HRESULT);  
```  
  
## Parameter  
 *CertificateHash[]*  
 [out] Der Hash der Zertifikate  
  
 *CertName[]*  
 [out] Die Namen des Zertifikats.  
  
 *HostName[]*  
 [out] Die Hostnamen der Zertifikate  
  
 *Länge*  
 [out] stellt die Länge der Arrays *CertificateHash*, *CertName* und *HostName* dar.  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## Hinweise  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  