---
title: Erstellen die Server-Connection-Dateien (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Creating Server Connection Files
- Sybase Console,Server Connection File Validation
ms.assetid: 35ef396f-9f98-429d-9fc5-4f413d08fb37
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3560921debc16ed2752b27cfe174e68958496b0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="creating-the-server-connection-files-sybasetosql"></a>Erstellen die Server-Connection-Dateien (SybaseToSQL)
Informationen zum Server kann entweder im Bereich "Server" der Skriptdatei oder in einem separaten Server Verbindungsdatei angegeben werden. Die Befehlszeilenparameter für die Server-Verbindungsdatei ist, `-c <serverconnectionfile>`. Wenn die gleiche Id in der Skriptdatei und die Verbindungsdatei Server vorhanden ist, wird die Definition des Servers in der Skriptdatei angesehen.  
  
**Beispiel:**  
  
```  
1.<!--Sample of server connection file commands -->  
  
<sybase name="<source-server-unique-name>">  
  
  <standard-mode>  
  
    <provider value="Ole DB Provider"/>  
  
    <server-name value="<server-name>"/>  
  
    <server-port value="<port>"/>  
  
    <user-id value="<password>"/>  
  
  </standard-mode>  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
```  
2.<!—Sample of server connection file commands-->  
<sybase name="<source-server-unique-name>">  
  
  <advanced-mode>  
  
    <connection-string value="User ID=<user-name>;Password=<password>;Provider=ASEOLEDB.1;Server=<server-name>;Port=<port>;OLE DB Services = -2;"/>  
  
  </advanced-mode >  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication >  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
## <a name="server-connection-file-validation"></a>Server-Verbindung Dateiüberprüfung  
Benutzer kann problemlos überprüfen Benutzervoreinstellung Verbindung Serverdatei anhand der Schemadefinitionsdatei **S2SSConsoleScriptServersSchema.xsd** in den Ordner "Schemas" verfügbar.  
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole funktioniert [Ausführen der Konsole SSMA &#40; SybaseToSQL &#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Executing the SSMA Console (Ausführen der SSMA-Konsole)](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
