---
title: Ausführen von Transaktionen in ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 872d7aca21569018180e537c635032a9d036e3dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connections-in-adomdnet---performing-transactions"></a>Verbindungen in ADOMD.NET - Ausführen von Transaktionen
  In ADOMD.NET verwenden Sie das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekt, um den Transaktionskontext für ein gegebenes <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt zu verwalten. Diese Funktionalität ermöglicht es Ihnen, mehrere Befehle vom gleichen Kontext auszuführen. Jeder Befehl liest die gleichen Daten, ohne dass sich die gelesenen Daten zwischen jeder Befehlsausführung ändern.  
  
> [!NOTE]  
>  Die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> Klasse ist die Implementierung von der **System.Data.IDbTransaction** Schnittstelle, Teil der [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Klassenbibliothek und implementiert, die von allen .NET Framework-Datenanbietern, die unterstützen Transaktionen.  
  
 Um Dirty Reads zu vermeiden, unterstützt das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekt nur Read Committed-Transaktionen, in denen während des Lesens der Daten freigegebene Sperren aufrecht erhalten werden.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> wird verwendet, um die Transaktion zu starten. Um die Transaktion zu verwenden, werden Befehle dann gegen die Verbindung ausgeführt, die die Transaktion gestartet hat. Wenn Sie mit der Transaktion fertig sind, können Sie entweder ein Rollback oder ein Commit für die Transaktion ausführen.  
  
## <a name="starting-a-transaction"></a>Starten einer Transaktion  
 Sie erstellen eine Instanz des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekts, indem Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A>-Methode des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekts aufrufen. Im folgenden Beispiel wird veranschaulicht, wie eine Instanz des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekts erstellt wird:  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>Ausführen von Rollbacks für eine Transaktion  
 Um ein Rollback für eine bestehende, unvollständige Transaktion auszuführen, rufen Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A>-Methode des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekts auf. Wenn Sie diese Methode für eine bestehende, vollständige Transaktion aufrufen, wird eine Ausnahme ausgelöst.  
  
## <a name="committing-a-transaction"></a>Commitausführung für eine Transaktion  
 Nachdem Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A>-Methode aufgerufen haben, um eine Transaktion zu starten, können Sie die Transaktion abschließen, indem Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A>-Methode des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekts aufrufen. Wird diese Methode für eine bestehende, vollständige Transaktion aufgerufen, wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [Aufbauen von Verbindungen in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)   
 [ADOMD.NET-Clientprogrammierung](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
