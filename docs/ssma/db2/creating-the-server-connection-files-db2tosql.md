---
title: Erstellen die Server-Connection-Dateien (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c49bcf7ccc71e5e2b441ec4e9bfcdbbdc2dd62e6
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="creating-the-server-connection-files-db2tosql"></a>Erstellen die Server-Connection-Dateien (DB2ToSQL)
Informationen zum Server kann entweder im Bereich "Server" der Skriptdatei oder in einem separaten Server Verbindungsdatei angegeben werden. Die Befehlszeilenparameter für die Server-Verbindungsdatei ist, `-c <serverconnectionfile>`. Wenn die gleiche Id in der Skriptdatei und die Verbindungsdatei Server vorhanden ist, wird die Definition des Servers in der Skriptdatei angesehen.  
  
**Beispiel: 1**  
  
```  
<!--Sample of server connection file commands -->  
  
<db2 name="<source-server-unique-name>">  
  
    <standard-mode>  
  
      <connection-provider value ="OleDB Provider"/>  
  
      <!-- Defines server manager to connect.  
  
              Available manager attribute values  
  
              • zOs      - upgrades the project (default)  
  
              • LUW       - displays an error and halts the execution-->  
  
      <database-manager value="$Db2Manager$"/>  
  
      <server-name value="$Db2HostName$" />  
  
      <port value="$Db2Port$" />  
  
      <initial-catalog value="$Db2Instance$" />  
  
      <user-id value="$Db2UserName$" />  
  
      <password value="$Db2Password$"/>  
  
    </standard-mode>  
  
</db2>  
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
Im nächsten Schritt in der Konsole funktioniert [Ausführen der Konsole SSMA &#40; DB2ToSQL &#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der SSMA-Konsole](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  

