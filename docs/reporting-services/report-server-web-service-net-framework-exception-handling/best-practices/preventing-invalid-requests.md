---
title: "Verhindern von ungültigen Anforderungen | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4ec670f66ad710e0f9a21f03681aedcac943ef35
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="preventing-invalid-requests"></a>Verhindern von ungültigen Anforderungen
  Sie können verhindern, dass bestimmte Ausnahmearten ausgelöst werden, indem Sie den Anwendungsablauf analysieren und sicherstellen, dass die an den Berichtsserver gesendeten Anforderungen gültig sind. In Anwendungen, in denen die Benutzer den Namen eines Berichts, einer Datenquelle oder eines anderen Berichtsserverelements ändern oder aktualisieren dürfen, sollten Sie beispielsweise den Text, den ein Benutzer eingeben kann, validieren. Sie sollten stets nach reservierten Zeichen suchen, bevor die Anforderung an einen Berichtsserver gesendet werden kann. Verwenden Sie den bedingten **Wenn** -Anweisungen oder andere logische Konstrukte im Code, um die Benutzer darauf hinzuweisen, dass sie die zum Senden von Anforderungen auf dem Berichtsserver erforderlichen Bedingungen nicht erfüllt sind.  
  
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
  
 Weitere Informationen zu den verschiedenen Fehlerarten, die verhindert werden können, bevor Anforderungen an den Berichtsserver gesendet werden, finden Sie unter [SoapException Tabelle "Fehler"](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md). Weitere Informationen zur Vertiefung des vorherigen Beispiels mithilfe von Try/Catch-Blöcken finden Sie unter [versuchen und Catch-Blöcke](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Einführung in die Ausnahmebehandlung in Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services-SoapException-Klasse](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
