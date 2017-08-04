---
title: "Ausführen der Schritte nach der Installation | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 14df01be1d7298be68b3d358d33662c55821279a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="complete-the-post-installation-steps"></a>Ausführen der Schritte nach der Installation
  Nach der Installation von Distributed Replay müssen Sie die Distributed Replay Controller und -Client-Dienstkonten ändern.  
  
### <a name="to-complete-the-post-installation-steps"></a>So führen Sie die Schritte nach der Installation aus  
  
1.  **Erstellen Sie Firewallregeln**: Auf den Controller- und Clientcomputern müssen Sie für den entsprechenden Dienst den eingehenden Datenverkehr durch die Firewall zulassen. Geben Sie die Firewallregeln für die ausführbaren Dienstdateien an, die sich in den Installationsordnern befinden.  
  
    1.  Erstellen Sie für den Controllerdienst eine Regel für **DReplayController.exe**. Diese Datei befindet sich im Installationsordner. Mit dem folgenden Befehl aktivieren Sie beispielsweise diese Regel, wobei `%InstallPath%` den Installationsordner des Diensts darstellt:  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  Erstellen Sie für den Clientdienst auf jedem Clientcomputer eine Regel für **DReplayClient.exe**. Diese Datei befindet sich im Installationsordner. Mit dem folgenden Befehl aktivieren Sie beispielsweise diese Regel, wobei `%InstallPath%` den Installationsordner des Diensts darstellt:  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **Erteilen Sie jedem Client Berechtigungen für den Zielserver**: Wenn Sie die Installation des Clientdiensts auf den Clientcomputern abgeschlossen haben, müssen Sie der sysadmin-Rolle für die Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]manuell die Clientdienstkonten hinzufügen.  
  
## <a name="net-framework-security"></a>.NET Framework-Sicherheit  
 Sie müssen über Administratorberechtigungen verfügen, um eine der Distributed Replay-Funktionen zu installieren. Nur bei einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung mit sysadmin-Berechtigungen können der sysadmin-Serverrolle des Testservers die Clientdienstkonten hinzugefügt werden. Weitere Informationen zu Sicherheitsüberlegungen für Distributed Replay finden Sie unter [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
  
