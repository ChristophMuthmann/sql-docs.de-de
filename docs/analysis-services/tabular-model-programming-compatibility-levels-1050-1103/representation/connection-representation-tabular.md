---
title: Verbindungsdarstellung (tabellarisch) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 4b410b16-d36e-4185-bb20-922e66e5e2b7
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ea8e493f0f1d6e8a53e4e0ef8cfe6620bf37d7e2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="connection-representation-tabular"></a>Verbindungsdarstellung (tabellarisch)
  Das Verbindungsobjekt definiert die Quelle der Daten, die das tabellarische Modell auffüllen.  
  
## <a name="connection-representation"></a>Verbindungsdarstellung  
 Die Spezifikation für das Verbindungsobjekt folgt den Regeln für OLE DB-Anbieter.  
  
### <a name="connection-in-amo"></a>Verbindung in AMO  
 Wenn eine tabellarische Modelldatenbank mithilfe von AMO verwaltet wird, entspricht das <xref:Microsoft.AnalysisServices.DataSource>-Objekt in AMO 1:1 dem logischen Verbindungsobjekt.  
  
 Der folgende Codeausschnitt veranschaulicht, wie eine AMO-Datenquelle oder ein Verbindungsobjekt in einem tabellarischen Modell erstellt wird.  
  
```  
  
//Create an OLEDB connection string  
StringBuilder SqlCnxStr = new StringBuilder();  
SqlCnxStr.Append(String.Format("Data Source={0};" ,SQLServer.Text));  
SqlCnxStr.Append(String.Format("Initial Catalog={0};", SQLDatabase.Text));  
SqlCnxStr.Append(String.Format("Persist Security Info={0};", false));  
SqlCnxStr.Append(String.Format("Integrated Security={0};", "SSPI"));  
SqlCnxStr.Append(String.Format("Provider={0}", "SQLNCLI11"));  
String DatasourceCnxString = SqlCnxStr.ToString();  
  
//Verify connection string and connectivity  
System.Data.OleDb.OleDbConnection OleDbCnx = new System.Data.OleDb.OleDbConnection(DatasourceCnxString);  
try  
{  
    OleDbCnx.Open();  
}  
catch ()  
{  
    throw;  
}  
String newDataSourceName = (string.IsNullOrEmpty(DataSourceName.Text) || string.IsNullOrWhiteSpace(DataSourceName.Text)) ? SQLDatabase.Text : DataSourceName.Text;  
AMO.DataSource newDatasource = newDatabase.DataSources.Add(newDataSourceName, newDataSourceName);  
newDatasource.ConnectionString = DatasourceCnxString.Text;  
if (impersonateServiceAccount.Checked)  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateServiceAccount);  
else  
{  
    if (String.IsNullOrEmpty(impersonateAccountUserName.Text))  
    {  
        MessageBox.Show(String.Format("Account User Name cannot be blank when using 'ImpersonateAccount' mode"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        return;  
    }  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateAccount, impersonateAccountUserName.Text, impersonateAccountPassword.Text);  
}  
newDatasource.Update();  
  
```  
  
## <a name="tabular-amo-2012-sample"></a>Tabular AMO 2012-Beispiel  
 Um ein besseres Verständnis für die Verwendung von AMO zur Erstellung und Bearbeitung von verbindungsdarstellungen, finden Sie in der Quellcode in der Stichprobe Tabular AMO 2012; Prüfen Sie insbesondere die Quelldatei: Database.cs. Das Beispiel ist auf Codeplex verfügbar. Beispielcode wird nur zur Verdeutlichung der hier erläuterten logischen Konzepte bereitgestellt und sollte nicht in einer Produktionsumgebung verwendet werden.  
  
  
