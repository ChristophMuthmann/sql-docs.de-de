---
title: "Hinzuf&#252;gen eines Assemblyverweises zu einem Bericht (SSRS) | Microsoft Docs"
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
  - "Benutzerdefinierte Assemblys [Reporting Services], verweisen"
  - "Benutzerdefinierter Code [Reporting Services]"
  - "Hinzufügen von Assemblyverweisen"
  - "Assemblys [Reporting Services], Verweise"
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
caps.latest.revision: 43
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 43
---
# Hinzuf&#252;gen eines Assemblyverweises zu einem Bericht (SSRS)
  Wenn Sie benutzerdefinierten Code einbetten, der Verweise auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassen enthält, die sich nicht in <xref:System.Math> oder <xref:System.Convert> befinden, müssen Sie einen Assemblyverweis auf den Bericht bereitstellen, damit der Berichtsprozessor die Namen auflösen kann. Weitere Informationen finden Sie unter [Hinzufügen von Code zu einem Bericht &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md).  
  
### So fügen Sie einen Assemblyverweis einem Bericht hinzu  
  
1.  Klicken Sie in der **Entwurfsansicht** mit der rechten Maustaste auf die Entwurfsoberfläche außerhalb des Rahmens des Berichts, und klicken Sie auf **Berichtseigenschaften**.  
  
2.  Klicken Sie auf **Verweise**.  
  
3.  Klicken Sie in **Assemblys hinzufügen oder entfernen**auf **Hinzufügen** , und klicken Sie dann auf die Schaltfläche mit den Auslassungspunkten, um zur Assembly zu wechseln.  
  
4.  Klicken Sie unter **Klassen hinzufügen oder entfernen**auf **Hinzufügen** , und geben Sie dann den Namen der Klasse ein. Geben Sie außerdem einen Instanznamen an, der im Bericht verwendet werden soll.  
  
    > [!NOTE]  
    >  Geben Sie nur für instanzbasierte Mitglieder einen Klassen- und Instanznamen an. Geben Sie in der Liste **Klassen** keine statischen Mitglieder an. Weitere Informationen finden Sie unter [Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Berichtseigenschaften (Dialogfeld), Verweise](../Topic/Report%20Properties%20Dialog%20Box,%20References.md)  
  
  