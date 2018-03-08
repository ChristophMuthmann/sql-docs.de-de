---
title: Named Pipes-Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a8a88c3d7f54d4bf31cb5256e52d8257297ae91
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="named-pipes-properties"></a>Named Pipes-Eigenschaften
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Verwenden Sie die Seite **Protokoll**im Dialogfeld **Named Pipes-Eigenschaften** , um die Named Pipe anzuzeigen oder zu ändern, die von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verwenden des Named Pipes-Protokoll überwacht wird.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss neu gestartet werden, um das Protokoll zu aktivieren oder zu deaktivieren oder die Named Pipe zu ändern.  
  
## <a name="options"></a>enthalten  
 **Enabled**  
 Mögliche Werte sind **Ja** und **Nein**.  
  
 **Pipename**  
 Gibt die Named Pipe an, an der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelauscht wird. Standardmäßig lauscht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] folgende: `\\.\pipe\sql\query` nach der Standardinstanz und `\\.\pipe\MSSQL$<instancename>\sql\query` nach einer benannten Instanz. Dieses Feld ist auf 2047 Zeichen begrenzt.  
  
## <a name="creating-an-alternate-named-pipe"></a>Erstellen einer alternativen Named Pipe  
 Zum Ändern der Named Pipe geben Sie im Feld **Pipename** einen neuen Pipenamen ein. Beenden Sie anschließend [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und führen Sie einen Neustart aus. Da **sql\query** bekannt ist als Named Pipe, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet wird, kann eine Änderung der Pipe das Risiko eines Angriffs durch böswillige Programme reduzieren.  
  
### <a name="example"></a>Beispiel  
 Geben Sie **\\\\.\pipe\unit\app** ein, um an der Pipe **unit\app** zu lauschen.  
  
 Geben Sie **\\\\.\pipe\acct** ein, um an der Pipe **acct** zu lauschen.  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
