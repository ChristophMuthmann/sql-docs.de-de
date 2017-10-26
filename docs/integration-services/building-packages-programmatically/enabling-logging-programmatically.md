---
title: Programmgesteuertes Aktivieren der Protokollierung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: dd512f022832b57aa3fdcb85260926dd8354298c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="enabling-logging-programmatically"></a>Programmgesteuertes Aktivieren der Protokollierung
  Das Laufzeitmodul stellt eine Auflistung von <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider>-Objekten bereit, mit deren Hilfe ereignisspezifische Informationen während der Paketüberprüfung und -ausführung aufgezeichnet werden können. <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider>-Objekte sind für <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer>-Objekte verfügbar; hierzu zählen auch die Objekte <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, <xref:Microsoft.SqlServer.Dts.Runtime.Package>, <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> und <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>. Die Protokollierung wird für einzelne Container oder das gesamte Paket aktiviert.  
  
 Es gibt mehrere Typen von Protokollanbietern, die für einen zu verwendenden Container verfügbar sind. Dies bietet die Flexibilität, Protokollinformationen in vielen verschiedenen Formaten erstellen und speichern zu können. Das Eintragen eines Containerobjekts zur Protokollierung umfasst zwei Schritte. Zuerst wird die Protokollierung aktiviert, und im zweiten Schritt wird ein Protokollanbieter ausgewählt. Die Eigenschaften <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> und <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> des Containers werden zum Angeben der protokollierten Ereignisse und zum Auswählen des Protokollanbieters verwendet.  
  
## <a name="enabling-logging"></a>Aktivieren der Protokollierung  
 Die <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A>-Eigenschaft ist in jedem Container verfügbar, der eine Protokollierung ausführen kann, und legt fest, ob die Ereignisinformationen des Containers im Ereignisprotokoll aufgezeichnet werden. Der Eigenschaft wird ein Wert aus der <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>-Struktur zugewiesen, sie wird standardmäßig vom übergeordneten Container geerbt. Die Eigenschaft wird verwendet, wenn der Container ein Paket ist und daher kein übergeordnetes Element verfügt, das <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>, die standardmäßig die **deaktiviert**.  
  
### <a name="selecting-a-log-provider"></a>Auswählen eines Protokollanbieters  
 Nach der <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> -Eigenschaftensatz auf **aktiviert**, ein Protokollanbieter hinzugefügt wird die <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> -Auflistung des Containers, um den Vorgang abzuschließen. Die <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders>-Auflistung steht im <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions>-Objekt zur Verfügung und enthält die für den Container ausgewählten Protokollanbieter. Zum Erstellen eines Anbieters und Hinzufügen dieses Anbieters zu einer Auflistung wird die <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A>-Methode aufgerufen. Die Methode gibt daraufhin den Protokollanbieter zurück, der der Auflistung hinzugefügt wurde. Jeder Anbieter verfügt über eindeutige Konfigurationseinstellungen, und diese Eigenschaften werden mithilfe der <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>-Eigenschaft festgelegt.  
  
 In der folgenden Tabelle werden die verfügbaren Protokollanbieter, ihre Beschreibung und ihre <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>-Informationen aufgeführt.  
  
|Anbieter|Description|ConfigString-Eigenschaft|  
|--------------|-----------------|---------------------------|  
|SQL Server Profiler|Generiert SQL-Ablaufverfolgungen, die aufgezeichnet und im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Profiler angezeigt werden können. Die standardmäßige Dateinamenerweiterung für diesen Anbieter ist TRC.|Es ist keine Konfiguration erforderlich.|  
|SQL Server|Schreibt Ereignisprotokolleinträge in die **Sysssislog** Tabelle in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anbieter erfordert eine angegebene Verbindung zur Datenbank sowie den Namen der Zieldatenbank.|  
|Textdatei|Schreibt Ereignisprotokolleinträge im durch Trennzeichen getrennten CSV-Format in ASCII-Textdateien. Die standardmäßige Dateinamenerweiterung für diesen Anbieter ist LOG.|Der Name eines Dateiverbindungs-Managers.|  
|Windows-Ereignisprotokoll|Schreibt Protokolle in das Anwendungsprotokoll im standardmäßigen Windows-Ereignisprotokoll auf dem lokalen Computer.|Es ist keine Konfiguration erforderlich.|  
|XML-Datei|Schreibt Ereignisprotokolleinträge in Dateien im XML-Format. Die standardmäßige Dateinamenerweiterung für diesen Anbieter ist XML.|Der Name eines Dateiverbindungs-Managers.|  
  
 Ereignisse enthalten sind, oder aus dem Ereignisprotokoll ausgeschlossen werden, indem die **EventFilterKind** und **EventFilter** Eigenschaften des Containers. Der **EventFilterKind** Struktur enthält zwei Werte **ExclusionFilter** und **InclusionFilter**, die angeben, ob die Ereignisse, die sind hinzugefügt der **EventFilter** in das Ereignisprotokoll enthalten sind. Die **EventFilter** Eigenschaft ist ein Zeichenfolgenarray, das die Namen der Ereignisse, die Gegenstand enthält der Filterung sind, dann zugewiesen.  
  
 Mit dem folgenden Code wird die Protokollfunktion eines Pakets aktiviert, der Protokollanbieter für Textdateien zur <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders>-Auflistung hinzugefügt und eine Liste der Ereignisse angegeben, die in die Protokollausgabe aufgenommen werden sollen.  
  
## <a name="sample"></a>Beispiel  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      ConnectionManager loggingConnection = p.Connections.Add("FILE");  
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";  
  
      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");  
      provider.ConfigString = loggingConnection.Name;  
      p.LoggingOptions.SelectedLogProviders.Add(provider);  
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;  
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute",   
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };  
      p.LoggingMode = DTSLoggingMode.Enabled;  
  
      // Add tasks and other objects to the package.  
  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
  
    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")  
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"  
  
    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")  
    provider.ConfigString = loggingConnection.Name  
    p.LoggingOptions.SelectedLogProviders.Add(provider)  
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion  
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _  
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}  
    p.LoggingMode = DTSLoggingMode.Enabled  
  
    ' Add tasks and other objects to the package.  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

