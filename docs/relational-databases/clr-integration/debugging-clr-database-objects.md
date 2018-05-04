---
title: Debuggen von CLR-Datenbankobjekten | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
caps.latest.revision: 46
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8bf6b05d891d18fec8cfc063321f294c914cfa13
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="debugging-clr-database-objects"></a>Debuggen von CLR-Datenbankobjekten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Debuggen von [!INCLUDE[tsql](../../includes/tsql-md.md)] und CLR (Common Language Runtime)-Objekten in der Datenbank. Die Hauptaspekte des Debuggens in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind die leichte Einrichtung und Handhabung und die Integration des SQL Server-Debuggers in den Microsoft Visual Studio-Debugger. Darüber hinaus ist das Debuggen sprachübergreifend. Benutzer können Einzelschritte in CLR-Objekte aus [!INCLUDE[tsql](../../includes/tsql-md.md)] und umgekehrt ausführen. Der Transact-SQL-Debugger in SQL Server Management Studio kann nicht verwendet werden, um Datenbankobjekte zu debuggen, aber Sie können die Objekte debuggen, indem Sie die Debugger in Visual Studio verwenden. Das Debuggen verwalteter Datenbankobjekte in Visual Studio unterstützt alle gängigen Debugfunktionen, wie z. B. „Einzelschritt“- und „Prozedurschritt“-Anweisungen innerhalb von Routinen, die auf dem Server ausgeführt werden. Debugger können während des Debuggens Breakpoints festlegen, Aufruflisten prüfen, Variablen prüfen und Variablenwerte ändern. Beachten Sie, dass Visual Studio .NET 2003 nicht für CLR-Integrationsprogrammierung oder das Debuggen verwendet werden kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beinhaltet ein vorinstalliertes .NET Framework, und Visual Studio .NET 2003 kann nicht die .NET Framework 2.0-Assemblys verwenden.  
  
 Weitere Informationen zum Debuggen von verwalteten Codes mithilfe von Visual Studio finden Sie unter der "[Debuggen von verwaltetem Code](http://go.microsoft.com/fwlink/?LinkId=120377)" Thema in der Visual Studio-Dokumentation.  
  
## <a name="debugging-permissions-and-restrictions"></a>Debuggen von Berechtigungen und Einschränkungen  
 Debuggen ist ein Vorgang mit hohen Berechtigungen, und daher nur von Mitgliedern der der **Sysadmin** festen Serverrolle dürfen daher dazu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Während des Debuggens gelten die folgenden Einschränkungen:  
  
-   Das Debuggen von CLR-Routinen kann nur von einer Debugger-Instanz gleichzeitig vorgenommen werden. Diese Einschränkung ist vorhanden, da jegliche CLR-Codeausführung eingefroren wird, wenn der Breakpoint erreicht wird, und die Ausführung wird erst fortgesetzt, wenn sich der Debugger vom Breakpoint fortbewegt. Allerdings können Sie das Debuggen von [!INCLUDE[tsql](../../includes/tsql-md.md)] auf anderen Verbindungen fortführen. Obwohl das [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debuggen keine anderen Ausführungen auf dem Server einfriert, könnte es dazu führen, dass durch Aufrechterhaltung einer Sperre andere Verbindungen warten.  
  
-   Für vorhandene Verbindungen kann kein Debuggen vorgenommen werden. Nur neue Verbindungen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], erfordern Informationen über die Client- und Debugger-Umgebung, bevor die Verbindung hergestellt werden kann.  
  
 Aufgrund der oben genannten Einschränkungen empfehlen wir, dass [!INCLUDE[tsql](../../includes/tsql-md.md)]- und CLR-Code auf einem Testserver und nicht auf einem Produktionsserver gedebuggt werden.  
  
