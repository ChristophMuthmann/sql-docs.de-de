---
title: Connecting to Data Sources in the Script Task | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 825ff059476614085a338dd9c568031885bed64b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Herstellen einer Verbindung zu Datenquellen im Skripttask 
  Verbindungs-Manager bieten Zugriff auf Datenquellen, die im Paket konfiguriert wurden. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Der Skripttask erreichen dieser Verbindungs-Manager über die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> Eigenschaft von der **Dts** Objekt. Jeder Verbindungs-Manager in der <xref:Microsoft.SqlServer.Dts.Runtime.Connections>-Auflistung speichert Informationen darüber, wie eine Verbindung mit der zugrunde liegenden Datenquelle hergestellt werden kann.  
  
 Wenn Sie die <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A>-Methode eines Verbindungs-Managers aufrufen, stellt der Verbindungs-Manager eine Verbindung zur Datenquelle her (falls diese nicht bereits besteht), und gibt die entsprechenden Verbindungsinformationen zur Verwendung im Skripttaskcode zurück.  
  
> [!NOTE]  
>  Benötigen Sie die Art der Verbindung vom Verbindungs-Manager vor dem Aufruf zurückgegeben **AcquireConnection**. Da der Skripttask **Option Strict** aktiviert ist, müssen Sie die Verbindung, der zurückgegeben wird, als Typ umwandeln **Objekt**, um den richtigen Verbindungstyp, bevor Sie ihn verwenden können.  
  
 Sie können die <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Runtime.Connections>-Auflistung verwenden, die von der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>-Eigenschaft zurückgegeben wird, um nach einer vorhandenen Verbindung zu suchen, bevor Sie diese Verbindung im Code verwenden.  
  
> [!IMPORTANT]  
>  Der AcquireConnection-Methode von Verbindungs-Managern, die nicht verwaltete Objekte, z. B. der OLE DB-Verbindungs-Manager und der Excel-Verbindungs-Manager im verwalteten Code eines Skripttasks zurückgeben, kann nicht abgerufen werden. Allerdings lesen Sie die "ConnectionString"-Eigenschaft dieser Verbindungs-Manager werden können, und Verbinden mit der Datenquelle direkt im Code mithilfe der Verbindungszeichenfolge mit einer **OledbConnection** aus der **"System.Data.OleDb"** Namespace.  
>   
>  Wenn Sie die AcquireConnection-Methode einer Verbindung Manager, die nicht verwaltete Objekte zurückgibt aufrufen müssen, verwenden Sie eine [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Verbindungs-Manager. Wenn Sie den [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]-Verbindungs-Manager zur Verwendung eines OLE DB-Anbieters konfigurieren, stellt er über den [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Datenanbieter für OLE DB eine Verbindung her. In diesem Fall die AcquireConnection-Methode gibt ein **System.Data.OleDb.OleDbConnection** anstelle eines nicht verwalteten Objekts. So konfigurieren Sie eine [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Verbindungs-Manager für die Verwendung mit einer Excel-Datenquelle, wählen Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB-Anbieter für Jet, geben Sie eine Exceldatei, und geben Sie `Excel 8.0` (für Excel 97 und höher) als Wert des **erweiterte Eigenschaften** auf die **alle** auf der Seite der **Verbindungs-Manager** (Dialogfeld).  
  
## <a name="connections-example"></a>Verbindungsbeispiel  
 Im folgenden Beispiel wird veranschaulicht, wie Verbindungs-Manager innerhalb des Skripttasks aufgerufen werden können. Im Beispiel wird davon ausgegangen, dass Sie erstellt und konfiguriert eine [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Verbindungs-Manager mit dem Namen **Test ADO.NET Connection** und einem Flatfile-Verbindungs-Manager mit dem Namen **Test Flat File Connection**. Beachten Sie, dass die [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Verbindungs-Manager gibt einen **SqlConnection** -Objekt, das Sie sofort verwenden können, für die Verbindung mit der Datenquelle. Der Verbindungs-Manager für Flatfiles gibt im Gegensatz dazu nur eine Zeichenfolge mit Pfad und Dateinamen zurück. Müssen Sie Methoden verwenden das **System.IO** Namespace geöffnet und bearbeitet werden, mit der Flatfile-Datei.  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Erstellen von Verbindungs-Manager](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

