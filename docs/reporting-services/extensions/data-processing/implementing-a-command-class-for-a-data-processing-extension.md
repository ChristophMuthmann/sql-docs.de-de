---
title: "Implementieren eine Befehlsklasse für a Data Processing Extension | Microsoft Docs"
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
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: b601aa43ecce5347f7229999455360be761f3bd3
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>Implementieren einer Command-Klasse für Datenverarbeitungserweiterungen
  Die **Befehl** -Objekt formuliert eine Anforderung und übergibt sie an der Datenquelle. Der Befehlstext kann viele verschiedene syntaktische Formate haben, einschließlich Text und XML. Wenn Ergebnisse zurückgegeben werden, die **Befehl** Objekt gibt Ergebnisse zurück wie eine **DataReader** Objekt.  
  
 Zum Erstellen einer **Befehl** -Klasse, implementieren Sie <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>. Implementieren der <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> Methode, um ein Ergebnis zurückzugeben, legen Sie als eine **DataReader** Objekt. Die <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> Methode Ihrer **Befehl** Klasse sollte eine Implementierung, die akzeptiert enthalten eine <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> -Aufzählung als Argument. Wenn Sie die Datenverarbeitungserweiterungen im Berichts-Designer bereitstellen, geben Sie eine Implementierung an, die einen <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly>-Fall in der Methode <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> behandelt. Eine Schema-Only-Implementierung wird verwendet, um dem Berichts-Designer eine Felderliste zur Verfügung zu stellen. Die **DataReader** zurückgegebenes Objekt die <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> Methode muss Typen- und Namensdaten für die Felder enthalten, oder legen Sie die Spalten, in Ihrem Resultset.  
  
 Optional, Ihre **Befehl** Klasse implementieren kann <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>. Mithilfe dieser Oberfläche kann eine Implementierungsklasse eine Abfrage analysieren und eine Parameterliste in der Abfrage zurückgeben. Die Funktionen der <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>-Schnittstelle werden nur im Berichts-Designer verwendet. Wenn Sie <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> implementieren, können Benutzer des Berichts-Designers zur Eingabe von Parametern aufgefordert werden, wenn ein Bericht im Vorschaumodus ausgeführt wird. Darüber hinaus sehen Sie die Parameter in der **Parameter** auf der Registerkarte die **DataSet** Dialogfeld.  
  
> [!NOTE]  
>  Sie sollten <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> nicht implementieren, wenn die benutzerdefinierte Datenverarbeitungserweiterung keine Parameter unterstützt.  
  
 Ein Beispiel **Befehl** -klassenimplementierung, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