## <a name="overview-of-debugging-managed-database-objects"></a>Übersicht über das Debuggen von verwalteten Datenbankobjekten  
 Das Debuggen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfolgt nach einem Pro-Verbindungsmodell. Ein Debugger kann nur Aktivitäten zu einer Clientverbindung erkennen und debuggen, mit der er verknüpft ist. Da die Funktionalität eines Debuggers nicht durch den Verbindungstyp eingeschränkt wird, können sowohl TDS- (Tabular Data Stream) als auch HTTP-Verbindungen gedebuggt werden. Allerdings ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht das Debuggen vorhandener Verbindungen. Das Debuggen unterstützt alle üblichen Debugfunktionen innerhalb von Routinen, die auf dem Server ausgeführt werden. Die Interaktion zwischen einem Debugger und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geschieht durch DCOM (Distributed Component Object Model).  
  
 Weitere Informationen und Szenarien über das Debuggen verwalteter, gespeicherter Prozeduren, Funktionen, Trigger, benutzerdefinierte Typen und Aggregate finden Sie in der "[SQL CLR-Integration Datenbank das Serverdebuggen](http://go.microsoft.com/fwlink/?LinkId=120378)" Thema in der Visual Studio (Dokumentation).  
  
 Das TCP/IP-Netzwerkprotokoll muss in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiviert werden, damit Visual Studio von einem Remotecomputer aus zum Entwickeln, Debuggen und Bereitstellen verwendet werden kann. Weitere Informationen zum Aktivieren des TCP/IP-Protokolls auf dem Server finden Sie unter [Konfigurieren von Clientprotokollen](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-debug-a-managed-database-object"></a>So debuggen Sie ein verwaltetes Datenbankobjekt  
  
1.  Öffnen Sie Microsoft Visual Studio, und erstellen Sie ein neues [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Projekt. Stellen Sie eine Verbindung zu einer Datenbank auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her.  
  
2.  Erstellen Sie einen neuen Typ. In **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, wählen Sie **hinzufügen** und **neues Element...** Aus der **neues Element hinzufügen** wählen **Stored Procedure**, **eine benutzerdefinierte Funktion**, **User-Defined Type**,  **Trigger**, **aggregieren**, oder **Klasse**. Geben Sie einen Namen für die Quelldatei des neuen Typs aus, und klicken Sie auf **hinzufügen**.  
  
3.  Fügen Sie Code für den neuen Typ zum Texteditor hinzu. Beispielcode für eine gespeicherte Prozedur finden Sie in einem späteren Abschnitt in diesem Thema.  
  
4.  Fügen Sie ein Skript hinzu, das den Typ testet. In **Projektmappen-Explorer**, erweitern Sie die **TestScripts** Directory doppelklicken **Test.sql** um die standardmäßige Standardtestskript-Quelldatei zu öffnen. Fügen Sie das Testskript, das den Code dazu aufruft, zu debuggen, zum Texteditor hinzu. Ein Beispielskript sehen Sie unten.  
  
5.  Platzieren Sie einen oder mehrere Breakpoints im Quellcode. Mit der rechten Maustaste auf eine Codezeile im Texteditor – innerhalb der Funktion oder eine Routine, die Sie debuggen möchten, und wählen Sie **Haltepunkt** und **Haltepunkt einfügen**. Der Breakpoint wird hinzugefügt und hebt die Codezeile in Rot hervor.  
  
6.  In der **Debuggen** klicken Sie im Menü **Debuggen** zum Kompilieren, bereitstellen und Testen Sie das Projekt. Das Testskript in Test.sql wird ausgeführt, und das verwaltete Datenbankobjekt wird aufgerufen.  
  
7.  Wenn der gelbe Pfeil, der den Anweisungszeiger kennzeichnet, am Breakpoint angezeigt wird, pausiert die Codeausführung, und Sie können mit dem Debuggen Ihres verwalteten Datenbankobjekts beginnen. Sie können **Prozedurschritt** aus der **Debuggen** -Menü, um den Anweisungszeiger zur nächsten Zeile des Codes zu gelangen. Die **"lokal"** Fenster wird verwendet, um den Status der Objekte, die aktuell vom Anweisungszeiger hervorgehoben beobachten. Variablen können hinzugefügt werden, um die **Überwachen** Fenster. Der Zustand der überwachten Variablen kann während der gesamten Debuggingsitzung beobachtet werden und nicht nur, wenn die Variable sich in der Codezeile befindet, die aktuell vom Anweisungszeiger hervorgehoben wird. Wählen Sie im Menü Debuggen Weiter aus, um mit dem Anweisungszeiger zum nächsten Breakpoint zu springen oder um die Ausführung der Routine abzuschließen, wenn keine weiteren Breakpoints vorhanden sein sollten.  
  
### <a name="example"></a>Beispiel  
 Das folgende Beispiel gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version an den Aufrufer zurück.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 Im Folgenden handelt es sich um ein Testskript, das die oben definierte gespeicherte Prozedur GetVersion aufruft.  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierkonzepte für die Integration der Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
