---
title: SQL Server Native Client-Konfigurationseigenschaften (Registerkarte "Flags") | Microsoft Docs
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
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
caps.latest.revision: "17"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30942b3a880515d7286a6a44b3fec53cab7443f3
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client-Konfigurationseigenschaften (Registerkarte Flags)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Clients auf diesem Computer die Kommunikation mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Servern mithilfe der Protokolle der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Bibliotheksdatei. Mithilfe dieser Seite wird der Clientcomputer so konfiguriert, dass die Anforderung einer verschlüsselten Verbindung mit Secure Sockets Layer (SSL) möglich ist. Wenn keine verschlüsselte Verbindung hergestellt werden kann, führt dies zu einem Verbindungsfehler.  
  
 Der Anmeldeprozess ist immer verschlüsselt. Die unten genannten Optionen gelten nur für verschlüsselte Daten. Weitere Informationen zur Verschlüsselungsart der Kommunikation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und zu Konfigurationsanweisungen für den Client, damit dieser die Stammzertifizierungsstelle des Serverzertifikats als vertrauenswürdig einstuft, finden Sie unter „Verschlüsseln von Verbindungen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]“ und „Gewusst wie: Aktivieren von Verschlüsselungsverbindungen für [!INCLUDE[ssDE](../../includes/ssde-md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager)“ in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="options"></a>enthalten  
 **ForceEncryption**  
 Fordern Sie eine Verbindung über SSL an.  
  
 **TrustServerCertificate**  
 Wenn diese Option auf **Nein**festgelegt ist, versucht der Clientprozess, das Serverzertifikat zu überprüfen. Client und Server müssen jeweils über ein Zertifikat von einer öffentlichen Zertifizierungsstelle verfügen. Wenn dieses Zertifikat auf dem Clientcomputer nicht vorhanden ist oder bei der Überprüfung des Zertifikats ein Fehler erzeugt wird, wird die Verbindung beendet.  
  
 Wenn diese Option auf **Ja**festgelegt ist, überprüft der Client das Serverzertifikat nicht. Dadurch wird die Verwendung eines selbstsignierten Zertifikats ermöglicht.  
  
 Das**TrustServerCertificate** -Flag ist nur verfügbar, wenn das **ForceEncryption** -Flag auf **Ja**festgelegt ist.  
  
  
