---
title: "Erstellen einer gültigen Verbindungszeichenfolge mithilfe des Shared Memory-Protokoll | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64005912a185443249487d710eeb6d8a7630ed1f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>Erstellen einer gültigen Verbindungszeichenfolge mithilfe des Shared Memory-Protokolls
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Verbindungen mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem Client auf demselben Computer ausgeführt wird, verwenden das shared Memory-Protokoll. Shared Memory verfügt über keine konfigurierbaren Eigenschaften. Es wird immer zuerst versucht, Shared Memory zu verwenden; es ist nicht möglich, dieses Protokoll von der obersten Position der Liste **Aktivierte Protokolle** in der Liste **Eigenschaften der Clientprotokolle** zu verschieben. Das Shared Memory-Protokoll kann deaktiviert werden, was insbesondere bei der Problembehandlung eines der anderen Protokolle nützlich ist.  
  
 Sie können keinen Alias mithilfe des Shared Memory-Protokolls erstellen. Allerdings wird bei aktiviertem Shared Memory über den namentlichen Verbindungsaufbau zu [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Shared Memory-Verbindung hergestellt. Für Shared Memory-Verbindungszeichenfolgen wird das Format `lpc:<servername>[\instancename]`verwendet.  
  
## <a name="connecting-to-the-local-server"></a>Herstellen einer Verbindung mit dem lokalen Server  
 Beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , das auf dem gleichen Computer wie der Client ausgeführt wird, können Sie **(local)** als Servernamen verwenden. Aus Gründen der Mehrdeutigkeit wird dies nicht empfohlen, kann aber nützlich sein, wenn vom Client bekannt ist, dass er auf dem vorgesehenen Computer ausgeführt wird. Beim Erstellen einer Anwendung für mobile Benutzer mit getrennter Verbindung (beispielsweise für Verkaufspersonal, wobei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Laptops ausgeführt und zum Speichern von Projektdaten verwendet wird) würde beispielsweise die Verbindung eines Clients zu **(local)** immer zu dem auf dem Laptop ausgeführten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt. Anstelle von **(local)** kann das Wort**localhost**oder ein Punkt ( **.**) verwendet werden.  
  
## <a name="verifying-your-connection-protocol"></a>Überprüfen Ihres Verbindungsprotokolls  
 Von der folgenden Abfrage wird das Protokoll zurückgegeben, das für die aktuelle Verbindung verwendet wird.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Beispiele:  
 Die folgenden Namen werden mit dem lokalen Computer mithilfe des Shared Memory-Protokolls verbunden, falls dieses aktiviert ist:  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 Sie können keinen Alias für eine Shared Memory-Verbindung erstellen.  
  
> [!NOTE]  
>  Die Angabe einer IP-Adresse im Feld **Server** führt zu einer TCP/IP-Verbindung.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)   
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
