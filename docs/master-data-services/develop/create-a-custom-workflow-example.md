---
title: "Beispiel für einen benutzerdefinierten Workflow (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d797fa15beed3babd34d0fdeccf0a607ef41b715
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-custom-workflow---example"></a>Erstellen eines benutzerdefinierten Workflows – Beispiel
  Wenn Sie in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] eine benutzerdefinierte Klassenbibliothek für den Workflow erstellen, erstellen Sie eine Klasse, die die Schnittstelle „Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender“ implementiert. Diese Schnittstelle beinhaltet eine Methode, <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>, die beim Start eines Workflows vom SQL Server MDS Workflow Integration Service aufgerufen wird. Die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>-Methode enthält zwei Parameter: *workflowType* enthält den Text, den Sie in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] in das Textfeld **Workflowtyp** eingegeben haben, und *dataElement* enthält Metadaten sowie Elementdaten für das Element, das die Workflowgeschäftsregel ausgelöst hat.  
  
## <a name="custom-workflow-example"></a>Beispiel für einen benutzerdefinierten Workflow  
 Das folgende Codebeispiel veranschaulicht die Implementierung der <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>-Methode zum Extrahieren der Namens-, Code- und LastChgUserName-Attribute von den XML-Daten für das Element, das die Workflowgeschäftsregel ausgelöst hat. Zudem erfahren Sie, wie eine gespeicherte Prozedur zum Einfügen der Attribute in eine andere Datenbank aufgerufen wird. Ein Beispiel für die Elementdaten-XML und eine Erläuterung der enthaltenen Tags finden Sie unter [Benutzerdefinierte Workflow-XML-Beschreibung &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
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
 [Erstellen eines benutzerdefinierten Workflows &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
