---
title: Erstellen die Server-Connection-Dateien (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Server Connection File Creation
- Server Connection File, Server Connection File Validation
ms.assetid: 002f129e-0868-48ad-a4b4-c68b5007e12e
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: db9027dd99e27749bcf7f7124147b5200f128310
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="creating-the-server-connection-files-oracletosql"></a>Erstellen die Server-Connection-Dateien (OracleToSQL)
Informationen zum Server kann entweder im Bereich "Server" der Skriptdatei oder in einem separaten Server Verbindungsdatei angegeben werden. Die Befehlszeilenparameter für die Server-Verbindungsdatei ist, `-c <serverconnectionfile>`. Wenn die gleiche Id in der Skriptdatei und die Verbindungsdatei Server vorhanden ist, wird die Definition des Servers in der Skriptdatei angesehen.  
  
**Beispiel 1:**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <tns-name-mode>  
  
    <connection-provider value="OracleClient"/>  
  
    <service-name value="(DESCRIPTION =(ADDRESS_LIST =(ADDRESS = (PROTOCOL = TCP)(HOST = <host-name>)(PORT = 1521)))(CONNECT_DATA =(SERVICE_NAME = <service-name>)))"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </tns-name-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
**Beispiel: 2**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <connection-string-mode>  
  
    <connection-provider value="OleDB Provider"/>  
  
    <custom-connection-string value="Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<host-name>)(PORT=1521))(CONNECT_DATA=(SID=<instance-name>)));User ID=<user-name>;Password=<password>"/>  
  
  </connection-string-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole Betrieb [Ausführen der Konsole SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Executing the SSMA Console (Ausführen der SSMA-Konsole)](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
