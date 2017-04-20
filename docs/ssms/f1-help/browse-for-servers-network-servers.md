---
title: Nach Servern suchen (Netzwerkserver) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0dfaef0364cf72e994b0fe5de778adc8a18bd715
ms.lasthandoff: 04/11/2017

---
# <a name="browse-for-servers-network-servers"></a>Nach Servern suchen (Netzwerkserver)
Wenn Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Komponente herstellen und nicht den genauen Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz kennen, klicken Sie im Feld **Servername** auf **Suche fortsetzen** , um das Dialogfeld **Nach Servern suchen** zu öffnen.  
  
Dieses Dialogfeld wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst aufgefüllt, sofern dieser auf den Servercomputern ausgeführt wird. Es gibt mehrere Gründe, warum der Name einer Instanz ggf. nicht in der Liste angezeigt wird:  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst wird auf dem Computer, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ausgeführt wird, möglicherweise nicht ausgeführt.  
  
-   UDP-Port 1434 wird möglicherweise von einer Firewall blockiert.  
  
-   Das **HideInstance** -Flag wurde möglicherweise festgelegt.  
  
Um eine Verbindung mit einer Instanz herzustellen, die nicht in der Liste angezeigt wird, geben Sie eine vollständige Verbindungszeichenfolge für die Instanz ein, einschließlich der TCP/IP-Portnummer oder des Pipenamens der Named Pipes.  
  
## <a name="options"></a>enthalten  
**Wählen Sie für Ihre Verbindung eine SQL Server-Instanz im Netzwerk aus**  
Legen Sie den Server fest, zu dem eine Verbindung hergestellt werden soll, indem Sie auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz klicken, die in der Baumstruktur angezeigt wird. Sie können Teile der Strukturansicht durch Klicken auf die Knoten ein- bzw. ausblenden, die mit den Symbolen **+** bzw. **–** gekennzeichnet sind.  
  

