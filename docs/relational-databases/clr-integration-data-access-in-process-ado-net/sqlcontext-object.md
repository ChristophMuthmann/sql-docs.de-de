---
title: SqlContext-Objekt | Microsoft Docs
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
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: "54"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70a25a1b656e20ff7d2457df581a3a1b94ee3b9a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sqlcontext-object"></a>SqlContext-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Beim Aufrufen einer Prozedur oder Funktion, wenn Sie eine Methode in einer common Language Runtime (CLR) den benutzerdefinierten Typ aufrufen, oder wenn Ihre Aktion einen in einer der definierten Trigger auslöst, rufen Sie verwalteten Code auf dem Server die [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Sprachen. Da die Ausführung dieses Codes im Rahmen einer Benutzerverbindung erforderlich ist, wird ein Zugriff auf den Kontext des aufrufenden Codes vonseiten des auf dem Server ausgeführten Code benötigt. Zusätzlich dazu sind bestimmte Datenzugriffsvorgänge unter Umständen nur gültig, wenn sie im Kontext des aufrufenden Programms ausgeführt werden. Beispielsweise ist der Zugriff auf in Triggervorgängen verwendete eingefügte und gelöschte Pseudotabellen nur im Kontext des aufrufenden Codes gültig.  
  
 Der Kontext des aufrufenden Codes wird in einem **SqlContext** -Objekt abstrahiert. Weitere Informationen zu den **SqlTriggerContext** Methoden und Eigenschaften finden Sie unter der **Microsoft.SqlServer.Server.SqlTriggerContext** -Klasse Referenzdokumentation finden Sie in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** stellt den Zugriff auf folgende Komponenten bereit:  
  
-   **SqlPipe**: Das **SqlPipe** -Objekt stellt die "Pipe" dar, d. h. den Kanal, durch den die Ergebnisse den Client erreichen. Weitere Informationen zu den **SqlPipe** Objekt, finden Sie unter [SqlPipe-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: Das **SqlTriggerContext** -Objekt kann nur innerhalb eines CLR-Triggers abgerufen werden. Es stellt Informationen über den Vorgang bereit, durch den der Trigger ausgelöst wurde, sowie eine Übersicht der aktualisierten Spalten. Weitere Informationen zu den **SqlTriggerContext** Objekt, finden Sie unter [SqlTriggerContext-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: Die **IsAvailable** -Eigenschaft wird verwendet, um die Verfügbarkeit des Kontexts zu ermitteln.  
  
-   **WindowsIdentity**: Die **WindowsIdentity** -Eigenschaft wird verwendet, um die Windows-Identität des aufrufenden Programms abzurufen.  
  
## <a name="determining-context-availability"></a>Bestimmen der Kontextverfügbarkeit  
 Fragen Sie die **SqlContext** -Klasse ab, um zu ermitteln, ob der gerade ausgeführte Code prozessintern ausgeführt wird. Überprüfen Sie dazu die **IsAvailable** -Eigenschaft des **SqlContext** -Objekts. Die **IsAvailable** Eigenschaft ist schreibgeschützt und gibt **"true"** , wenn der aufrufende Code, in ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und auf andere **SqlContext** Member zugegriffen werden kann. Wenn die **IsAvailable** -Eigenschaft **False**zurückgibt, lösen alle anderen **SqlContext** -Elemente eine **InvalidOperationException**-Ausnahme aus, falls sie verwendet werden. Wenn **IsAvailable** **False**zurückgibt, schlagen alle Versuche, ein Verbindungsobjekt zu öffnen, bei denen "context connection=true" festgelegt ist, fehl.  
  
## <a name="retrieving-windows-identity"></a>Abrufen der Windows-Identität  
 CLR-codeausführung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird immer im Kontext des Prozesskontos aufgerufen. Wenn der Code bestimmte Aktionen mit der Identität des aufrufenden Benutzers anstelle von ausführen, sollten die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Identitätstoken abgerufen werden sollen, über-Prozessidentität der **WindowsIdentity** Eigenschaft von der  **SqlContext** Objekt. Die **WindowsIdentity** -Eigenschaft gibt eine **WindowsIdentity** Instanz darstellt. die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Identität des Aufrufers oder Null, wenn der Client authentifiziert wurde mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. Nur mit der **EXTERNAL_ACCESS** -Berechtigung oder **UNSAFE** -Berechtigung markierte Assemblys können auf diese Eigenschaft zugreifen.  
  
 Nach dem Erhalt des **WindowsIdentity** -Objekts können aufrufende Benutzer einen Identitätswechsel für das Clientkonto durchführen und Aktionen mit der neuen Identität ausführen.  
  
 Die Identität des aufrufenden Benutzers ist nur über **SqlContext.WindowsIdentity** verfügbar, wenn der Client, der die Ausführung der gespeicherten Prozedur oder der Funktion initiiert hat, mithilfe der Windows-Authentifizierung eine Verbindung mit dem Server hergestellt hat. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung stattdessen verwendet wurde, diese Eigenschaft ist null, und der Code des Aufrufers annehmen kann.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Abrufen der Windows-Identität des aufrufenden Clients und der Identitätswechsel des Clients veranschaulicht.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SqlPipe-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR-Trigger](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Von SQL Server verwendete prozessinterne spezifische Erweiterungen für ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
