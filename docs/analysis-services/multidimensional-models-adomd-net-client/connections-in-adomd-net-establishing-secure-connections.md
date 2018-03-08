---
title: Aufbauen von sicheren Verbindungen in ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6916e57fc0135fc5688c6569eaeb8341caa23b82
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="connections-in-adomdnet---establishing-secure-connections"></a>Verbindungen in ADOMD.NET - aufbauen von sicheren Verbindungen
  Wenn Sie eine Verbindung in ADOMD.NET verwenden, hängt die Sicherheitsmethode aus, die für die Verbindung verwendet wird der Wert des der **ProtectionLevel** Eigenschaft der Verbindungszeichenfolge verwendet wird, beim Aufrufen der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> Methode von der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 Die **ProtectionLevel** Eigenschaft bietet vier Sicherheitsebenen: nicht authentifiziert, authentifiziert, signiert und verschlüsselt. In der folgenden Tabelle werden diese verschiedenen Sicherheitsstufen beschrieben.  
  
> [!NOTE]  
>  Wenn Sie Datenbankverbindungspooling verwenden, ist die Datenbank nicht in der Lage, Sicherheit zu verwalten. Das liegt daran, dass für Datenbankverbindungspooling Verbindungszeichenfolgen identisch sein müssen, um Verbindungen zu einem Pool zusammenzufassen. Deshalb müssen Sie Sicherheit an anderer Stelle verwalten.  
  
