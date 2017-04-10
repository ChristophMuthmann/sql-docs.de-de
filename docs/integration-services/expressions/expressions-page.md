---
title: "Seite Ausdr&#252;cke | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.expressionspage.f1"
helpviewer_keywords: 
  - "Ausdrücke (Seite) (Dialogfeld)"
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Seite Ausdr&#252;cke
  Mithilfe der Seite **Ausdrücke** können Sie Eigenschaftsausdrücke bearbeiten und auf die Dialogfelder **Eigenschaftsausdrucks-Editor** und **Eigenschaftsausdrucks-Generator** zugreifen.  
  
 Eigenschaftsausdrücke aktualisieren die Werte von Eigenschaften, wenn das Paket ausgeführt wird. Eigenschaftsausdrücke können mit den Eigenschaften von Paketen, Tasks, Containern, Verbindungs-Managern sowie einigen Datenflusskomponenten verwendet werden. Die Ausdrücke werden ausgewertet und ihre Ergebnisse werden anstelle der Werte verwendet, auf die Sie die Eigenschaften festgelegt haben, als Sie das Paket und die Paketobjekte konfiguriert haben. Die Ausdrücke können Variablen und die Funktionen und Operatoren enthalten, die die Ausdruckssprache bereitstellt. Beispielsweise können Sie die Betreffzeile für den Task Mail senden generieren, indem Sie den Wert einer Variablen, die die Zeichenfolge "Weather forecast for " enthält, und die zurückgegebenen Ergebnisse der GETDATE()-Funktion zu der Zeichenfolge "Weather forecast for 4/5/2006" verketten.  
  
 Weitere Informationen zum Schreiben von Ausdrücken und zum Verwenden von Eigenschaftsausdrücken finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) und [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## enthalten  
 **Ausdrücke (...)**  
 Klicken Sie auf die Auslassungspunkte (...), um das Dialogfeld **Eigenschaftsausdrucks-Editor** zu öffnen. Weitere Informationen finden Sie unter [Property Expressions Editor](../../integration-services/expressions/property-expressions-editor.md).  
  
 **\<Eigenschaftenname>**  
 Klicken Sie auf die Schaltfläche mit den drei Punkten, um das Dialogfeld **Ausdrucks-Generator** zu öffnen. Weitere Informationen finden Sie unter [Expression Builder](../../integration-services/expressions/expression-builder.md).  
  
## Siehe auch  
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Systemvariablen](../../integration-services/system-variables.md)   
 [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  