---
title: Konfigurieren von Clientprotokollen | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
caps.latest.revision: "35"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f9f3e68de28e6dd2052b2f0fd0f40acd5a167678
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="configure-client-protocols"></a>Konfigurieren von Clientprotokollen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird die Konfiguration von Clientprotokollen beschrieben, die mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers von Clientanwendungen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendet werden. Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Clientkommunikation mit TCP/IP und dem Named Pipes-Protokoll. Auch das Shared Memory-Protokoll steht zur Verfügung, wenn der Client eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz auf demselben Computer herstellt. Zum Auswählen des Protokolls stehen drei allgemeine Methoden zur Verfügung.  
  
-   Das Konfigurieren aller Clientanwendungen für dasselbe Netzwerkprotokoll durch Festlegen der Protokollreihenfolge im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager.  
  
-   Das Konfigurieren einer einzelnen Clientanwendung zum Verwenden eines anderen Netzwerkprotokolls durch Erstellen eines Alias. Weitere Informationen finden Sie unter [Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   In einigen Clientanwendungen, beispielsweise sqlcmd.exe, kann das Protokoll als Teil der Verbindungszeichenfolge angegeben werden. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit dem Datenbankmodul mithilfe von sqlcmd](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
###  <a name="EnableDisable"></a> So aktivieren oder deaktivieren Sie ein Clientprotokoll  
  
1.  Erweitern Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager **SQL Server Native Client-Konfiguration**, klicken Sie mit der rechten Maustaste auf **Clientprotokolle**, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Um ein Protokoll zu aktivieren, klicken Sie auf das gewünschte Protokoll im Feld **Deaktivierte Protokolle** , und klicken Sie dann auf **Aktivieren**.  
  
3.  Um ein Protokoll zu deaktivieren, klicken Sie auf das gewünschte Protokoll im Feld **Aktivierte Protokolle** , und klicken Sie dann auf **Deaktivieren**.  
  
###  <a name="ChangeDefault"></a> So ändern Sie das Standardprotokoll oder die Protokollreihenfolge für Clientcomputer  
  
1.  Erweitern Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager **SQL Server Native Client-Konfiguration**, klicken Sie mit der rechten Maustaste auf **Clientprotokolle**, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Soll die Reihenfolge der Protokolle beim Aufbauen einer Verbindung mit **geändert werden, klicken Sie im Feld** Aktivierte Protokolle **auf** Nach oben **bzw.**Nach unten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Das obere Protokoll im Feld **Aktivierte Protokolle** ist das Standardprotokoll.  
  
    > [!IMPORTANT]  
    >  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager erstellt Registrierungseinträge für die Serveraliaskonfigurationen und die Standard-Netzwerkbibliothek des Clients. Die Anwendung installiert jedoch weder die Clientnetzwerkbibliotheken noch die Netzwerkprotokolle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Clientnetzwerkbibliotheken werden im Rahmen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup installiert. Die Netzwerkprotokolle werden im Rahmen von Microsoft Windows Setup installiert (oder über die Anwendung **Netzwerk** in der **Systemsteuerung**). Als Teil von Windows Setup steht möglicherweise kein spezielles Netzwerkprotokoll zur Verfügung. Weitere Informationen zum Installieren dieser Netzwerkprotokolle finden Sie in der Dokumentation des Herstellers.  
  
###  <a name="Configure"></a> So konfigurieren Sie einen Client für die Verwendung von TCP/IP  
  
1.  Erweitern Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager **SQL Server Native Client-Konfiguration**, klicken Sie mit der rechten Maustaste auf **Clientprotokolle**, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Feld **Aktivierte Protokolle** auf die Pfeile, um die Reihenfolge zu ändern, in der mit den Protokollen versucht werden soll, eine Verbindung zu SQL Server herzustellen. Das obere Protokoll im Feld **Aktivierte Protokolle** ist das Standardprotokoll.  
  
 Das Shared Memory-Protokoll wird getrennt durch Aktivieren des Kästchens **Shared Memory-Protokoll aktivieren** aktiviert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren des Timeouts für Remoteanmeldungen (Serverkonfigurationsoption)](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