|Sicherheitsebene|ProtectionLevel-Wert|  
|--------------------|---------------------------|  
|*nicht authentifizierte Verbindung*<br /> Eine nicht authentifizierte Verbindung nimmt keine Form der Authentifizierung vor. Diese Art der Verbindung stellt die am häufigsten unterstützte, aber am wenigsten sichere Verbindungsart, dar.|**InclusionThresholdSetting**|  
|*authentifizierte Verbindung*<br /> Eine authentifizierte Verbindung authentifiziert den Benutzer, der die Verbindung herstellt, sichert jedoch keine weitere Kommunikation. Diese Art der Verbindung ist sinnvoll, da Sie die Identität des Benutzers oder der Anwendung feststellen können, der oder die eine Verbindung mit der analytischen Datenquelle herstellt.|**Verbinden**|  
|*signierte Verbindung*<br /> Eine signierte Verbindung authentifiziert den Benutzer, der die Verbindung anfordert, und stellt anschließend sicher, dass die Übertragungen nicht verändert werden. Diese Art von Verbindung ist nützlich, wenn die Echtheit der übertragenen Daten überprüft werden muss. Eine signierte Verbindung verhindert jedoch nur, dass der Inhalt des Datenpakets geändert wird. Der Inhalt kann unterwegs noch immer angezeigt werden.<br /><br /><br /><br /> Beachten Sie, dass eine signierte Verbindung nur von der XML for Analysis-Anbieter von bereitgestellten unterstützt wird [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|**Pkt Integrität** oder **PktIntegrity**|  
|*verschlüsselte Verbindung*<br /> Eine verschlüsselte Verbindung ist der von ADOMD.NET verwendete Standardverbindungstyp. Diese Verbindungsart authentifiziert den Benutzer, der die Verbindung anfordert, und verschlüsselt außerdem die übertragenen Daten. Eine verschlüsselte Verbindung ist die sicherste Verbindungsart, die von ADOMD.NET erstellt werden kann. Der Inhalt des Datenpakets kann nicht angezeigt oder geändert werden, sodass die Daten während der Übertragung geschützt sind.<br /><br /><br /><br /> Eine verschlüsselte Verbindung wird nur unterstützt, von der XML for Analysis-Anbieter von bereitgestellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|**Pkt Datenschutz** oder **PktPrivacy**|  
  
 Es sind jedoch nicht alle Sicherheitsebenen für alle Arten von Verbindungen verfügbar:  
  
-   Eine TCP-Verbindung kann alle der vier Sicherheitsebenen verwenden. Tatsächlich stellt eine zusammen mit der integrierten Sicherheit von Windows verwendete TCP-Verbindung die sicherste Methode der Verbindung mit einer analytischen Datenquelle dar.  
  
-   Eine HTTP-Verbindung kann nur eine authentifizierte Verbindung sein. Aus diesem Grund die **ProtectionLevel** Eigenschaft muss festgelegt werden, um **verbinden**.  
  
-   Eine HTTPS-Verbindung kann nur eine verschlüsselte Verbindung sein. Aus diesem Grund die **ProtectionLevel** Eigenschaft muss festgelegt werden, um **Pkt Datenschutz** oder **PktPrivacy**.  
  
## <a name="securing-tcp-connections"></a>Sichern von TCP-Verbindungen  
 Für eine TCP-Verbindung die **ProtectionLevel** Eigenschaft unterstützt alle vier Sicherheitsebenen, wie in der folgenden Tabelle gezeigt.  
  
|ProtectionLevel-Wert|Verwendung mit TCP-Verbindung?|Ergebnisse|  
|---------------------------|------------------------------|-------------|  
|**InclusionThresholdSetting**|ja|Gibt eine nicht authentifizierte Verbindung an.<br /><br /> Vom Anbieter wird ein TCP-Datenstrom angefordert, es wird jedoch für den Benutzer, der den Datenstrom anfordert, keinerlei Authentifizierung ausgeführt.|  
|**Verbinden**|ja|Gibt eine authentifizierte Verbindung an.<br /><br /> Vom Anbieter wird ein TCP-Datenstrom angefordert, und klicken Sie dann den Sicherheitskontext des Benutzers, der den Datenstrom anfordert, wird anhand des Servers authentifiziert wird: Wenn die Authentifizierung erfolgreich ist, wird keine andere Aktion ausgeführt. Wenn die Authentifizierung fehlschlägt, trennt das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt die Verbindung zur mehrdimensionalen Datenquelle, und eine Ausnahme wird ausgelöst.<br /><br /> Nachdem die Authentifizierung erfolgreich gewesen ist oder fehlschlägt, wird der Sicherheitskontext, der verwendet wird, um die Verbindung zu authentifizieren, freigegeben.|  
|**Pkt Integrität** oder **PktIntegrity**|ja|Gibt eine signierte Verbindung an.<br /><br /> Vom Anbieter wird ein TCP-Datenstrom angefordert, und klicken Sie dann den Sicherheitskontext des Benutzers, der den Datenstrom anfordert, wird anhand des Servers authentifiziert wird:<br /><br /> <br /><br /> Wenn die Authentifizierung erfolgreich ist, schließt das  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt den bestehenden TCP-Datenstrom und öffnet einen signierten TCP-Datenstrom, der alle Anforderungen verarbeitet. Alle Anforderungen von Daten und Metadaten werden mithilfe des Sicherheitskontexts authentifiziert, der zum Öffnen der Verbindung verwendet wurde. Zudem wird jedes Paket digital signiert, um sicherzustellen, dass die Nutzlast des TCP-Pakets nicht auf irgendeine Weise geändert wurde.<br /><br /> <br /><br /> Wenn die Authentifizierung fehlschlägt, trennt das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt die Verbindung zur mehrdimensionalen Datenquelle, und eine Ausnahme wird ausgelöst.|  
|**Pkt Datenschutz** oder **PktPrivacy**|ja|Gibt eine verschlüsselte Verbindung an.<br /><br /> <br /><br /> Beachten Sie, dass Sie auch eine verschlüsselte Verbindung angeben können, indem Sie nicht Festlegen der **ProtectionLevel** Eigenschaft in der Verbindungszeichenfolge angegeben.<br /><br /> <br /><br /> Vom Anbieter wird ein TCP-Datenstrom angefordert, und der Sicherheitskontext des Benutzers, der den Datenstrom anfordert, wird bei dem Server authentifiziert.<br /><br /> <br /><br /> Wenn die Authentifizierung erfolgreich ist, schließt das  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt den bestehenden TCP-Datenstrom und öffnet einen verschlüsselten TCP-Datenstrom, der alle Anforderungen verarbeitet. Alle Anforderungen von Daten und Metadaten werden mithilfe des Sicherheitskontexts authentifiziert, der zum Öffnen der Verbindung verwendet wurde. Außerdem wird die Nutzlast eines jeden TCP-Pakets mit der höchsten Verschlüsselungsmethode verschlüsselt, die sowohl von dem Anbieter als auch von der multidimensionalen Datenquelle unterstützt wird.<br /><br /> <br /><br /> Wenn die Authentifizierung fehlschlägt, trennt das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt die Verbindung zur mehrdimensionalen Datenquelle, und eine Ausnahme wird ausgelöst.|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>Verwenden der integrierten Sicherheit von Windows für die Verbindung  
 Die integrierte Sicherheit von Windows ist die sicherste Möglichkeit, eine Verbindung zu einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] herzustellen und zu sichern. Die integrierte Sicherheit von Windows zeigt während des Authentifizierungsprozesses keine Sicherheitsanmeldeinformationen wie Benutzername oder Kennwort an, stattdessen wird die Sicherheits-ID des zurzeit ausgeführten Prozesses verwendet, um die Identität zu ermitteln. Für die meisten Clientanwendungen stellt diese Sicherheits-ID die Identität des gerade angemeldeten Benutzers dar.  
  
 Um die integrierte Sicherheit von Windows zu verwenden, sind für die Verbindungszeichenfolge die folgenden Einstellungen erforderlich:  
  
