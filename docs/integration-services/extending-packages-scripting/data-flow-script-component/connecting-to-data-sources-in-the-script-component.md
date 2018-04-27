---
title: Herstellen einer Verbindung mit Datenquellen in der Skriptkomponente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: eabc1eaaf12394025f6e40b331fce5fd14b75c30
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Herstellen einer Verbindung zu Datenquellen in der Skriptkomponente 
  Ein Verbindungs-Manager ist eine praktische Einheit, die die Informationen kapselt und speichert, die benötigt werden, um eine Verbindung mit einem bestimmten Datenquellentyp herzustellen. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Sie können vorhandene Verbindungs-Manager über das benutzerdefinierte Skript in der Quell- oder Zielkomponente zum Zugriff freigeben, indem Sie auf der Seite **Verbindungs-Manager** des **Transformations-Editors für Skripterstellung** auf die Schaltfläche **Hinzufügen** oder **Entfernen** klicken. Um Daten zu laden und zu speichern und möglicherweise auch eine Verbindung mit der Datenquelle herzustellen und diese zu beenden, müssen Sie jedoch Ihren eigenen benutzerdefinierten Code schreiben. Weitere Informationen über die Seite **Verbindungs-Manager** im **Transformations-Editor für Skripterstellung** finden Sie unter [Configuring the Script Component in the Script Component Editor (Konfigurieren der Skriptkomponente im Skriptkomponenten-Editor)](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) oder [Script Transformation Editor (Connection Managers Page) (Transformations-Editor für Skripterstellung (Seite „Verbindungs-Manager“))](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 Die Skriptkomponente erstellt im **ComponentWrapper**-Projektelement eine **Connections**-Collectionklasse, die einen stark typisierten Accessor für jeden Verbindungs-Manager enthält, der denselben Namen wie der Verbindungs-Manager trägt. Diese Collection wird von der **Connections**-Eigenschaft der **ScriptMain**-Klasse verfügbar gemacht. Die Accessoreigenschaft gibt einen Verweis auf den Verbindungs-Manager als Instanz von <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> zurück. Wenn Sie beispielsweise auf der Seite Verbindungs-Manager des Dialogfelds den Verbindungs-Manager `MyADONETConnection` hinzugefügt haben, können Sie mit dem folgenden Code im Skript einen Verweis darauf hinzufügen:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  Der Verbindungstyp, der vom Verbindungs-Manager zurückgegeben wird, muss bekannt sein, bevor Sie **AcquireConnection** aufrufen. Da für den Skripttask **Option Strict** aktiviert ist, müssen Sie die Verbindung, die als **Object**-Typ zurückgegeben wird, vor ihrer Verwendung in den richtigen Verbindungstyp umwandeln.  
  
 Anschließend rufen Sie die **AcquireConnection**-Methode des jeweiligen Verbindungs-Managers auf, um entweder die zugrunde liegende Verbindung oder die für die Verbindung mit der Datenquelle erforderlichen Informationen zu erhalten. Mit folgendem Code erhalten Sie beispielsweise einen Verweis auf ein **System.Data.SqlConnection**-Objekt, das von einem ADO.NET-Verbindungs-Manager umschlossen wird:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 Wenn Sie im Gegensatz dazu einen Verbindungs-Manager für Flatfiles aufrufen, wird nur der Pfad und der Dateiname der Dateidatenquelle zurückgegeben.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 Übergeben Sie dann diesen Pfad und den Dateinamen an ein **System.IO.StreamReader**- oder **Streamwriter**-Objekt, um die Daten in der Flatfile zu lesen oder zu schreiben.  
  
> [!IMPORTANT]  
>  Wenn Sie in einer Skriptkomponente verwalteten Code schreiben, können Sie die AcquireConnection-Methode nicht für Verbindungs-Manager wie den OLEDB- oder den Excel-Verbindungs-Manager aufrufen, die nicht verwaltete Objekte zurückgeben. Sie können jedoch die ConnectionString-Eigenschaft dieser Verbindungs-Manager lesen und mithilfe der Verbindungszeichenfolge einer OLEDB-**Verbindung** aus dem **System.Data.OleDb**-Namespace direkt im Code eine Verbindung mit der Datenquelle herstellen.  
>   
>  Wenn Sie die AcquireConnection-Methode eines Verbindungs-Managers aufrufen müssen, der nicht verwaltete Objekte zurückgibt, verwenden Sie einen ADO.NET-Verbindungs-Manager. Wenn Sie den ADO.NET-Verbindungs-Manager zur Verwendung eines OLE DB-Anbieters konfigurieren, stellt er über den .NET Framework-Datenanbieter für OLE DB eine Verbindung her. In diesem Fall gibt die AcquireConnection-Methode ein **System.Data.OleDb.OleDbConnection**-Objekt anstelle eines nicht verwalteten Objekts zurück. Zur Konfiguration eines ADO.NET-Verbindungs-Managers zur Verwendung mit einer Excel-Datenquelle wählen Sie den Microsoft OLEDB-Anbieter für Jet aus, geben eine Excel-Arbeitsmappe an und geben dann `Excel 8.0` (für Excel 97 und höher) als Wert für **Erweiterte Eigenschaften** auf der Seite **Alle** des Dialogfelds **Verbindungs-Manager** ein.  
  
 Weitere Informationen zur Verwendung von Verbindungs-Managern mit der Skriptkomponente finden Sie unter [Creating a Source with the Script Component (Erstellen einer Quelle mit der Skriptkomponente)](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) und [Creating a Destination with the Script Component (Erstellen eines Ziels mit der Skriptkomponente)](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services (SSIS) Connections (Integration Services-Verbindungen (SSIS))](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Erstellen von Verbindungs-Managern](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
