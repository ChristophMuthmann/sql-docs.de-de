---
title: Grundlegendes zu synchronen und asynchronen Transformationen | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9cc38505042dadb1b057a737279be82bb7923432
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>Grundlegendes zu synchronen und asynchronen Transformationen
  Den Unterschied zwischen einer synchronen und asynchronen Transformation in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] versteht man am besten, wenn man die Grundzüge einer synchronen Transformation kennt. Wenn eine synchrone Transformation Ihre Anforderungen nicht erfüllt, könnte Ihr Design eine asynchrone Transformation erfordern.  
  
## <a name="synchronous-transformations"></a>Synchrone Transformationen  
 Bei einer synchronen Transformation werden eingehende Zeilen verarbeitet und zeilenweise in den Datenfluss übergeben. Die Ausgabe ist mit der Eingabe synchron, erfolgt demnach gleichzeitig. Deshalb werden bei der Transformation zur Verarbeitung einer bestimmten Zeile keine Informationen über andere Zeilen im Dataset benötigt. In der eigentlichen Bereitstellung werden Zeilen bei der Weitergabe von einer Komponente zur nächsten in Puffern gruppiert, die jedoch für den Benutzer transparent sind; man kann davon ausgehen, dass jede Zeile separat verarbeitet wird.  
  
 Ein Beispiel für eine synchrone Transformation ist die Transformation für Datenkonvertierung. Für jede eingehende Zeile wird der Wert in der angegebenen Spalte konvertiert und dann die Zeile weitergesendet. Jeder einzelne Konvertierungsvorgang ist von allen anderen Zeilen im Dataset unabhängig.  
  
 In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Skripterstellung und Programmierung, geben Sie eine synchrone Transformation durch die ID der Eingabe einer Komponente suchen und Zuweisen der **SynchronousInputID** -Eigenschaft der Ausgaben der Komponente. Dadurch wird das Datenflussmodul angewiesen, jede Zeile aus der Eingabe zu verarbeiten und jede Zeile automatisch an angegebene Ausgaben zu senden. Wenn Sie möchten, dass jede Zeile an jede Ausgabe gesendet wird, brauchen Sie keinen zusätzlichen Code für die Ausgabe der Daten zu schreiben. Bei Verwendung von der **ExclusionGroup** Eigenschaft, um anzugeben, dass Zeilen nur an einer Gruppe von Ausgaben, sollten wie in der Transformation für bedingtes Teilen, die Sie aufrufen müssen die **DirectRow** Methode auswählen das entsprechende Ziel für jede Zeile. Wenn Sie eine Fehlerausgabe haben, müssen Sie aufrufen **DirectErrorRow** Zeilen mit Problemen an die Fehlerausgabe anstelle der standardmäßigen Ausgabe zu senden.  
  
## <a name="asynchronous-transformations"></a>Asynchrone Transformationen  
 Möglicherweise erfordert Ihr Design eine asynchrone Transformation, wenn die Verarbeitung der einzelnen Zeilen unabhängig von allen anderen Zeilen nicht möglich ist. Anders ausgedrückt, können Sie nicht jede Zeile bei der Verarbeitung an den Datenfluss weitergeben, sondern müssen Daten asynchron bzw. zu einer anderen Zeit als die Eingabe ausgeben. Zum Beispiel erfordern die folgenden Szenarios eine asynchrone Transformation:  
  
-   Die Komponente muss mehrere Datenpuffer abrufen, bevor die Verarbeitung ausgeführt werden kann. Ein Beispiel ist die Transformation zum Sortieren, bei der die Komponente den vollständigen Satz an Zeilen in einem Vorgang verarbeiten muss.  
  
-   Die Komponente muss Zeilen mehrerer Eingaben kombinieren. Ein Beispiel ist die Transformation für Zusammenführen, bei der die Komponente mehrere Zeilen jeder Eingabe überprüfen und sie anschließend in sortierter Reihenfolge zusammenführen muss.  
  
-   Es gibt keine 1:1-Entsprechung zwischen Eingabezeilen und Ausgabezeilen. Ein Beispiel ist die Transformation für das Aggregieren, bei der die Komponente eine Zeile zur Ausgabe hinzufügen muss, um die berechneten Aggregatwerte aufzunehmen.  
  
 In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Skripterstellung und Programmierung, geben Sie eine asynchrone Transformation durch Zuweisen eines Werts von 0 bis der **SynchronousInputID** -Eigenschaft der Ausgaben der Komponente. zugreifen. Dadurch wird das Datenflussmodul angewiesen, nicht jede Zeile automatisch an die Ausgaben zu senden. Anschließend müssen Sie den Code schreiben, um jede Zeile explizit an die jeweilige Ausgabe zu senden, indem sie dem neuen Ausgabepuffer hinzugefügt wird, der für die Ausgabe einer asynchronen Transformation erstellt wird.  
  
> [!NOTE]  
>  Da eine Quellkomponente auch jede Zeile, die aus der Datenquelle gelesen wird, explizit ihren Ausgabepuffern hinzufügen muss, ähnelt eine Quelle einer Transformation mit asynchronen Ausgaben.  
  
 Es wäre auch mögliche, eine asynchrone Transformation zu erstellen, die eine synchrone Transformation emuliert, indem man jede Eingabezeile explizit in die Ausgabe kopiert. Mit diesem Ansatz könnten Sie Spalten umbenennen oder Datentypen oder -formate konvertieren. Dieser Ansatz beeinträchtigt jedoch die Leistung. Sie können die gleichen Ergebnisse bei besserer Leistung erreichen, indem Sie eingebaute Integration Services-Komponenten verwenden, wie zum Beispiel Kopieren von Spalten oder Datenkonvertierung.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer synchronen Transformation mit der Skriptkomponente](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Erstellen einer asynchronen Transformation mit der Skriptkomponente](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [Entwickeln einer benutzerdefinierten Transformationskomponente mit synchronen Ausgaben](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [Entwickeln einer benutzerdefinierten Transformationskomponente mit asynchronen Ausgaben](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  

