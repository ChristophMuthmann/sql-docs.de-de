---
title: "Konfigurieren eines Servers für die Überwachung einer alternativen Pipe | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: edc73b858a08ea0f8bda9e7a4d5ede8d2c05cccf
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe"></a>Konfigurieren eines Servers für die Überwachung einer alternativen Pipe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie einen Server konfigurieren können, um eine alternative Pipe in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers überwachen zu können. Standardmäßig lauscht die Standardinstanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] an der Named Pipe \\\\.\pipe\sql\query. Benannte Instanzen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] und [!INCLUDE[ssEW](../../includes/ssew-md.md)] überwachen andere Pipes.  
  
 Es gibt drei Möglichkeiten, mit einer Clientanwendung eine Verbindung mit einer bestimmten benannten Pipe herzustellen:  
  
-   Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienstes auf dem Server  
  
-   Erstellen eines Alias auf dem Client unter Angabe der benannten Pipe  
  
-   Programmieren Sie den Client so, dass die Verbindung mithilfe einer benutzerdefinierten Verbindungszeichenfolge hergestellt wird.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>So konfigurieren Sie die vom SQL Server-Datenbankmodul verwendete Named Pipe  
  
1.  Erweitern Sie im SQL Server-Konfigurations-Manager im Konsolenbereich **SQL Server-Netzwerkkonfiguration**, und klicken Sie dann auf **Protokolle für** *\<Instanzname>*.  
  
2.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Named Pipes**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Geben Sie auf der Registerkarte **Protokoll** im Feld **Pipename** die Pipe ein, an der [!INCLUDE[ssDE](../../includes/ssde-md.md)] gelauscht werden soll, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie im Konsolenbereich auf **SQL Server-Dienste**.  
  
5.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server (**\<Instanzname>**)**, und klicken Sie dann auf **Neu starten**, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu beenden und neu zu starten.  
  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine alternative Pipe überwacht, können Sie auf drei Arten mit einer Clientanwendung eine Verbindung zu einer bestimmten benannten Pipe herstellen:  
  
-   Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienstes auf dem Server  
  
-   Erstellen eines Alias auf dem Client unter Angabe der benannten Pipe  
  
-   Programmieren Sie den Client so, dass die Verbindung mithilfe einer benutzerdefinierten Verbindungszeichenfolge hergestellt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Server-Netzwerkkonfiguration](../../database-engine/configure-windows/server-network-configuration.md)  
  
  
