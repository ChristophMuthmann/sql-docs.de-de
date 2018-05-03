---
title: Behandeln von Fehlern in der TOM-API (Analysis Services AMO-TOM) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ec44daa0-a90e-42ad-b70d-6a7a7a4e4b7b
caps.latest.revision: 4
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a81032f741553717327548b1dbcf812506ce5914
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors-in-the-tom-api-analysis-services-amo-tom"></a>Behandeln von Fehlern in der TOM-API (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Eine gängige Praxis für verwaltete Bibliotheken wie Analysis Services Management Objects (AMO) tabellarisches Objekt Model (TOM) ist die Verwendung von Ausnahmen als Mechanismus für die Berichterstattung von fehlerbedingungen für den Benutzer.  

Wenn ein Fehler im AMO-TOM erkannt wird, als das Auslösen einige .NET Standardausnahmen wie **ArgumentException** und **InvalidOperationException**, TOM kann auch mehrere TOM-spezifische Ausnahmen auslösen.  

TOM Ausnahmen abgeleitet sind [AmoException-Klasse](http://msdn.microsoft.com/library/microsoft.analysisservices.amoexception.aspx), sowohl AMO und TOM-spezifische Ausnahmen abdecken. 

Um die Ausnahmebehandlung in TOM zu veranschaulichen, betrachten wir eine der häufigeren Ausnahmen, die [OperationException Klasse](http://msdn.microsoft.com/library/microsoft.analysisservices.operationexception.aspx).

**OperationException** wird ausgelöst, wenn ein Benutzer einen Vorgang auf dem Analysis Services-Server initiiert und der Server ausfällt, einen Vorgang ausführen, weil die Aktion ungültig war, oder aufgrund eines anderen internen oder externen Fehlers. 

Wenn ausgelöst, ** OperationException ** Objekt enthält eine Liste der vom Server zurückgegebenen XMLA-Fehler. 

Beachten Sie, dass der Server Änderungen nicht akzeptieren, die ungültig sind. In diesem Fall Wiederherstellen der **Modell** Struktur wieder in den letzten bekannten guten Zustand mit der [UndoLocalChanges-Methode](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.model.undolocalchanges.aspx), beheben Sie das Modell, und klicken Sie dann erneut. 

## <a name="code-example-handle-exceptions"></a>Codebeispiel: Ausnahmen behandeln, die 
 
```
 try 
 { 
  // Change the Model, for example create a table. 
  // … 
   model.saveChanges(); 
 } 
  catch(operationException ex) 
 { 
  foreach(XmlaError err in ex.Results.OfType<XmlaError>().cast<XmlaError>()) 
  { 
   Console.WriteLine(“Error returned from the server:” + err.Messsage ); 
  } 
 } 
```

## <a name="next-steps"></a>Nächste Schritte

Andere relevante Ausnahmen umfassen Folgendes:

- [TomInternalException-Klasse](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tominternalexception.aspx)
- [TomValidationException-Klasse](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tomvalidationexception.aspx)
- [JsonSerializationException-Klasse](http://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_JsonSerializationException.htm)
