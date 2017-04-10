---
title: "Implementierung von untergeordneten Paketen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Untergeordnete Pakete"
ms.assetid: ab0c09d7-ce2e-487d-a1ed-a4b5adb6cc01
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Implementierung von untergeordneten Paketen
  Wenn Sie mithilfe von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]den Lastenausgleich implementieren, werden die untergeordneten Pakete auf anderen Servern installiert, um die verfügbare CPU bzw. die Serverzeit zu nutzen. Für das Erstellen und Ausführen der untergeordneten Pakete sind die folgenden Schritte erforderlich:  
  
-   Entwerfen der untergeordneten Pakete.  
  
-   Verschieben der Pakete auf den Remoteserver.  
  
-   Erstellen eines Auftrags des SQL Server-Agents auf dem Remoteserver, der einen Schritt zum Ausführen des untergeordneten Pakets enthält.  
  
-   Testen und Debuggen des Auftrags des SQL Server-Agents und der untergeordneten Pakete.  
  
 Beim Entwerfen der untergeordneten Pakete sind die Entwurfsmöglichkeiten unbegrenzt. Dabei können Sie jede beliebige Funktionalität verwenden. Beim Zugriff des Pakets auf die Daten müssen Sie jedoch sicherstellen, dass der Server, mit dem das Paket ausgeführt wird, auf die Daten zugreifen kann.  
  
 Um das übergeordnete Paket zu identifizieren, das untergeordnete Pakete ausführt, klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mit der rechten Maustaste auf das Paket in Projektmappen-Explorer, und klicken Sie dann auf **Einstiegspunktpaket**.  
  
 Nach dem Entwerfen der untergeordneten Pakete werden diese im nächsten Schritt auf den Remoteservern bereitgestellt.  
  
## Verschieben des untergeordneten Pakets auf die Remoteinstanz  
 Es gibt mehrere Möglichkeiten zum Verschieben von Paketen auf andere Server. Es werden die folgenden zwei Methoden vorgeschlagen:  
  
-   Exportieren von Paketen mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Bereitstellen von Paketen durch Erstellen eines Bereitstellungshilfsprogramms für das Projekt, in dem die bereitzustellenden Pakete enthalten sind, und anschließendes Ausführen des Paketinstallations-Assistenten zum Installieren der Pakete im Dateisystem bzw. in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Sie müssen die Bereitstellung für jeden zu verwendenden Remoteserver wiederholen.  
  
## Erstellen der Aufträge des SQL Server-Agents  
 Nach dem Bereitstellen der untergeordneten Pakete auf verschiedenen Servern müssen Sie auf jedem Server, auf dem ein untergeordnetes Paket enthalten ist, einen Auftrag des SQL Server-Agents erstellen. Der Auftrag des SQL Server-Agents enthält einen Schritt zum Ausführen der untergeordneten Pakete beim Aufruf des Agentauftrags. Die Aufträge des SQL Server-Agents sind keine geplanten Aufträge. Sie führen die untergeordneten Pakete nur dann aus, wenn Sie vom übergeordneten Paket aufgerufen werden. Die Benachrichtigung über den Erfolg oder Misserfolg des Auftrags an das übergeordnete Paket spiegelt den Erfolg oder Misserfolg des Auftrags des SQL Server-Agents wider und gibt an, ob der Auftrag erfolgreich aufgerufen wurde. Die Benachrichtigung beinhaltet jedoch nicht den Erfolg oder Misserfolg des untergeordneten Pakets bzw. eine Benachrichtigung, ob das Paket ausgeführt wurde.  
  
## Debuggen der Aufträge des SQL Server-Agents und der untergeordneten Pakete  
 Sie können die Aufträge des SQL Server-Agents und ihre untergeordneten Pakete testen, indem Sie eine der folgenden Methoden verwenden:  
  
-   Ausführen der einzelnen untergeordneten Pakete im SSIS-Designer, indem Sie im Menü **Debuggen** / **Starten ohne Debugging**.  
  
-   Ausführen der einzelnen Aufträge des SQL Server-Agents auf dem Remotecomputer mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um sicherzustellen, dass die Pakete ausgeführt werden.  
  
 Weitere Informationen zur Fehlerbehebung bei der Ausführung von Paketen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträgen finden Sie unter [SSIS-Paket wird nicht ausgeführt, wenn das SSIS-Paket von einem SQL Server-Agent-Auftrag abgerufen wird](http://support.microsoft.com/kb/918760) in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base für Support.  
  
 Vom SQL Server-Agent wird der Subsystemzugriff für einen Proxy überprüft und der Zugriff auf den Proxy jedes Mal gewährt, wenn der Auftragsschritt ausgeführt wird.  
  
 Sie können einen Proxy in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen.  
  
## Verwandte Aufgaben  
  
-   [Ausführen eines Pakets auf dem SSIS-Server mit SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  