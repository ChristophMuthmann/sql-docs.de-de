---
title: "Beispiel für einen benutzerdefinierten Workflow (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2b3ad5ab349456364d2aa0af8826dd6970e55b1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---example"></a>Erstellen Sie einen benutzerdefinierten Workflow - Beispiel
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], bei der Erstellung einer benutzerdefinierten Workflow-Klassenbibliothek, erstellen Sie eine Klasse, die die Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender-Schnittstelle implementiert. Diese Schnittstelle beinhaltet eine Methode, <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>, d. h. von SQL Server MDS Workflow Integration Service aufgerufen, wenn ein Workflow startet. Die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> Methode enthält zwei Parameter: *WorkflowType* enthält den Text, die Sie eingegeben, in haben der **Workflowtyp** in das Textfeld [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], und *DataElement* enthält Metadaten sowie Elementdaten Daten für das Element, das die workflowgeschäftsregel ausgelöst hat.  
  
## <a name="custom-workflow-example"></a>Beispiel für einen benutzerdefinierten Workflow  
 Das folgende Codebeispiel veranschaulicht die Implementierung der <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>-Methode zum Extrahieren der Namens-, Code- und LastChgUserName-Attribute von den XML-Daten für das Element, das die Workflowgeschäftsregel ausgelöst hat. Zudem erfahren Sie, wie eine gespeicherte Prozedur zum Einfügen der Attribute in eine andere Datenbank aufgerufen wird. Ein Beispiel für die Elementdaten-XML und eine Erläuterung der enthaltenen Tags finden Sie unter [benutzerdefinierte Workflow-XML-Beschreibung &#40; Master Data Services &#41; ](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie einen benutzerdefinierten Workflow &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
