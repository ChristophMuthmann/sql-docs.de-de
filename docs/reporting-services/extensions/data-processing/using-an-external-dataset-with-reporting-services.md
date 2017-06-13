---
title: Verwenden eines externen Datasets mit Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSet objects [Reporting Services]
- data processing extensions [Reporting Services], custom DataSet objects
- custom DataSet objects [Reporting Services]
- external DataSet objects [Reporting Services]
ms.assetid: 11daa013-ec17-4760-80e3-6d84cd8d5722
caps.latest.revision: 49
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1521035e49494a2e183ea35a6ad981a710ff52ff
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="using-an-external-dataset-with-reporting-services"></a>Verwenden eines externen Datasets mit Reporting Services
  Die **DataSet** Objekt ist getrennt, für die Unterstützung verteilter Datenszenarien mit [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]. Die **DataSet** Objekt ist eine speicherresidente Darstellung von Daten, auf denen ein konsistentes relationales Programmiermodell unabhängig von der Datenquelle. Es kann mit mehreren verschiedenen Datenquellen verwendet werden, mit XML-Daten oder zur Verwaltung lokaler Daten in einer Anwendung. Die **DataSet** -Objekt stellt einen vollständigen Satz von Daten, einschließlich verknüpfter Tabellen, Einschränkungen und Beziehungen zwischen Tabellen dar. Aufgrund der der **DataSet** objektspezifischen vielseitig beim Speichern und Verfügbarmachen von Daten, die Daten möglicherweise häufig verarbeitet und transformiert Sie in eine **DataSet** Objekt, bevor die Daten in Berichten erfolgt.  
  
 Mit [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -datenverarbeitungserweiterungen können Sie alle benutzerdefinierten integrieren **DataSet** Objekte, die von externen Anwendungen erstellt werden. Um dies zu erreichen, erstellen Sie eine benutzerdefinierte datenverarbeitungserweiterung in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] , fungiert als zwischen Brücke Ihrem **DataSet** Objekt und dem Berichtsserver her. Hauptteil des Codes für die Verarbeitung dieses **DataSet** Objekt befindet sich der **DataReader** Klasse, die Sie erstellen.  
  
 Der erste Schritt beim Verfügbarmachen von Ihrem **DataSet** Objekt auf dem Berichtsserver wird zum Implementieren einer anbieterspezifischen Methode in Ihrer **DataReader** Klasse, die Werte kann ein **DataSet** Objekt. Im folgende Beispiel wird gezeigt, wie zum Laden von statischer Daten in einem **DataSet** Objekt mithilfe einer anbieterspezifischen Methode in Ihrer **DataReader** Klasse.  
  
```vb  
'Private members of the DataReader class  
Private m_dataSet As System.Data.DataSet  
Private m_currentRow As Integer  
  
'Method to create a dataset  
Friend Sub CreateDataSet()  
   ' Create a dataset.  
   Dim ds As New System.Data.DataSet("myDataSet")  
   ' Create a data table.   
   Dim dt As New System.Data.DataTable("myTable")  
   ' Create a data column and set various properties.   
   Dim dc As New System.Data.DataColumn()  
   dc.DataType = System.Type.GetType("System.Decimal")  
   dc.AllowDBNull = False  
   dc.Caption = "Number"  
   dc.ColumnName = "Number"  
   dc.DefaultValue = 25  
   ' Add the column to the table.   
   dt.Columns.Add(dc)  
   ' Add 10 rows and set values.   
   Dim dr As System.Data.DataRow  
   Dim i As Integer  
   For i = 0 To 9  
      dr = dt.NewRow()  
      dr("Number") = i + 1  
      ' Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr)  
   Next i  
  
   ' Fill the dataset.  
   ds.Tables.Add(dt)  
  
   ' Use a private variable to store the dataset in your  
   ' DataReader.  
   m_dataSet = ds  
  
   ' Set the current row to -1.  
   m_currentRow = - 1  
End Sub 'CreateDataSet  
```  
  
```csharp  
// Private members of the DataReader class  
private System.Data.DataSet m_dataSet;  
private int m_currentRow;  
  
// Method to create a dataset  
internal void CreateDataSet()  
{  
   // Create a dataset.  
   System.Data.DataSet ds = new System.Data.DataSet("myDataSet");  
   // Create a data table.   
   System.Data.DataTable dt = new System.Data.DataTable("myTable");  
   // Create a data column and set various properties.   
   System.Data.DataColumn dc = new System.Data.DataColumn();   
   dc.DataType = System.Type.GetType("System.Decimal");   
   dc.AllowDBNull = false;   
   dc.Caption = "Number";   
   dc.ColumnName = "Number";   
   dc.DefaultValue = 25;   
   // Add the column to the table.   
   dt.Columns.Add(dc);   
   // Add 10 rows and set values.   
   System.Data.DataRow dr;   
   for(int i = 0; i < 10; i++)  
   {   
      dr = dt.NewRow();   
      dr["Number"] = i + 1;   
      // Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr);  
   }  
  
   // Fill the dataset.  
   ds.Tables.Add(dt);  
  
   // Use a private variable to store the dataset in your  
   // DataReader.  
   m_dataSet = ds;  
  
   // Set the current row to -1.  
   m_currentRow = -1;  
}  
```  
  
```csharp  
public bool Read()  
{  
   m_currentRow++;  
   if (m_currentRow >= m_dataSet.Tables[0].Rows.Count)   
   {  
      return (false);  
   }   
   else   
   {  
      return (true);  
   }  
}  
  
public int FieldCount  
{  
   // Return the count of the number of columns, which in  
   // this case is the size of the column metadata  
   // array.  
   get { return m_dataSet.Tables[0].Columns.Count; }  
}  
  
public string GetName(int i)  
{  
   return m_dataSet.Tables[0].Columns[i].ColumnName;  
}  
  
public Type GetFieldType(int i)  
{  
   // Return the actual Type class for the data type.  
   return m_dataSet.Tables[0].Columns[i].DataType;  
}  
  
public Object GetValue(int i)  
{  
   return m_dataSet.Tables[0].Rows[m_currentRow][i];  
}  
  
public int GetOrdinal(string name)  
{  
   // Look for the ordinal of the column with the same name and return it.  
   // Returns -1 if not found.  
   return m_dataSet.Tables[0].Columns[name].Ordinal;  
}  
```  
  
 Sobald Sie erstellen oder Ihr Dataset abzurufen, können Sie die **DataSet** Objekt in den Implementierungen der der **lesen**, **GetValue**, **GetName**, **GetOrdinal**, **GetFieldType**, und **FieldCount** Mitglied der **DataReader** Klasse.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
