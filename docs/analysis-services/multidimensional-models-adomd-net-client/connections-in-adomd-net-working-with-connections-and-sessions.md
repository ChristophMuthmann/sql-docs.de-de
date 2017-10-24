---
title: Arbeiten mit Verbindungen und Sitzungen in ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6926a8cd71983a98d68f59e0dbe30a1b0e78ece8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="connections-in-adomdnet---working-with-connections-and-sessions"></a>Verbindungen in ADOMD.NET - arbeiten mit Verbindungen und Sitzungen
  In XML for Analysis (XMLA) unterstützen Sitzungen zustandsbehaftete Vorgänge während des Zugriffs auf analytische Daten. Sitzungen sind der Rahmen für den Bereich und den Kontext von Befehlen und Transaktionen für eine analytische Datenquelle. Die XMLA-Elemente verwendet, um Sitzungen zu verwalten sind [BeginSession](../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md), [Sitzung](../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md), und [EndSession](../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md).  
  
 ADOMD.NET verwendet diese drei XMLA-Sitzungselemente beim Start einer Sitzung, beim Durchführen einer Abfrage oder Abfragen von Daten während einer Sitzung und beim Beenden einer Sitzung.  
  
## <a name="starting-a-session"></a>Starten einer Sitzung  
 Die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>-Eigenschaft des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekts enthält den Bezeichner der aktiven Sitzung, die dem <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt zugeordnet ist. Durch die ordnungsgemäße Verwendung dieser Eigenschaft können Sie sowohl die Client- als auch die Server-Statusbehaftung in Ihrer Anwendung kontrollieren:  
  
-   Wenn die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> Eigenschaftensatz ist nicht mit einer gültigen Sitzung-ID, wenn die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> -Methode aufgerufen wird, die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> Objekts fordert eine neue Sitzungs-ID des Anbieters. ADOMD.NET initiiert eine Sitzung, indem es einen XMLA- **BeginSession** -Header an den Anbieter sendet. Ist ADOMD.NET beim Start einer Sitzung erfolgreich, setzt ADOMD.NET den Wert der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>-Eigenschaft auf den Sitzungs-ID der neu generierten Sitzung.  
  
-   Ist die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> bei Aufruf der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A>-Methode auf eine gültige Sitzungs-ID gesetzt, versucht das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt, eine Verbindung zur angegebenen Sitzung aufzubauen.  
  
 Wenn das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt keine Verbindung zur angegebenen Sitzung aufbauen kann oder der Anbieter keine Sitzungen unterstützt, wird eine Ausnahme ausgelöst.  
  
> [!NOTE]  
>  Nachdem ADOMD.NET eine Sitzung generiert hat, können Sie mehrere <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekte mit einer einzelnen aktiven Sitzung verbinden oder die Verbindung eines einzelnen <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekts mit dieser Sitzung trennen und das Objekt mit einer anderen Sitzung verbinden.  
  
## <a name="working-in-a-session"></a>Arbeiten in einer Sitzung  
 Nachdem ADOMD.NET das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> -Objekt mit einer gültigen Sitzung sendet ADOMD.NET einen XMLA **Sitzung** -Header an den Anbieter mit jeder Anforderung von Daten oder Metadaten, die von einer Anwendung vorgenommen werden. Bei jeder Anforderung wird die Sitzungs-ID auf den Wert der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>-Eigenschaft gesetzt.  
  
 Eine Sitzungs-ID garantiert nicht, dass eine Sitzung gültig bleibt. Wenn eine Sitzung abläuft (beispielsweise bei einem Timeout der Sitzung oder wenn die Verbindung unterbrochen wird), kann der Anbieter die Aktionen der Sitzung beenden und rückgängig machen. In diesem Fall alle nachfolgenden Methodenaufrufe vom der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> Objekt wird eine Ausnahme ausgelöst. Da Ausnahmen nur ausgelöst werden, wenn die nächste Anforderung zum Anbieter gesendet wird, und nicht, wenn die Sitzung abläuft, muss Ihre Anwendung in der Lage sein, diese Ausnahmen immer dann behandeln zu können, wenn Ihre Anwendung Daten oder Metadaten vom Anbieter empfängt.  
  
## <a name="closing-a-session"></a>Beenden einer Sitzung  
 Wenn die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> Methode wird aufgerufen, ohne Angabe des Werts der *EndSession* Parameter, oder wenn die *EndSession* Parameter auf "true", sowohl die Verbindung mit der Sitzung und die Sitzung festgelegt ist zugeordnete der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> -Objekt geschlossen werden. Um eine Sitzung zu beenden, sendet ADOMD.NET einen XMLA- **EndSession** -Header an den Anbieter, mit der Sitzungs-ID festgelegt werden, auf den Wert, der die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> Eigenschaft.  
  
 Wenn die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> -Methode aufgerufen wird und die *EndSession* Parametersatz auf "false", die diesem zugeordnete Sitzung die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> Objekt bleibt aktiv, aber die Verbindung mit der Sitzung wird beendet.  
  
## <a name="example-of-managing-a-session"></a>Beispiel für die Verwaltung einer Sitzung  
 Das folgende Beispiel veranschaulicht, wie eine Verbindung geöffnet, eine Sitzung generiert und eine Verbindung beendet wird, während in ADOMD.NET die Sitzung geöffnet bleibt:  
  
```vb  
Public Function CreateSession(ByVal connectionString As String) As String  
    Dim strSessionID As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' First, try to connect to the specified data source.  
        ' If the connection string is not valid, or if the specified  
        ' provider does not support sessions, an exception is thrown.  
        objConnection.ConnectionString = connectionString  
        objConnection.Open()  
  
        ' Now that the connection is open, retrieve the new  
        ' active session ID.  
        strSessionID = objConnection.SessionID  
        ' Close the connection, but leave the session open.  
        objConnection.Close(False)  
        Return strSessionID  
  
    Finally  
        objConnection = Nothing  
    End Try  
End Function  
```  
  
```csharp  
static string CreateSession(string connectionString)  
{  
    string strSessionID = "";  
    AdomdConnection objConnection = new AdomdConnection();  
    try  
    {  
        /*First, try to connect to the specified data source.  
          If the connection string is not valid, or if the specified  
          provider does not support sessions, an exception is thrown. */  
        objConnection.ConnectionString = connectionString;  
        objConnection.Open();  
  
        // Now that the connection is open, retrieve the new  
        // active session ID.  
        strSessionID = objConnection.SessionID;  
        // Close the connection, but leave the session open.  
        objConnection.Close(false);  
        return strSessionID;  
    }  
    finally  
    {  
        objConnection = null;  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Aufbauen von Verbindungen in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
  

