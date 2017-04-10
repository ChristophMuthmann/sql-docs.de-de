---
title: "Hinzuf&#252;gen von Code zu einem Bericht (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Code [Reporting Services]"
  - "Benutzerdefinierter Code [Reporting Services]"
  - "Ausdrücke [Reporting Services], Code"
  - "Hinzufügen von Code"
  - "Berichte [Reporting Services], Code"
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
caps.latest.revision: 41
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 41
---
# Hinzuf&#252;gen von Code zu einem Bericht (SSRS)
  Sie können in jedem beliebigen Ausdruck einen eigenen benutzerdefinierten Code aufrufen. Sie können Code auf folgende zwei Arten bereitstellen:  
  
-   Betten Sie in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] geschriebenen Code direkt in Ihren Bericht ein. Falls der Code auf ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] verweist, das nicht <xref:System.Math> oder <xref:System.Convert> ist, müssen Sie dem Bericht den Verweis hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Assemblyverweises zu einem Bericht &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md). Weitere Informationen zu anderen Verweisen finden Sie unter [Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
-   Stellen Sie mit dem [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]eine benutzerdefinierte Codeassembly bereit. Wenn Sie eine benutzerdefinierte Assembly bereitstellen, müssen Sie sie sowohl auf dem Computer, auf dem Sie den Bericht schreiben, als auch auf dem Berichtsserver, auf dem Sie den Bericht anzeigen, installieren. Weitere Informationen finden Sie unter [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md).  
  
### So fügen Sie einem Bericht eingebetteten Code hinzu  
  
1.  Klicken Sie in der **Entwurfsansicht** mit der rechten Maustaste auf die Entwurfsoberfläche außerhalb des Rahmens des Berichts, und klicken Sie auf **Berichtseigenschaften**.  
  
2.  Klicken Sie auf **Code**.  
  
3.  Geben Sie den Code unter **Benutzerdefinierter Code**ein. Fehler im Code erzeugen Warnungen, wenn der Bericht ausgeführt wird. Im folgenden Beispiel wird eine benutzerdefinierte Funktion namens `ChangeWord` erstellt, die das Wort "`Bike`" mit "`Bicycle`" ersetzt.  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  Im folgenden Beispiel wird gezeigt, wie ein Datasetfeld namens Kategorie in einem Ausdruck an diese Funktion übergeben wird:  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     Wenn Sie diesen Ausdruck einer Tabellenzelle hinzufügen, in der Kategoriewerte angezeigt werden, wird, wenn das Wort "Bike" im Datasetfeld für diese Zeile enthalten ist, stattdessen das Wort "Bicycle" als Tabellenzellenwert angezeigt.  
  
## Siehe auch  
 [Berichtseigenschaften (Dialogfeld), Code](../Topic/Report%20Properties%20Dialog%20Box,%20Code.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Verweise auf Parametersammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/parameters-collection-references-report-builder-and-ssrs.md)  
  
  