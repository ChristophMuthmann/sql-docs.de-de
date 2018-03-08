---
title: "Behandeln von Warnungen und Fällen, die keine Ausnahmen verursachen | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/06/2017
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
- exceptions [Reporting Services], warnings that don't cause
- warnings [Reporting Services]
ms.assetid: 475c0713-6265-44e7-9ebc-ebdd1b89e0af
caps.latest.revision: "30"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 47464e428f2fa10d06b1e02c66b12bc99e7c8da5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="handling-warnings-and-cases-that-do-not-cause-exceptions"></a>Behandeln von Warnungen und Fällen, die keine Ausnahmen verursachen
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] löst keine Ausnahmen für Warnungen und bestimmte Fehler aus. Wenn Sie z. B. die Methode <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> verwenden, um einen neuen Bericht auf dem Berichtsserver zu veröffentlichen, werden alle auftretenden Warnungen als Array der <xref:ReportService2010.Warning>-Objekte zurückgegeben. Diese Warnungen sollten so behandelt und angezeigt werden, dass eine entsprechende Maßnahme getroffen werden kann.  
  
```vb  
Try  
   rs.CreateCatalogItem(name, parentFolder, False, definition, Nothing, warnings)  
  
   If Not (warnings.Length = 0) Then  
      Dim warning As Warning  
      For Each warning In warnings  
         Console.WriteLine(warning.Message)  
      Next warning  
   Else  
      Console.WriteLine("Report {0} created successfully with no warnings", name)  
   End If  
  
Catch ex As SoapException  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.CreateCatalogItem("Report", name, parentFolder, false, definition, null, out warnings);  
  
   if (warnings.Length != 0)  
   {  
      foreach (Warning warning in warnings)  
      {  
         Console.WriteLine(warning.Message);  
      }  
   }  
   else  
      Console.WriteLine("Report {0} created successfully with no warnings", name);  
}  
  
catch (SoapException ex)  
{  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
 Eine andere Möglichkeit der Fehlerbehandlung liegt in der Auswertung der Rückgabewerte bestimmter Methoden. Beispiel: Mithilfe der Methode <xref:ReportService2010.ReportingService2010.FindItems%2A> können bestimmte Elemente in der Berichtsserver-Datenbank gesucht werden. Wenn keine Elemente gefunden werden, die den Suchkriterien entsprechen, wird ein NULL-Array von <xref:ReportService2010.CatalogItem>-Objekten zurückgegeben. Sie sollten das Array auswerten, auf **NULL** prüfen, und den Benutzer informieren, wenn keine Elemente gefunden wurden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 <xref:ReportService2010.CatalogItem>   
 [Introducing Exception Handling in Reporting Services (Einführung in die Ausnahmebehandlung in Reporting Services)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException Class (Reporting Services-SoapException-Klasse)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
