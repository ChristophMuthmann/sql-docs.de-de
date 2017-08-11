---
title: Initialisieren von Objekten benutzerdefinierter Assemblys | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ab05efc7baba58a34180faa038cb58c7f57f4af2
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="initializing-custom-assembly-objects"></a>Initialisieren von Objekten benutzerdefinierter Assemblys
  In einigen Fällen müssen Sie die Werte der Eigenschaften und Felder in Ihren benutzerdefinierten Assemblyklassen beim Instanziieren initialisieren. Wahrscheinlich müssen Sie die benutzerdefinierten Klassen mit den Werten initialisieren, die Ihnen von den globalen Objektauflistungen des Berichts zur Verfügung stehen. Überschreiben Sie dazu die **OnInit** Methode der **Code** -Objekts eines Berichts. Für den Zugriff auf **OnInit**, verwenden Sie die **Code** -Element der Berichtsdefinition. Es gibt zwei Verfahren zum Initialisieren der Eigenschaft oder ein Feld Werte der Klassen in einer benutzerdefinierten Assembly, die Sie in Ihrem Bericht verwenden möchten: Sie können entweder deklarieren und erstellen Sie eine neue Instanz Ihrer Klasse verwenden **OnInit**, oder rufen Sie eine öffentlich verfügbare Methode mit **OnInit**.  
  
## <a name="global-object-collections-and-initialization"></a>Globale Objektauflistungen und Initialisierung  
 Zum Initialisieren der benutzerdefinierten Klassenvariablen stehen Ihnen mehrere Auflistungen zur Verfügung. Sie können die **Globals** und **Benutzer** Sammlungen. Die **Parameter**, **Felder** und **ReportItems** Auflistungen sind nicht für Sie verfügbar, die zum Zeitpunkt des berichtslebensdauerzyklus bei der **OnInit** Methode aufgerufen wird. Verwenden Sie die freigegebenen Auflistungen, **Globals** oder **Benutzer**, müssen Sie die **Bericht** -Objektverweis. Z. B. zum Initialisieren der benutzerdefinierten Klasse anhand der aktuellen Sprache des auf den Bericht zugreifenden Benutzers Ihrer **Code** Element könnte wie folgt aussehen:  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Eine Möglichkeit, die Eigenschaften- und Feldwerte einer Klasse zu initialisieren (wie bereits zuvor gezeigt), besteht darin, die neue Klasse zu deklarieren und eine neue Instanz davon zu erstellen, indem Sie einen überschriebenen Konstruktor aufrufen.  
  
 Eine weitere Möglichkeit zum Initialisieren der Werte Eigenschaften- und Feldwerte der Klassen in Ihren benutzerdefinierten Assemblys wird zum Aufrufen einer öffentlich verfügbaren Methode, die Sie definieren, aus der **OnInit** Methode. Sie müssen zuerst in der Berichtsdefinitionsdatei einen Instanznamen für die Klasse hinzufügen. Sobald Sie den entsprechenden Assemblyverweis und den Instanznamen hinzugefügt haben, können Sie die Initialisierungsmethode aufrufen, um die Eigenschaften- und Feldwerte für Ihre Klasse zu initialisieren. Ihre **OnInit** Methode kann wie folgt aussehen:  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Weitere Informationen zum Hinzufügen von Namen einer Assembly und den Instanznamen für die benutzerdefinierte Klasse finden Sie unter [Hinzufügen eines Assemblyverweises zu einem Bericht &#40; SSRS &#41; ](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Weitere Informationen zu globalen objektauflistungen finden Sie unter [integrierte Auflistungen in Ausdrücken &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
