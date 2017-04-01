---
title: "CreateSSLCertificateBinding-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "CreateSSLCertificateBinding"
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# CreateSSLCertificateBinding-Methode (WMI: MSReportServer_ConfigurationSetting)
  Erstellt eine SSL-Zertifikatsbindung  
  
## Syntax  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## Parameter  
 *Application*  
 Der Name der Anwendung, für die die Zertifikatsbindung erstellt werden soll  
  
 *CertificateHash*  
 Der Hash für das Zertifikat  
  
 *IPAddress*  
 Die IP-Adresse für die Anwendung  
  
 *Port*  
 Der SSL-Port, der der Bindung zugeordnet ist.  
  
 *Lcid*  
 Das Gebietsschema, das für die zurückgegebenen Fehlermeldungen verwendet werden soll  
  
 *Fehler*  
 [out] Die Beschreibung der Fehler, die aufgetreten sind  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Fehlercode gibt an, dass der Aufruf nicht erfolgreich war.  
  
## Hinweise  
 Diese Methode fügt rsreportserver.config eine Bindung für die Anwendung hinzu. Wenn HTTP.SYS noch keine Bindung enthält, wird diese dort erstellt.  
  
 Vor dem Erstellen der Bindung untersucht der Methodenaufruf die URL-Reservierungen für die angegebene Anwendung, um zu überprüfen, ob die SSL-Zertifikatsbindung gültig ist.  
  
 Die folgenden Bedingungen werden überprüft und können Ursache für Fehler sein:  
  
1.  Das Zertifikat ist nicht vorhanden.  
  
2.  Die angegebene IPAddress entspricht keiner IPAddress dieses Computers.  
  
3.  Die angegebene IP-Adresse ist eine DHCP-IP-Adresse (ändert sich in regelmäßigen Abständen). Verwenden Sie stattdessen die Platzhalter-IP-Adresse (0.0.0.0).  
  
4.  Die angegebene IP-Adresse entspricht weder der IP-Adresse für URL-Reservierungen noch ist eine Platzhalter- oder Hostnamen-URL-Reservierung vorhanden.  
  
5.  Eine URL-Reservierung, die einen Hostnamen angibt, ist vorhanden, der Hostname stimmt jedoch nicht mit dem Zertifikathostnamen überein.  
  
## Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  