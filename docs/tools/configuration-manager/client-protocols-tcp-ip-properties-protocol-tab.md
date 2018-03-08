---
title: Clientprotokolle - TCP / IP-Eigenschaften (Registerkarte Protokoll) | Microsoft Docs
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
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1fa2175534441ab464452a1f549833742daaa185
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="client-protocols---tcp-ip-properties-protocol-tab"></a>Client Protocols - TCP IP Properties (Protocol Tab)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Verwenden Sie im Konfigurations-Manager von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Dialogfeld **Eigenschaften von TCP/IP** die Registerkarte **Protokoll** , um die folgenden Optionen anzuzeigen oder anzugeben. Zum Herstellen einer Verbindung mit einem anderen Port geben Sie die Portnummer im Dialogfeld **Standardport** ein. Weitere Informationen zu Verbindungszeichenfolgen finden Sie unter [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md).  
  
## <a name="options"></a>enthalten  
 **Standardport**  
 Gibt den Standardport an, der von der TCP/IP-Netzwerkbibliothek zum Herstellen einer Verbindung mit der Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet wird. Der Standardport ist 1433.  
  
 Beim Verbinden mit einer Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]verwendet der Client diesen Wert. Wenn die Standardinstanz zur Überwachung eines anderen Ports konfiguriert wurde, ändern Sie diesen Wert in diese Portnummer.  
  
 Beim Herstellen einer Verbindung mit einer benannten Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]versucht der Client, die Portnummer vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst zu erhalten, der auf dem Servercomputer ausgeführt wird. Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst nicht ausgeführt wird, muss die Portnummer über diese Einstellung oder in der Verbindungszeichenfolge angegeben werden.  
  
 **Aktiviert**  
 Mögliche Werte sind **Yes** und **No**.  
  
 **Keep Alive**  
 Dieser Parameter steuert, wie oft (in Millisekunden) TCP durch das Senden eines **KEEPALIVE** -Pakets zu überprüfen versucht, ob eine Verbindung im Leerlauf noch reagiert. Der Standardwert beträgt 30000 Millisekunden.  
  
 **Erhaltungsintervall**  
 Dieser Parameter bestimmt das Intervall (in Millisekunden), das **KEEPALIVE** -Pakete voneinander trennt, bis eine Antwort erhalten wird. Der Standardwert beträgt 1.000 Millisekunden.  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Neuer Alias &#40; Registerkarte "Alias" &#41;](../../tools/configuration-manager/new-alias-alias-tab.md)   
 [&#60;Alias&#62;-Eigenschaften &#40;Registerkarte „Alias“&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)  
  
  
