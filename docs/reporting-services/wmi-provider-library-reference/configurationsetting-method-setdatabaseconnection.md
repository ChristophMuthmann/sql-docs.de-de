---
title: 'SetDatabaseConnection-Methode (WMI: MSReportServer_ConfigurationSetting) | Microsoft-Dokumentation'
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
apiname:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d570b4d32481e15ce78bef98c97b7330192f1c8c
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="configurationsetting-method---setdatabaseconnection"></a>ConfigurationSetting-Methode: SetDatabaseConnection
  Legt die Berichtsserver-Datenbankverbindung auf eine bestimmte Berichtsserver-Datenbank fest  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameter  
 *Server*  
 Der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, die zum Hosten der Berichtsserver-Datenbank verwendet wird.  
  
 *DatabaseName*  
 Der Name der Berichtsserver-Datenbank  
  
 *CredentialsType*  
 Der Typ der zu verwendenden Anmeldeinformationen für die Verbindung. Folgende Werte sind möglich:  
  
-   0 – Windows  
  
-   1 – [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 – Windows-Dienst  
  
 *UserName*  
 Der Kontoname, der zum Herstellen der Verbindung mit der Berichtsserver-Datenbank verwendet wird  
  
 *Kennwort*  
 Das Kennwort, das zum Herstellen der Verbindung mit der Berichtsserver-Datenbank verwendet wird  
  
 *HRESULT*  
 [out] Wert, der angibt, ob der Aufruf erfolgreich war oder zu einem Fehler geführt hat.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt *HRESULT* zurück, wodurch der Erfolg oder das Fehlschlagen des Methodenaufrufs angegeben wird. Der Wert 0 (null) gibt an, dass der Methodenaufruf erfolgreich war. Ein Wert ungleich 0 (null) gibt an, dass ein Fehler aufgetreten ist.  
  
## <a name="remarks"></a>Remarks  
 Wenn der *CredentialsType* -Parameter auf 0 (Windows) festgelegt ist, müssen die Parameter *UserName* und *Password* festgelegt werden. Der *UserName* -Parameter muss die Form „domain\username“ haben, und der Wert muss einen gültigen Windows-Anmeldenamen darstellen.  
  
 Wenn der *CredentialsType* -Parameter auf 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) festgelegt ist, muss der im *UserName* -Parameter übergebene Wert den Anforderungen an einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen entsprechen.  
  
 Wenn der *CredentialsType* -Parameter auf 2 (Windows-Dienst) festgelegt ist, verwendet der Berichtsserver die integrierte Sicherheit, um eine Verbindung mit der Berichtsserver-Datenbank herzustellen, und die Parameter *UserName* und *Password* werden ignoriert. Der Report Server-Webdienst verwendet entweder das [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Konto oder das Konto eines Anwendungspools und das Windows-Dienstkonto, um auf die Berichtsserver-Datenbank zuzugreifen.  
  
 Die „SetDatabaseConnection“-Methode verschlüsselt und speichert beim Aufruf die Anmelde- und Datenbankinformationen in der Konfigurationsdatei für den angegebenen Berichtsserver.  
  
 Die „SetDatabaseConnection“-Methode überprüft nicht, ob der Berichtsserver mithilfe der angegebenen Daten eine Verbindung mit der Berichtsserver-Datenbank herstellen kann.  
  
 Wenn die „ConnectionPoolSize“-Eigenschaft zum ersten Mal festgelegt wird, werden folgende Prozessoren zugrunde gelegt: ConnectionPoolSize = Anzahl der Prozessoren x 75.  
  
 Die „SetDatabaseConnection“-Methode erteilt den angegebenen Konten keine Berechtigungen. Sie müssen die [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md) -Methode für jedes Konto aufrufen, das Zugriff auf die Berichtsserver-Datenbank erfordert, und dann das resultierende Skript ausführen.  
  
## <a name="requirements"></a>Anforderungen  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
