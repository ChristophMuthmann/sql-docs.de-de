---
title: "Implementierung des &#252;bergeordneten Pakets | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Übergeordnete Pakete [Integration Services]"
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Implementierung des &#252;bergeordneten Pakets
  Beim Lastenausgleich von SSIS-Paketen über verschiedene Server ist der nächste Schritt das Erstellen des übergeordneten Pakets, nachdem die untergeordneten Pakete erstellt, bereitgestellt und für ihre Ausführung Remoteaufträge des SQL Server-Agents erstellt wurden. Das übergeordnete Paket enthält dann mehrere Tasks Auftrag des SQL Server-Agents ausführen, wobei die einzelnen Tasks jeweils einen Auftrag des SQL Server-Agents zum Ausführen eines der untergeordneten Pakete aufrufen. Die im übergeordneten Paket enthaltenen Tasks Auftrag des SQL Server-Agents ausführen führen wiederum die verschiedenen Aufträge des SQL Server-Agents aus. Jeder einzelne Task des übergeordneten Pakets enthält Informationen, z. B. über das Herstellen einer Verbindung zum Remoteserver sowie über den auf diesem Server auszuführenden Auftrag. Weitere Informationen finden Sie unter [Execute SQL Server Agent Job Task](../../integration-services/packages/execute-sql-server-agent-job-task.md).  
  
 Um das übergeordnete Paket zu identifizieren, das untergeordnete Pakete ausführt, klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mit der rechten Maustaste auf das Paket in Projektmappen-Explorer, und klicken Sie dann auf **Einstiegspunktpaket**.  
  
## Auflisten untergeordneter Pakete  
 Wenn Sie ein Projekt, das ein übergeordnetes Paket und untergeordnete Pakete enthält, über den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitstellen, können Sie eine Liste der untergeordneten Pakete anzeigen lassen, die von den übergeordneten Paketen ausgeführt werden. Wenn Sie das übergeordnete Paket ausführen, wird automatisch für das übergeordnete Paket ein Bericht **Übersicht** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellt. Der Bericht führt die untergeordneten Pakete auf, die vom Task "Paket ausführen" ausgeführt wurden, der sich im übergeordneten Paket befindet. Dies wird im folgenden Bild gezeigt.  
  
 ![Übersichtsbericht mit Liste der untergeordneten Pakete](../../integration-services/packages/media/overviewreport-childpackagelisting.png "Übersichtsbericht mit Liste der untergeordneten Pakete")  
  
 Weitere Informationen zum Zugreifen auf den Bericht **Übersicht** finden Sie unter [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
## Rangfolgeneinschränkungen im übergeordneten Paket  
 Wenn Sie im übergeordneten Paket zwischen den Tasks "Task 'Auftrag des SQL Server-Agents ausführen'" Rangfolgeneinschränkungen erstellen, steuern diese nur die Startzeit der Aufträge des SQL Server-Agents auf den Remoteservern. Rangfolgeneinschränkungen können keine Informationen bezüglich des Erfolgs oder Misserfolgs der untergeordneten Pakete empfangen, die in den Schritten der Aufträge des SQL Server-Agents ausgeführt werden.  
  
 Das bedeutet, dass der Erfolg oder Misserfolg eines untergeordneten Pakets nicht an das übergeordnete Paket weitergegeben wird, da die einzige Funktion des Tasks Auftrag des SQL Server-Agents ausführen im übergeordneten Paket darin besteht, den Auftrag des SQL Server-Agents für die Ausführung des untergeordneten Pakets anzufordern. Nach dem erfolgreichen Aufruf des Auftrags des SQL Server-Agents empfängt das übergeordnete Paket das Ergebnis <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success>.  
  
 Der Misserfolg dieses Szenarios bedeutet nur, dass beim Remoteaufruf des Tasks Auftrag des SQL Server-Agents ein Fehler aufgetreten ist. Dies kann z. B. vorkommen, wenn der Remoteserver ausgefallen ist und der Agent nicht antwortet. Allerdings kann das übergeordnete Paket seinen Task erfolgreich abschließen, solange der Agent ausgelöst wird.  
  
> [!NOTE]  
>  Sie können den Task „SQL ausführen“ verwenden, in dem die Transact-SQL-Anweisung **sp_start_job N'package_name'** enthalten ist. Weitere Informationen finden Sie unter [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).  
  
## Debugging-Umgebung  
 Verwenden Sie beim Testen des übergeordneten Pakets die Umgebung des Designers zum Debuggen, indem Sie im Menü Debuggen auf Debuggen starten klicken oder F5 drücken. Alternativ können Sie das Eingabeaufforderungs-Hilfsprogramm **dtexec**verwenden. Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
  