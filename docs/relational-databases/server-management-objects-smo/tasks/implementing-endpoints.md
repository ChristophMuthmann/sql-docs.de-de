---
title: Implementieren von Endpunkten | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: endpoints [SMO]
ms.assetid: f8674dbb-9bc0-488f-9def-e9e0ce1ddf86
caps.latest.revision: "45"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a1d8ce479654f80d54c1a5aef6fb63138e13dbc6
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="implementing-endpoints"></a>Implementieren von Endpunkten
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Ein Endpunkt ist ein Dienst, der Anforderungen systemeigen überwachen kann. SMO unterstützt verschiedene Typen von Endpunkten mit dem <xref:Microsoft.SqlServer.Management.Smo.Endpoint> Objekt. Sie können einen Endpunkt erstellen, der einen bestimmten Typ von Nutzlast handhabt, der ein bestimmtes Protokoll nutzt, indem Sie eine Instanz eines <xref:Microsoft.SqlServer.Management.Smo.Endpoint>-Objekts erstellen und dessen Eigenschaften einrichten.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.Endpoint.EndpointType%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Management.Smo.Endpoint> Objekt kann verwendet werden, um die folgenden Nutzlasttypen festzulegen:  
  
-   Datenbankspiegelung  
  
-   SOAP (SOAP-Endpunkte werden in [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] und früheren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Versionen unterstützt)  
  
-   Service Broker  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
  
 Darüber hinaus kann die <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A>-Eigenschaft verwendet werden, um die beiden folgenden unterstützten Protokolle anzugeben:  
  
-   HTTP-Protokoll  
  
-   TCP-Protokoll  
  
 Nachdem Sie den Typ der Nutzlast angegeben, die tatsächliche Nutzlast kann festgelegt werden mithilfe der <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Payload%2A> -Objekteigenschaft. Die <xref:Microsoft.SqlServer.Management.Smo.Payload>-Objekteigenschaft stellt einen Verweis auf ein Nutzlastobjekt eines bestimmten Typs bereit, dessen Eigenschaften geändert werden können.  
  
 Für das <xref:Microsoft.SqlServer.Management.Smo.DatabaseMirroringPayload>-Objekt müssen Sie die Spiegelungsrolle angeben und ob Verschlüsselung aktiviert wird. Die <xref:Microsoft.SqlServer.Management.Smo.ServiceBrokerPayload> -Objekt erfordert Informationen über die nachrichtenweiterleitung, die maximale Anzahl zulässiger Verbindungen und den Authentifizierungsmodus. Das <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethod.%23ctor%2A>-Objekt erfordert, dass diverse Eigenschaften eingerichtet werden müssen; hierunter auch die <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethodCollection.Add%2A>-Objekteigenschaft, die die SOAP-Nutzlastmethoden angibt, die Clients zur Verfügung stehen (gespeicherte Prozeduren und benutzerdefinierte Funktionen).  
  
 Ähnlich kann das tatsächliche Protokoll über die <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Protocol%2A>-Objekteigenschaft eingerichtet werden, die auf ein Protokollobjekt verweist, das den von der <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A>-Eigenschaft festgelegten Typ besitzt. Das <xref:Microsoft.SqlServer.Management.Smo.HttpProtocol>-Objekt erfordert eine Liste der eingeschränkten IP-Adressen und Informationen über Port, Website und Authentifizierung. Die <xref:Microsoft.SqlServer.Management.Smo.TcpProtocol> -Objekt erfordert ebenfalls eine Liste der eingeschränkten IP-Adressen und Portinformationen.  
  
 Wenn der Endpunkt erstellt wurde und vollständig definiert ist, kann Datenbankbenutzern, Gruppen, Rollen und Anmeldungen der Zugriff gewährt, aufgehoben oder verweigert werden.  
  
## <a name="example"></a>Beispiel  
 Für das folgende Codebeispiel müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-basic"></a>Erstellen eines Datenbankspiegelungs-Endpunkt-Diensts in Visual Basic  
 Im Codebeispiel wird veranschaulicht, wie ein Datenbankspiegelungs-Endpunkt in SMO erstellt wird. Dies ist notwendig, bevor Sie einen Datenbankspiegel erstellen. Verwenden Sie <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> und andere Eigenschaften auf dem <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt, um einen Datenbankspiegel zu erstellen.  
  
```VBNET
'Set up a database mirroring endpoint on the server before setting up a database mirror.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Endpoint object variable for database mirroring.
Dim ep As Endpoint
ep = New Endpoint(srv, "Mirroring_Endpoint")
ep.ProtocolType = ProtocolType.Tcp
ep.EndpointType = EndpointType.DatabaseMirroring
'Specify the protocol ports.
ep.Protocol.Http.SslPort = 5024
ep.Protocol.Tcp.ListenerPort = 6666
'Specify the role of the payload.
ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All
'Create the endpoint on the instance of SQL Server.
ep.Create()
'Start the endpoint.
ep.Start()
Console.WriteLine(ep.EndpointState)
``` 
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-c"></a>Erstellen eines Datenbankspiegelungs-Endpunkt-Diensts in Visual C#  
 Im Codebeispiel wird veranschaulicht, wie ein Datenbankspiegelungs-Endpunkt in SMO erstellt wird. Dies ist notwendig, bevor Sie einen Datenbankspiegel erstellen. Verwenden Sie <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> und andere Eigenschaften auf dem <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt, um einen Datenbankspiegel zu erstellen.  
  
```csharp  
{  
            //Set up a database mirroring endpoint on the server before   
        //setting up a database mirror.   
        //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Define an Endpoint object variable for database mirroring.   
            Endpoint ep = default(Endpoint);  
            ep = new Endpoint(srv, "Mirroring_Endpoint");  
            ep.ProtocolType = ProtocolType.Tcp;  
            ep.EndpointType = EndpointType.DatabaseMirroring;  
            //Specify the protocol ports.   
            ep.Protocol.Http.SslPort = 5024;  
            ep.Protocol.Tcp.ListenerPort = 6666;  
            //Specify the role of the payload.   
            ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All;  
            //Create the endpoint on the instance of SQL Server.   
            ep.Create();  
            //Start the endpoint.   
            ep.Start();  
            Console.WriteLine(ep.EndpointState);  
        }  
```  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-powershell"></a>+Erstellen eines Datenbankspiegelungs-Endpunkt-Diensts in PowerShell  
 Im Codebeispiel wird veranschaulicht, wie ein Datenbankspiegelungs-Endpunkt in SMO erstellt wird. Dies ist notwendig, bevor Sie einen Datenbankspiegel erstellen. Verwenden Sie <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> und andere Eigenschaften auf dem <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt, um einen Datenbankspiegel zu erstellen.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get a new endpoint to congure and add  
$ep = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Endpoint -argumentlist $srv,"Mirroring_Endpoint"  
  
#Set some properties  
$ep.ProtocolType = [Microsoft.SqlServer.Management.SMO.ProtocolType]::Tcp  
$ep.EndpointType = [Microsoft.SqlServer.Management.SMO.EndpointType]::DatabaseMirroring  
$ep.Protocol.Http.SslPort = 5024  
$ep.Protocol.Tcp.ListenerPort = 6666 #inline comment  
$ep.Payload.DatabaseMirroring.ServerMirroringRole = [Microsoft.SqlServer.Management.SMO.ServerMirroringRole]::All  
  
# Create the endpoint on the instance  
$ep.Create()  
  
# Start the endpoint  
$ep.Start()  
  
# Report its state  
$ep.EndpointState;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
