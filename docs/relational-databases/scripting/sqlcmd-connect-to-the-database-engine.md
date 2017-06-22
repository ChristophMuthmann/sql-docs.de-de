---
title: "Herstellen einer Verbindung mit dem Datenbankmodul mithilfe von „sqlcmd“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cccbf7d6ae6b1b999ab3f08eff2aee1771293c7f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sqlcmd---connect-to-the-database-engine"></a>Herstellen einer Verbindung mit dem Datenbankmodul mithilfe von „sqlcmd“
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Clientkommunikation mit dem TCP/IP-Netzwerkprotokoll (Standardeinstellung) und dem Named Pipes-Protokoll. Auch das Shared Memory-Protokoll steht zur Verfügung, wenn der Client eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz auf demselben Computer herstellt. Zum Auswählen des Protokolls stehen drei allgemeine Methoden zur Verfügung. Das vom **sqlcmd** -Hilfsprogramm verwendete Protokoll wird in der folgenden Reihenfolge bestimmt:  
  
-   **sqlcmd** verwendet das Protokoll, das wie unten beschrieben als Teil der Verbindungszeichenfolge angegeben ist.  
  
-   Wenn kein Protokoll als Teil der Verbindungszeichenfolge angegeben ist, verwendet **sqlcmd** das Protokoll, das als Teil des Alias definiert ist, mit dem eine Verbindung hergestellt wird. Informationen dazu, wie Sie **sqlcmd** durch das Erstellen eines Alias für die Verwendung eines bestimmten Netzwerkprotokolls konfigurieren, finden Sie unter [Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   Wenn das Protokoll nicht auf andere Weise definiert ist, verwendet **sqlcmd** das Netzwerkprotokoll, das durch die Protokollreihenfolge im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager bestimmt wird.  
  
 In den folgenden Beispielen werden verschiedene Möglichkeiten für das Herstellen einer Verbindung mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Standardinstanz über Port 1433 und mit benannten [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanzen veranschaulicht, die an Port 1691 lauschen sollen. In einigen dieser Beispiele wird die IP-Adresse des Loopbackadapters (127.0.0.1) verwendet. Testen Sie diese Einstellung mithilfe der IP-Adresse der Computer-Netzwerkschnittstellenkarte.  
  
 Stellen Sie eine Verbindung zu [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, indem Sie den Namen der Instanz angeben:  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 Stellen Sie eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, indem Sie die IP-Adresse angeben:  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 Stellen Sie eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, indem Sie die TCP/IP-Portnummer angeben:  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>So stellen Sie eine Verbindung über TCP/IP her  
  
-   Stellen Sie eine Verbindung mithilfe der folgenden allgemeinen Syntax her:  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   Stellen Sie eine Verbindung mit der Standardinstanz her:  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   Stellen Sie eine Verbindung mit einer benannten Instanz her:  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>So stellen Sie eine Verbindung mithilfe von Named Pipes her  
  
-   Stellen Sie eine Verbindung mithilfe einer der folgenden allgemeinen Syntaxangaben her:  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   Stellen Sie eine Verbindung mit der Standardinstanz her:  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   Stellen Sie eine Verbindung zu einer benannten Instanz her:  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>So stellen Sie eine Verbindung mithilfe des Shared Memory-Protokolls (einem lokalen Prozeduraufruf) von einem Client auf dem Server her  
  
-   Stellen Sie eine Verbindung mithilfe einer der folgenden allgemeinen Syntaxangaben her:  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   Stellen Sie eine Verbindung mit der Standardinstanz her:  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   Stellen Sie eine Verbindung mit einer benannten Instanz her:  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
