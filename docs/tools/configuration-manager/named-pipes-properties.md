---
title: "Named Pipes-Eigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pipes [SQL Server]"
  - "Lauschen [SQL Server], Pipes"
  - "Pipes [SQL Server], Lauschen an Pipes"
  - "Named Pipes [SQL Server], Lauschen an Pipes"
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Named Pipes-Eigenschaften
  Verwenden Sie die Seite **Protokoll**im Dialogfeld **Named Pipes-Eigenschaften** , um die Named Pipe anzuzeigen oder zu ändern, die von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verwenden des Named Pipes-Protokoll überwacht wird.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss neu gestartet werden, um das Protokoll zu aktivieren oder zu deaktivieren oder die Named Pipe zu ändern.  
  
## enthalten  
 **Enabled**  
 Mögliche Werte sind **Ja** und **Nein**.  
  
 **Pipename**  
 Gibt die Named Pipe an, an der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelauscht wird. Standardmäßig lauscht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] folgende: `\\.\pipe\sql\query` nach der Standardinstanz und `\\.\pipe\MSSQL$<instancename>\sql\query` nach einer benannten Instanz. Dieses Feld ist auf 2047 Zeichen begrenzt.  
  
## Erstellen einer alternativen Named Pipe  
 Zum Ändern der Named Pipe geben Sie im Feld **Pipename** einen neuen Pipenamen ein. Beenden Sie anschließend [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und führen Sie einen Neustart aus. Da **sql\query** bekannt ist als Named Pipe, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, kann eine Änderung der Pipe das Risiko eines Angriffs durch böswillige Programme reduzieren.  
  
### Beispiel  
 Geben Sie **\\\\.\pipe\unit\app** ein, um an der Pipe **unit\app** zu lauschen.  
  
 Geben Sie **\\\\.\pipe\acct** ein, um an der Pipe **acct** zu lauschen.  
  
## Siehe auch  
 [Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [Auswählen eines Netzwerkprotokolls](../Topic/Choosing%20a%20Network%20Protocol.md)   
 [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von Named Pipes](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md)  
  
  