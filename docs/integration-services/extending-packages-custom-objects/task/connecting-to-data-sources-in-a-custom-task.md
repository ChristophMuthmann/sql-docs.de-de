---
title: Herstellen einer Verbindung mit Datenquellen in einem benutzerdefinierten Task | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ConnectionManager objects
- connection managers [Integration Services], external data sources
- data sources [Integration Services], external
- custom tasks [Integration Services], external data sources
- external data sources [Integration Services]
- connections [Integration Services], external data sources
- SSIS custom tasks, external data sources
ms.assetid: 9f0b3a43-3eaa-4b3c-bb08-29b630c11306
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5b9446be2b632e6df78fbc1f66762de02d4644f5
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-a-custom-task"></a>Herstellen einer Verbindung mit Datenquellen in einem benutzerdefinierten Task
  Tasks stellen eine Verbindung mit externen Datenquellen her, um Daten mit einem Verbindungs-Manager abzurufen oder zu speichern. Zur Entwurfszeit stellt ein Verbindungs-Manager eine logische Verbindung dar und beschreibt Schlüsselinformationen wie den Servernamen und Authentifizierungseigenschaften. Zur Laufzeit rufen Tasks die <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A>-Methode des Verbindung-Managers auf, um die physische Verbindung mit der Datenquelle herzustellen.  
  
 Da ein Paket zahlreiche Tasks enthalten kann, von denen möglicherweise jede eine Verbindung mit einer anderen Datenquelle herstellt, verfolgt das Paket alle Verbindungs-Manager in einer Auflistung, nämlich in der <xref:Microsoft.SqlServer.Dts.Runtime.Connections>-Auflistung. Tasks suchen mithilfe der Auflistung in ihrem Paket nach dem Verbindungs-Manager, den sie bei der Überprüfung und Ausführung verwenden. Die <xref:Microsoft.SqlServer.Dts.Runtime.Connections>-Auflistung ist der erste Parameter der Methoden <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> und <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
 Sie können verhindern, dass der Task den falschen Verbindungs-Manager verwendet, indem Sie dem Benutzer die <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>-Objekte aus der Auflistung mithilfe eines Dialogfelds oder einer Dropdownliste auf der grafischen Benutzeroberfläche anzeigen. So hat der Benutzer nur die Auswahl zwischen den im Paket enthaltenen <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>-Objekten des geeigneten Typs.  
  
 Tasks rufen die <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A>-Methode auf, um die physische Verbindung mit der Datenquelle herzustellen. Die Methode gibt das zugrunde liegende Verbindungsobjekt zurück, das dann vom Task verwendet werden kann. Da der Verbindungs-Manager die Implementierungsdetails des zugrunde liegenden Verbindungsobjekts vom Task isoliert, muss der Task nur die <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A>-Methode aufrufen, um die Verbindung herzustellen, und muss sich um keine anderen Aspekte der Verbindung kümmern.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird die Überprüfung des <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>-Namens in den Methoden Validate und Execute dargestellt und gezeigt, wie mithilfe der <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A>-Methode eine physische Verbindung in der Execute-Methode hergestellt wird.  
  
```csharp  
private string connectionManagerName = "";  
  
public string ConnectionManagerName  
{  
  get { return this.connectionManagerName; }  
  set { this.connectionManagerName = value; }  
}  
  
public override DTSExecResult Validate(  
  Connections connections, VariableDispenser variableDispenser,  
  IDTSComponentEvents componentEvents, IDTSLogging log)  
{  
  // If the connection manager exists, validation is successful;  
  // otherwise, fail validation.  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception e)  
  {  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
  
public override DTSExecResult Execute(Connections connections,   
  VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,   
  IDTSLogging log, object transaction)  
{  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    object connection = cm.AcquireConnection(transaction);  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception exception)  
  {  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
```  
  
```vb  
Private _connectionManagerName As String = ""  
  
Public Property ConnectionManagerName() As String  
  Get  
    Return Me._connectionManagerName  
  End Get  
  Set(ByVal Value As String)  
    Me._connectionManagerName = value  
  End Set  
End Property  
  
Public Overrides Function Validate( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  ' If the connection manager exists, validation is successful;  
  ' otherwise fail validation.  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Return DTSExecResult.Success  
  Catch e As System.Exception  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
  
Public Overrides Function Execute( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging, ByVal transaction As Object) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Dim connection As Object = cm.AcquireConnection(transaction)  
    Return DTSExecResult.Success  
  Catch exception As System.Exception  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Erstellen von Verbindungs-Manager](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

