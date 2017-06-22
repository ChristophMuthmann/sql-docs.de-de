---
title: 'SetEmailConfiguration-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs'
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
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: da1694467a88220546fa8ec8e02ff78564f605ed
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-method---setemailconfiguration"></a>ConfigurationSetting Methode - SetEmailConfiguration
  Konfiguriert die E-Mail-Übermittlungserweiterung, die vom Berichtsserver zum Senden von E-Mails verwendet wird  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *SendUsingSMTPServer*  
 Ein boolescher Wert, der angibt, ob der Server zum Senden von E-Mails den SMTP-Server verwenden soll. Dieser Wert kann nur auf true festgelegt werden. Der Standardwert ist "false".  
  
 *SMTPServer*  
 Eine Zeichenfolge, die den Namen oder die IP-Adresse eines SMTP-Servers enthält  
  
 *SenderEmailAddress*  
 Die im Feld Von: verwendete E-Mail-Adresse für vom Berichtsserver gesendete E-Mails  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der *SendUsingSMTPServer* -Parameter auf **true**festgelegt ist, wird der **SendUsing** -Eintrag in der Berichtsserver-Konfigurationsdatei auf 1 festgelegt. Wenn *SendUsingSMTPServer* auf **false**festgelegt ist, wird der **SendUsing** -Eintrag nicht konfiguriert.  
  
 Diese Methode gibt Benutzern keine Möglichkeit, den **SendUsing** -Eintrag in der Berichtsserver-Konfigurationsdatei auf einen anderen Wert als 1 festzulegen. Sie müssen die Konfigurationsdateien manuell bearbeiten, um den Berichtsserver für eine andere Option als SMTP-Mail zu konfigurieren.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