-   Für die **integrierte Sicherheit von** -Eigenschaft nicht legen Sie diese Eigenschaft, oder legen Sie diese Eigenschaft auf **SSPI**.  
  
    > [!NOTE]  
    >  Integrierte Sicherheit von Windows ist nur für TCP-Verbindungen verfügbar, da der HTTP-Verbindungen verwenden, müssen die **grundlegende** Einstellung für die **integrierte Sicherheit von** Eigenschaft.  
  
-   Für die **ProtectionLevel** -Eigenschaft, legen Sie diese Eigenschaft auf **verbinden**, **Pkt Integrität**, oder **Pkt Datenschutz**.  
  
## <a name="securing-http-connections"></a>Sichern von HTTP-Verbindungen  
 HTTPS und Secure Sockets Layer (SSL) kann verwendet werden, um die HTTP-Kommunikation mit einer analytischen Datenquelle extern zu sichern.  
  
 Da ein XMLA-Anbieter nur sicheres HTTP verwendet, muss eine HTTP-Verbindung in ADOMD.NET eine signierte Verbindung sein, wie in der folgenden Tabelle dargestellt.  
  
|ProtectionLevel-Wert|Verwendung mit HTTP oder HTTPS|  
|---------------------------|----------------------------|  
|**InclusionThresholdSetting**|nein|  
|**Verbinden**|HTTP|  
|**Pkt Integrität** oder **PktIntegrity**|nein|  
|**Pkt Datenschutz** oder **PktPrivacy**|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>Öffnen einer sicheren HTTP-Verbindung  
 Im folgenden Beispiel wird veranschaulicht, wie ADOMD.NET verwendet wird, öffnen Sie eine HTTP-Verbindung für die **AdventureWorksAS** Beispiel [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank:  
  
```vb  
Public Function GetAWEncryptedConnection( _  
    Optional ByVal serverName As String = "https:\\localhost\isapy\msmdpump.dll") _  
    As AdomdConnection  
  
    Dim strConnectionString As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' To establish an encrypted connection, set the   
        ' ProtectionLevel setting to PktPrivacy.  
        strConnectionString = "DataSource=" & serverName & ";" & _  
            "Catalog=AdventureWorksAS;" & _  
            "ProtectionLevel=PktPrivacy;"  
  
        ' Note that username and password are not supplied here.  
        ' The current security context is used for authentication  
        ' purposes.  
  
        objConnection.ConnectionString = strConnectionString  
        objConnection.Open()  
    Catch ex As Exception  
        objConnection = Nothing  
        Throw ex  
    Finally  
        ' Return the encrypted connection.  
        GetAWEncryptedConnection = objConnection  
    End Try  
End Function  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Aufbauen von Verbindungen in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
  
