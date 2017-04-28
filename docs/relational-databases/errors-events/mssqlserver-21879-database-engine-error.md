---
title: MSSQLSERVER_21879 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4850aeaa925fa4aa74659d9a242c1972e7dbb0de
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver21879"></a>MSSQLSERVER_21879
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21879|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLErrorNum21879|  
|Meldungstext|Der umgeleitete Server '%s' kann nicht nach dem ursprünglichen Verleger '%s' und der Verlegerdatenbank '%s' abgefragt werden, um den Namen des Remoteservers zu bestimmen; Fehler %d, Fehlermeldung '%s.'|  
  
## <a name="explanation"></a>Erklärung  
**sp_validate_redirected_publisher** verwendet einen temporären Verbindungsserver, der erstellt wird, um eine Verbindung mit dem umgeleiteten Verleger herzustellen und den Namen des Remoteservers zu ermitteln. Fehler 21879 wird zurückgegeben, wenn die Verbindungsserverabfrage fehlschlägt. In dem Aufruf, mit dem der Remoteservername angefordert wird, wird der temporäre Verbindungsserver in der Regel zum ersten Mal verwendet. Wenn Verbindungsprobleme vorliegen, ist es daher wahrscheinlich, dass diese zuerst in diesem Aufruf augenscheinlich werden. Dieser Remoteaufruf führt auf dem Remoteserver einfach select **@@servername** aus.  
  
Für den Verbindungsserver, der zum Abfragen des umgeleiteten Verlegers verwendet wird, werden der Sicherheitsmodus, die Anmeldung und das Kennwort verwendet, die beim Aufruf von **sp_adddistpublisher** für den ursprünglichen Verleger angegeben wurden.  
  
-   Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung (Sicherheitsmodus 0) verwendet wurde, dann werden die angegebene Anmeldung und das Kennwort verwendet, um eine Verbindung mit dem Remoteserver herzustellen.  
  
-   Wurde die Windows-Authentifizierung (Sicherheitsmodus 1) verwendet, dann wird eine vertrauenswürdige Verbindung zum Herstellen der Verbindung genutzt.  
  
    -   Wenn **sp_validate_redirected_publisher** explizit von einem Benutzer aufgerufen wird, wird die Windows-Anmeldung, unter der der Benutzer Windows ausführt, für die Verbindung verwendet.  
  
    -   Wenn **sp_validate_redirected_**publisher von einem Replikations-Agent von **sp_get_redirected_publisher** aufgerufen wird, wird die dem Agent zugeordnete Windows-Anmeldung verwendet.  
  
Fehler 21879 kann darauf hinweisen, dass **sp_validate_redirected_publisher** mit einer Anmeldung aufgerufen wurde, die beim umgeleiteten Zielverleger nicht bekannt ist.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie sicher, dass die Anmeldung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung oder die Windows-Authentifizierung bei allen Verfügbarkeitsgruppenreplikaten gültig und autorisiert ist, auf die Abonnementmetadatentabellen (syssubscriptions und sysmergesubscriptions) in der Verlegerdatenbank zuzugreifen.  
  
Es sind einige besondere Dinge zu beachten, wenn der Fehler 21879 von einem Aufruf von **sp_get_redirected_publisher** zurückgegeben wird, der von einem Replikations-Agent initiiert worden ist, der auf einem anderen Knoten als dem Verteiler ausgeführt wird; z.B. einem Merge-Agent, der auf einem Abonnenten läuft. Wenn Windows-Authentifizierung für die Verbindung zum umgeleiteten Verleger verwendet wird, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Kerberos-Authentifizierung konfiguriert worden sein, damit erfolgreich eine Verbindung hergestellt werden kann. Wenn die Windows-Authentifizierung verwendet wird und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht für die Kerberos-Authentifizierung konfiguriert worden ist, dann wird der Fehler 18456 an einen Merge-Agent ausgegeben, der auf dem Abonnenten ausgeführt wird. Dieser Fehler gibt an, dass die Anmeldung 'NT AUTHORITY\ANONYMOUS LOGON' fehlgeschlagen ist. Dieses Problem kann auf drei Arten behandelt werden:  
  
-   Konfigurieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Kerberos-Authentifizierung Weitere Informationen finden Sie unter **Kerberos-Authentifizierung und SQL Server** in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
-   Verwenden Sie **sp_changedistpublisher**, um den dem ursprünglichen Verleger in MSdistpublishers zugeordneten Sicherheitsmodus zu ändern sowie um eine Anmeldung und ein Kennwort anzugeben, die für die Verbindung verwendet werden sollen.  
  
-   Geben Sie den Befehlszeilenparameter *BypassPublisherValidation* in der Merge-Agent-Befehlszeile an, um die Überprüfung zu umgehen, wenn **sp_get_redirected_publisher** beim Verteiler aufgerufen wird.  
  

