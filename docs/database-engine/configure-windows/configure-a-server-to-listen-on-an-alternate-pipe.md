---
title: "Konfigurieren eines Servers f&#252;r die &#220;berwachung einer alternativen Pipe (SQL Server-Konfigurations-Manager) | Microsoft Docs"
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
  - "Named Pipes [SQL Server], Konfigurieren"
  - "Lauschen [SQL Server], Pipes"
  - "Pipes [SQL Server], alternative"
  - "Alternative Pipes [SQL Server]"
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Konfigurieren eines Servers f&#252;r die &#220;berwachung einer alternativen Pipe (SQL Server-Konfigurations-Manager)
  In diesem Thema wird beschrieben, wie Sie einen Server konfigurieren können, um eine alternative Pipe in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers überwachen zu können. Standardmäßig lauscht die Standardinstanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] an der Named Pipe \\\\.\pipe\sql\query. Benannte Instanzen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] und [!INCLUDE[ssEW](../../includes/ssew-md.md)] überwachen andere Pipes.  
  
 Es gibt drei Möglichkeiten, mit einer Clientanwendung eine Verbindung mit einer bestimmten benannten Pipe herzustellen:  
  
-   Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienstes auf dem Server  
  
-   Erstellen eines Alias auf dem Client unter Angabe der benannten Pipe  
  
-   Programmieren Sie den Client so, dass die Verbindung mithilfe einer benutzerdefinierten Verbindungszeichenfolge hergestellt wird.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### So konfigurieren Sie die vom SQL Server-Datenbankmodul verwendete Named Pipe  
  
1.  Erweitern Sie im SQL Server-Konfigurations-Manager im Konsolenbereich **SQL Server-Netzwerkkonfiguration**, und klicken Sie dann auf **Protokolle für** *\<Instanzname>*.  
  
2.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Named Pipes**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Geben Sie auf der Registerkarte **Protokoll** im Feld **Pipename** die Pipe ein, an der [!INCLUDE[ssDE](../../includes/ssde-md.md)] gelauscht werden soll, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie im Konsolenbereich auf **SQL Server-Dienste**.  
  
5.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server (**\<Instanzname>**)**, und klicken Sie dann auf **Neu starten**, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu beenden und neu zu starten.  
  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine alternative Pipe überwacht, können Sie auf drei Arten mit einer Clientanwendung eine Verbindung zu einer bestimmten benannten Pipe herstellen:  
  
-   Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienstes auf dem Server  
  
-   Erstellen eines Alias auf dem Client unter Angabe der benannten Pipe  
  
-   Programmieren Sie den Client so, dass die Verbindung mithilfe einer benutzerdefinierten Verbindungszeichenfolge hergestellt wird.  
  
## Siehe auch  
 [Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/create or delete a server alias for use by a client.md)   
 [Server-Netzwerkkonfiguration](../../database-engine/configure-windows/server-network-configuration.md)  
  
  