---
title: Debuggen gespeicherter Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- debugging stored procedures [Analysis Services]
- stored procedures [Analysis Services], debugging
ms.assetid: 34f51b85-02b3-40dd-bf93-375a9e522385
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a2bec11c4a5d374c7e4dc2b9cc5a264c69402853
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="debugging-stored-procedures"></a>Debuggen gespeicherter Prozeduren
  Gespeicherte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Prozeduren sind eigentlich CLR- oder COM-Bibliotheken (normalerweise DLLs), die in C# (oder in einer anderen CLR- oder COM-Sprache) geschrieben sind. Das Debuggen einer gespeicherten Prozedur entspricht also im Wesentlichen dem Debuggen jeder anderen Anwendung in der Debugumgebung von Visual Studio. Sie debuggen gespeicherte Prozeduren in der Visual Studio-Entwicklungsumgebung mithilfe integrierter Debugfunktionen. Mit diesen können Sie an Prozedurspeicherorten stoppen, Speicher inspizieren und Werte registrieren, Variablen ändern, den Nachrichtenverkehr beobachten und einen genauen Blick auf das Funktionieren des Codes werfen.  
  
### <a name="to-debug-a-stored-procedure"></a>So debuggen Sie eine gespeicherte Prozedur  
  
1.  Öffnen Sie das zum Erstellen der DLL verwendete Projekt in Visual Studio.  
  
2.  Erstellen Sie Breakpoints in der Methode oder Funktion entsprechend der zu debuggenden Prozedur.  
  
3.  Verwenden Sie Visual Studio, um einen Debugbuild einer DLL für gespeicherte Prozeduren zu erstellen.  
  
4.  Stellen Sie die DLL auf dem Server bereit. Weitere Informationen zum Bereitstellen der DLL mit dem Server finden Sie unter [Erstellen gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md).  
  
5.  Sie benötigen eine Anwendung, um die zu testende gespeicherte Prozedur aufzurufen. Wenn Sie keine solche zur Verfügung haben, können Sie mit dem MDX-Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine MDX-Abfrage erstellen, um die zu testende gespeicherte Prozedur aufzurufen.  
  
6.  Hängen Sie in Visual Studio den Debugger an den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Prozess (Msmdsrv.exe) an.  
  
    1.  Aus der **Debuggen** Menü wählen **Anhängen ToProcess**.  
  
    2.  In der **Anhängen ToProcess** wählen Sie im Dialogfeld **Prozesse aller Benutzer anzeigen**.  
  
    3.  In der **verfügbare Prozesse** in die Liste der **Prozess** Spalte, klicken Sie auf **Msmdsrv.exe**. Werden auf dem Server mehrere Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ausgeführt, müssen Sie den Prozess mithilfe der ID der Instanz, die Sie verwenden wollen, identifizieren.  
  
    4.  In der **zuordnen** Text stellen Sie sicher, dass der entsprechende Programmtyp ausgewählt ist. Klicken Sie für eine CLR-DLL auf **wählen**, klicken Sie dann auf **diese Codetypen debuggen**, klicken Sie dann auf **verwaltet**, klicken Sie dann auf **OK**. Klicken Sie für eine COM-DLL auf **wählen**, klicken Sie dann auf **diese Codetypen debuggen**, klicken Sie dann auf **Native**, klicken Sie dann auf **OK**.  
  
    5.  Klicken Sie auf **Anfügen**.  
  
7.  Rufen Sie in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das Programm oder MDX-Skript zum Aufrufen der gespeicherten Prozedur auf. Der Debugger bricht um, wenn er eine Zeile mit einem Breakpoint erreicht. Sie können Variablen im Überwachungsfenster auswerten, Lokale anzeigen und den Code schrittweise durchlaufen.  
  
 Wenn Sie beim Debuggen einer Bibliothek Probleme haben, stellen Sie sicher, dass die entsprechende Programmdatenbankdatei (PDB-Datei) an den Bereitstellungsspeicherort auf dem Server kopiert wurde. Wurde diese Datei bei der Registrierung oder Bereitstellung nicht kopiert, müssen Sie sie manuell an denselben Speicherort wie die DLL kopieren. Bei systemeigenem Code (COM-DLL) ist die PDB-Datei im Unterverzeichnis \Debug gespeichert. Bei verwaltetem Code (CLR-DLL) ist sie im Unterverzeichnis \WINDEBUG gespeichert.  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionales Modell Assemblys-Verwaltung](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definieren von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

