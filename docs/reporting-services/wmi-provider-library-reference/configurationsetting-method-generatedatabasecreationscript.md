---
title: "ConfigurationSetting-Methode – GenerateDatabaseCreationScript | Microsoft-Dokumentation"
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
apiname: GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
caps.latest.revision: "25"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 668be602cce0b74e0d2662021b3e4306405c4fb7
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---generatedatabasecreationscript"></a>ConfigurationSetting-Methode – GenerateDatabaseCreationScript
  Generiert ein SQL-Skript, mit dem eine Berichtsserver-Datenbank erstellt werden kann  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *Databasename*  
 Eine Zeichenfolge, die den Namen der zu erstellenden Berichtsserver-Datenbank enthält  
  
 *Lcid*  
 Zur Lokalisierung von Rollennamen verwendeter Wert.  
  
 *IsSharePointMode*  
 Gibt an, ob die Datenbank im einheitlichen Modus oder im SharePoint-Modus erstellt werden soll.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]IsSharePointMode *True*=**wird ab** nicht mehr unterstützt, da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus ein gemeinsamer SharePoint-Dienst ist und nicht vom WMI-Anbieter kontrolliert wird. Es wird empfohlen, diesen Parameter immer auf **False**festzulegen.  
  
 *Skript*  
 [out] Eine Zeichenfolge, die das generierte SQL-Skript enthält  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Remarks  
 Diese Methode generiert ein SQL-Skript, mit dem Berichtsserver-Datenbanken für die Version des Berichtsservers erstellt werden, zu dem derzeit eine Verbindung besteht.  
  
 Der im Parameter *DatabaseName* angegebene Wert muss den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benennungskonventionen für Datenbanken entsprechen.  
  
 Die Methode überprüft beim Generieren des Skripts nicht das Vorhandensein der Datenbank.  
  
 Beim Generieren des Skripts überprüft diese Methode nicht, ob die Berichtsserver-Datenbank vorhanden ist.  
  
 Das generierte Skript unterstützt [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 und [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
