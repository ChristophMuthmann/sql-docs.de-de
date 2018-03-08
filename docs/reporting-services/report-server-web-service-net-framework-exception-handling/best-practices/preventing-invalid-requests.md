---
title: "Verhindern von ungültigen Anforderungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
caps.latest.revision: "32"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 527b27bc6a0af5195f167bb5ff7f0e84da027ef5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="preventing-invalid-requests"></a>Verhindern von ungültigen Anforderungen
  Sie können verhindern, dass bestimmte Ausnahmearten ausgelöst werden, indem Sie den Anwendungsablauf analysieren und sicherstellen, dass die an den Berichtsserver gesendeten Anforderungen gültig sind. In Anwendungen, in denen die Benutzer den Namen eines Berichts, einer Datenquelle oder eines anderen Berichtsserverelements ändern oder aktualisieren dürfen, sollten Sie beispielsweise den Text, den ein Benutzer eingeben kann, validieren. Sie sollten stets nach reservierten Zeichen suchen, bevor die Anforderung an einen Berichtsserver gesendet werden kann. Verwenden Sie bedingte **if**-Anweisungen oder andere logische Konstrukte im Code, um den Benutzer darauf aufmerksam zu machen, dass die erforderlichen Bedingungen für das Senden der Anforderung an den Berichtsserver nicht erfüllt sind.  
  
 Im folgenden vereinfachten C#-Beispiel erhalten die Benutzer eine freundliche Fehlermeldung, wenn Sie versuchen, einen Bericht mit einem Namen zu erstellen, der einen Schrägstrich (/) enthält.  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 Weitere Informationen zu den verschiedenen Fehlerarten, die verhindert werden können, bevor Anforderungen an den Berichtsserver gesendet werden, finden Sie unter [Tabelle für SoapException-Fehler](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md). Weitere Informationen zur Vertiefung des vorherigen Beispiels mithilfe von try/catch-Blöcken finden Sie unter [Verwenden von Try- und Catch-Blöcken](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Introducing Exception Handling in Reporting Services (Einführung in die Ausnahmebehandlung in Reporting Services)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException Class (Reporting Services-SoapException-Klasse)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
