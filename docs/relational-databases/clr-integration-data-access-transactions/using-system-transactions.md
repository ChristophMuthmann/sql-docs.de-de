---
title: Verwenden von System.Transactions | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40c3ac24cc6be800fea8da1fab407569e4cdab87
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-systemtransactions"></a>Verwenden von 'System.Transactions'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die **System.Transactions** Namespace bietet ein Transaktionsframework, die vollständig in ADO.NET integriert ist und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration der common Language Runtime (CLR). Die **System.Transactions.TransactionScope** -Klasse bewirkt, dass ein Codeblock transaktional wird, indem sie Verbindungen implizit in einer verteilten Transaktion einträgt. Sie müssen am Ende des Codeblocks, der durch **Complete** markiert wird, die **TransactionScope**-Methode aufrufen. Die **Dispose** -Methode wird aufgerufen, wenn die Programmausführung einen Codeblock verlässt, was dazu führt, dass die Transaktion nicht fortgeführt wird, wenn die **Complete** -Methode nicht aufgerufen wird. Wenn eine Ausnahme ausgelöst wurde, die dazu führt, dass der Code den Bereich verlässt, wird die Transaktion als nicht fortgeführt betrachtet.  
  
 Wir empfehlen die Verwendung eines **using** -Blocks um sicherzustellen, dass die **Dispose** -Methode für das **TransactionScope** -Objekt aufgerufen wird, wenn der **using** -Block verlassen wird. Wird für ausstehende Transaktionen kein Commit oder Rollback ausgeführt, wird die Leistung unter Umständen stark beeinträchtigt, da der Timeout für **TransactionScope** standardmäßig eine Minute beträgt. Wenn Sie keine **using** -Anweisung verwenden, müssen Sie alle Arbeiten in einem **Try** -Block ausführen und die **Dispose** -Methode im **Finally** -Block explizit aufrufen.  
  
 Wenn innerhalb von **TransactionScope**eine Ausnahme auftritt, wird die Transaktion als inkonsistent markiert und aufgegeben. Es wird ein Rollback für die Transaktion ausgeführt, wenn **TransactionScope** verworfen wird. Wenn keine Ausnahme auftritt, wird für teilnehmende Transaktionen ein Commit ausgeführt.  
  
 **TransactionScope** sollte nur verwendet werden, wenn auf lokale Datenquellen und Remotedatenquellen oder externe Ressourcen-Manager zugegriffen wird. Der Grund dafür ist, dass die **TransactionScope** -Klasse immer zur Höherstufung von Transaktionen führt, selbst dann, wenn sie nur innerhalb einer Kontextverbindung verwendet wird.  
  
> [!NOTE]  
>  Die **TransactionScope** -Klasse erstellt **System.Transactions.Transaction.IsolationLevel** standardmäßig mit dem Wert **Serializable** . Je nach Ihrer Anwendung kann es vorteilhaft sein, die Isolationsstufe herabzusetzen, um ein hohes Konfliktpotenzial in der Anwendung zu vermeiden.  
  
> [!NOTE]  
>  Es empfiehlt sich, nur Updates, Einfügungen und Löschungen innerhalb verteilter Transaktionen für Remoteserver auszuführen, da sie erhebliche Datenbankressourcen in Anspruch nehmen. Wenn der Vorgang auf dem lokalen Server ausgeführt werden soll, ist keine verteilte Transaktion notwendig, sondern es reicht eine lokale Transaktion aus. SELECT-Anweisungen sperren unter Umständen Datenbankressourcen, ohne dass dies erforderlich ist. Und in einigen Szenarien ist die Verwendung von Auswahlen möglicherweise notwendig. Jeder Arbeitsschritt, der nicht die Datenbank betrifft, sollte außerhalb des Transaktionsbereichs durchgeführt werden, sofern keine anderen Ressourcen-Manager von der Transaktion betroffen sind. Wenngleich eine Ausnahme innerhalb des Transaktionsbereichs ein Transaktionscommit verhindert, verfügt die **TransactionScope** -Klasse nicht über die Möglichkeit, außerhalb des Bereichs der Transaktion selbst ein Rollback von Änderungen auszuführen, die Ihr Code vorgenommen hat. Wenn Sie bestimmte Vorgänge beim Rollback der Transaktion ausführen möchten, müssen Sie eine eigene Implementierung der **System.Transactions.IEnlistmentNotification** -Schnittstelle schreiben und eine explizite Eintragung in die Transaktion vornehmen.  
  
## <a name="example"></a>Beispiel  
 Um mit **System.Transactions**zu arbeiten, müssen Sie über einen Verweis auf die Datei System.Transactions.dll verfügen.  
  
 Der nachfolgende Code zeigt, wie eine Transaktion erstellt wird, die für zwei verschiedene Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]heraufgestuft werden kann. Diese Instanzen werden durch zwei verschiedene **System.Data.SqlClient.SqlConnection** -Objekte dargestellt, die von einem **TransactionScope** -Block umschlossen werden. Der Code erstellt den **TransactionScope** -Block mit einer **using** -Anweisung und öffnet die erste Verbindung, wodurch sie automatisch im **TransactionScope**eingetragen wird. Die Transaktion wird anfänglich als einfache Transaktion, nicht als vollständig verteilte Transaktion, eingetragen. Der Code geht von der Existenz bedingter Logik aus (welche der Kürze halber weggelassen wurde). Er öffnet die zweite Verbindung nur, wenn es nötig ist, und trägt sie dann im **TransactionScope**ein. Wenn die Verbindung geöffnet wird, wird die Transaktion automatisch auf eine vollständig verteilte Transaktion hochgestuft. Der Code ruft dann **TransactionScope.Complete**auf, was zur Ausführung eines Commits für die Transaktion führt. Der Code gibt die beiden Verbindungen beim Beenden der **using** -Anweisungen für die Verbindungen frei. Die **TransactionScope.Dispose** -Methode für **TransactionScope** wird am Ende des **using** -Blocks für **TransactionScope**automatisch aufgerufen. Wenn an einem Punkt im **TransactionScope** -Block eine Ausnahme aufgetreten ist, wird **Complete** nicht aufgerufen, und für die verteilte Transaktion wird ein Rollback ausgeführt, sobald der **TransactionScope** gelöscht wird.  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CLR-Integration und -Transaktionen](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
