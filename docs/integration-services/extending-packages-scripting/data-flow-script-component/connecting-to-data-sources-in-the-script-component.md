---
title: Connecting to Data Sources in the Script Component | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2accca553f1bd9c536076fd0bbcebbff0ff2c42
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Herstellen einer Verbindung zu Datenquellen in der Skriptkomponente 
  Ein Verbindungs-Manager ist eine praktische Einheit, die die Informationen kapselt und speichert, die benötigt werden, um eine Verbindung mit einem bestimmten Datenquellentyp herzustellen. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Sie können vorhandene Verbindungs-Manager verfügbar machen für den Zugriff über das benutzerdefinierte Skript in der Quelle oder Ziel durch Klicken auf die **hinzufügen** und **entfernen** Schaltflächen auf der **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**. Um Daten zu laden und zu speichern und möglicherweise auch eine Verbindung mit der Datenquelle herzustellen und diese zu beenden, müssen Sie jedoch Ihren eigenen benutzerdefinierten Code schreiben. Weitere Informationen zu den **Verbindungs-Manager** auf der Seite der **Skript Transformations-Editor**, finden Sie unter [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) und [Skript Transformations-Editor &#40; Verbindungsseite-Manager &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 Die Skriptkomponente erstellt eine **Verbindungen** Auflistungsklasse in der **ComponentWrapper** -Projektelement, die einen stark typisierten Accessor für jeden Verbindungs-Manager mit den gleichen Namen wie der Verbindungs-Manager enthalten ist. Diese Auflistung abgelesen der **Verbindungen** Eigenschaft von der **ScriptMain** Klasse. Die Accessoreigenschaft gibt einen Verweis auf den Verbindungs-Manager als Instanz von <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> zurück. Wenn Sie beispielsweise auf der Seite Verbindungs-Manager des Dialogfelds den Verbindungs-Manager `MyADONETConnection` hinzugefügt haben, können Sie mit dem folgenden Code im Skript einen Verweis darauf hinzufügen:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  Benötigen Sie die Art der Verbindung, die vom Verbindungs-Manager zurückgegeben wird, vor dem Aufruf **AcquireConnection**. Da der Skripttask **Option Strict** aktiviert ist, müssen Sie die Verbindung, der zurückgegeben wird, als Typ umwandeln **Objekt**, um den richtigen Verbindungstyp, bevor Sie ihn verwenden können.  
  
 Anschließend rufen Sie die **AcquireConnection** Methode des jeweiligen Verbindungs-Managers zu erhalten, die zugrunde liegende Verbindung oder die Informationen, die für die Verbindung mit der Datenquelle erforderlich sind. Sie erhalten z. B. einen Verweis auf die **System.Data.SqlConnection** umschlossen einen ADO.NET-Verbindungs-Manager mit dem folgenden Code:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 Wenn Sie im Gegensatz dazu einen Verbindungs-Manager für Flatfiles aufrufen, wird nur der Pfad und der Dateiname der Dateidatenquelle zurückgegeben.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 Übergeben Sie dann diesen Pfad und Dateinamen ein, um eine **System.IO.StreamReader** oder **Streamwriter** zum Lesen oder schreiben die Daten in der Flatfile.  
  
> [!IMPORTANT]  
>  Wenn Sie in einer Skriptkomponente verwalteten Code schreiben, können nicht Sie die AcquireConnection-Methode der Connection Manager aufrufen, die nicht verwaltete Objekte, z. B. der OLE DB-Verbindungs-Manager und der Excel-Verbindungs-Manager zurückgeben. Jedoch die "ConnectionString"-Eigenschaft dieser Verbindungs-Manager gelesen werden können, und Verbinden mit der Datenquelle direkt im Code mithilfe der Verbindungszeichenfolge einer OLEDB- **Verbindung** aus der **"System.Data.OleDb"** Namespace.  
>   
>  Wenn Sie müssen zum Aufrufen der AcquireConnection-Methode eines Verbindungs-Managers, die nicht verwaltete Objekte zurückgibt, verwenden Sie einen ADO.NET-Verbindungs-Manager. Wenn Sie den ADO.NET-Verbindungs-Manager zur Verwendung eines OLE DB-Anbieters konfigurieren, stellt er über den .NET Framework-Datenanbieter für OLE DB eine Verbindung her. In diesem Fall die AcquireConnection-Methode gibt ein **System.Data.OleDb.OleDbConnection** anstelle eines nicht verwalteten Objekts. Um einen ADO.NET-Verbindungs-Manager für die Verwendung mit einer Excel-Datenquelle konfigurieren möchten, wählen Sie den Microsoft OLE DB-Anbieter für Jet, geben Sie eine Excel-Arbeitsmappe, und geben Sie dann `Excel 8.0` (für Excel 97 und höher) als Wert des **erweiterte Eigenschaften** auf die **alle** auf der Seite der **Verbindungs-Manager** (Dialogfeld).  
  
 Weitere Informationen zur Verwendung von Verbindungs-Manager mit der Skriptkomponente finden Sie unter [Erstellen einer Datenquelle mit der Skriptkomponente](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) und [Erstellen eines Ziels mit der Skriptkomponente](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Erstellen von Verbindungs-Manager](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
