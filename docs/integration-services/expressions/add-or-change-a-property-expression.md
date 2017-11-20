---
title: "Hinzufügen oder Ändern eines Eigenschaftsausdrucks | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e9f115f318366e743e0a933239b55ccda16b5171
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="add-or-change-a-property-expression"></a>Hinzufügen oder Ändern eines Eigenschaftsausdrucks
  Sie können Eigenschaftsausdrücke für Pakete, Tasks, Foreach-Schleifencontainer, For-Schleifencontainer, Sequenzcontainer, Ereignishandler, Verbindungs-Manager auf Paket- und Projektebene sowie für Protokollanbieter erstellen.  
  
 Um Eigenschaftsausdrücke zu erstellen oder zu ändern, können Sie entweder den **Eigenschaftsausdrucks-Editor** oder den **Ausdrucks-Generator**verwenden. Der **Eigenschaftsausdrucks-Editor** kann entweder über die benutzerdefinierten Editoren, die für Tasks und Container verfügbar sind, oder über das Fenster **Eigenschaften** aufgerufen werden. Auf den**Ausdrucks-Generator** kann über den **Eigenschaftsausdrucks-Editor**zugegriffen werden. Sie können zwar sowohl im **Eigenschaftsausdrucks-Editor** als auch im **Ausdrucks-Generator**Ausdrücke schreiben, der **Ausdrucks-Generator** bietet jedoch außerdem eine Reihe grafischer Tools, mit denen komplexe Ausdrücke problemlos erstellt werden können.  
  
 Weitere Informationen zu Syntax, Operatoren und Funktionen, die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bereitstellt, finden Sie unter [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md) und [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md). Das Thema für die einzelnen Operatoren oder Funktionen schließen Beispiele für das Verwenden des Operators bzw. der Funktion in einem Ausdruck ein. Beispiele für komplexere Ausdrücke finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
### <a name="to-create-or-change-a-property-expression"></a>So fügen Sie einen Eigenschaftsausdruck hinzu oder ändern ihn  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das Projekt mit dem gewünschten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen, und führen Sie dann eine der folgenden Aktionen aus:  
  
    -   Wenn es sich bei dem Element um einen Task oder einen Container handelt, doppelklicken Sie darauf, und klicken Sie dann im Editor auf **Ausdrücke** .  
  
    -   Klicken Sie mit der rechten Maustaste auf das Element, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie in das Feld **Ausdrücke** und dann auf die Auslassungspunkte (…).  
  
4.  Wählen Sie im **Eigenschaftsausdrucks-Editor**eine Eigenschaft in der Liste **Eigenschaft** aus, und gehen Sie dann wie folgt vor:  
  
    -   Geben Sie in die Spalte **Ausdruck** direkt einen Ausdruck ein oder ändern Sie ihn, und klicken Sie dann auf **OK**.  
  
         – oder –  
  
    -   Klicken Sie in der Ausdruckszeile der Eigenschaft auf die Auslassungspunkte (…), um den **Ausdrucks-Generator**zu öffnen.  
  
5.  (Optional) Führen Sie im **Ausdrucks-Generator**eine der folgenden Aufgaben aus:  
  
    -   Erweitern Sie die Option **Variablen**, um auf die System- und benutzerdefinierten Variablen zuzugreifen.  
  
    -   Erweitern Sie die Option [!INCLUDE[ssIS](../../includes/ssis-md.md)] Mathematische Funktionen **,**Zeichenfolgenfunktionen **,**Datums-/Uhrzeitfunktionen **,**NULL-Funktionen **,**Typumwandlungen **und**Operatoren **, um auf die Funktionen, die Umwandlungen und die Operatoren zuzugreifen, die von der**-Ausdruckssprache bereitgestellt werden.  
  
    -   Um einen Ausdruck im **Ausdrucks-Generator**zu erstellen oder zu ändern, ziehen Sie die Variablen, Spalten, Funktionen, Operatoren und Umwandlungen in das Feld **Ausdruck** oder geben den Ausdruck im Feld ein.  
  
    -   Klicken Sie im **Ausdrucks-Generator** auf **Ausdruck auswerten**, um das Auswertungsergebnis des Ausdrucks anzuzeigen.  
  
         Wenn der Ausdruck ungültig ist, wird eine Warnung angezeigt, in der die Syntaxfehler im Ausdruck beschrieben werden.  
  
        > [!NOTE]  
        >  Die Auswertung eines Ausdrucks weist der Eigenschaft das Auswertungsergebnis nicht zu.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Ausdrücke](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Integrationsservices &#40; SSIS &#41; Pakete](../../integration-services/integration-services-ssis-packages.md)   
 [Integration Services-Container](../../integration-services/control-flow/integration-services-containers.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integrationsservices &#40; SSIS &#41; Ereignishandler](../../integration-services/integration-services-ssis-event-handlers.md)   
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Integrationsservices &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

