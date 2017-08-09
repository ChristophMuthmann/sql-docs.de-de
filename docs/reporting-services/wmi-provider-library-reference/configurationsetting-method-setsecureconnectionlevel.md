---
title: 'SetSecureConnectionLevel-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft Docs'
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
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 219112996b6fd0c2fb1cb6eff5baca29b65e86d2
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---setsecureconnectionlevel"></a>ConfigurationSetting Methode - SetSecureConnectionLevel
  Legt die sichere Verbindungsebene des Berichtsservers fest  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *Ebene*  
 Ein ganzzahliger Wert, der eine sichere Verbindungsebene darstellt  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Bei einem Aufruf wird die SecureConnectionLevel-Eigenschaft des Berichtsservers auf den angegebenen Wert festgelegt. Der Wert 0 gibt an, dass SSL deaktiviert wird. Ein Wert größer oder gleich 1 gibt an, dass SSL aktiviert wird.  
  
-   Wenn der Wert festgelegt ist, wird das SecureConnectionLevel-Element in der Berichtsserver-Konfigurationsdatei geändert, und für das **URLRoot** -Element in der Konfigurationsdatei wird die Verwendung von „https://“ festgelegt, wenn das angegebene *Level* größer oder gleich 1 ist. Wenn das angegebene *Level* 0 ist, wird die Verwendung von „http://“ festgelegt.  
  
 In [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]wird SecureConnectionLevel zu einer ON-/OFF-Option mit dem Standardwert 0. Bei einem beliebigen Wert größer oder gleich 1, der über eine API der SetSecureConnectionLevel-Methode übergeben wird, wird SSL als aktiviert erachtet und die SecureConnectionLevel-Konfigurationseigenschaft in der Datei „rsreportserver.config“ entsprechend festgelegt. Werte von 2 und 3 werden weiterhin aus Gründen der Abwärtskompatibilität zugelassen.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
