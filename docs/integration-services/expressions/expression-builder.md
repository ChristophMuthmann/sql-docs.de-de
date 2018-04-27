---
title: Ausdrucks-Generator | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be743102bdebe8d30b612f58df606f7d20412f00
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="expression-builder"></a>Ausdrucks-Generator
  Verwenden Sie das Dialogfeld **Ausdrucks-Generator** , um mithilfe einer grafischen Benutzeroberfläche einen Eigenschaftsausdruck zu erstellen und zu bearbeiten oder den Ausdruck zu schreiben, der den Wert einer Variablen festlegt. Diese grafische Benutzeroberfläche bietet Listen von Variablen sowie integrierte Verweise auf Funktionen, Typumwandlungen und Operatoren der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Ausdruckssprache.  
  
 Ein Eigenschaftsausdruck ist ein einer Eigenschaft zugewiesener Ausdruck. Wenn der Ausdruck ausgewertet wird, wird die Eigenschaft dynamisch aktualisiert, damit das Auswertungsergebnis des Ausdrucks verwendet wird. Genauso ermöglicht ein Ausdruck, der in einer Variablen verwendet wird, das Update des Variablenwerts mit dem Auswertungsergebnis des Ausdrucks.  
  
 Es gibt mehrere Verwendungsmöglichkeiten für Ausdrücke:  
  
-   **Tasks** Aktualisieren Sie die „An“-Zeile, die ein Task des Typs „Mail“ senden verwendet, indem eine in einer Variablen gespeicherte E-Mail-Adresse eingefügt wird, oder aktualisieren Sie die Betreffzeile, indem Sie eine Zeichenfolge, wie z.B. "Sales for:", und das aktuelle Datum verketten, das von der GETDATE-Funktion zurückgegeben wird.  
  
-   **Variablen** Legen Sie den Wert einer Variablen auf den aktuellen Monat fest, indem Sie einen Ausdruck wie `DATEPART("mm",GETDATE())`verwenden. Oder legen Sie den Wert einer Zeichenfolge fest, indem Sie das Zeichenfolgenliteral und das aktuelle Datum mithilfe des Ausdrucks `"Today's date is " + (DT_WSTR,30)(GETDATE())`verketten.  
  
-   **Verbindungs-Manager** Legen Sie die Codepage eines Flatfile-Verbindungs-Managers fest, indem Sie eine Variable verwenden, die einen anderen Codepagebezeichner enthält, oder geben Sie die Anzahl der auszulassenden Zeilen in der Datendatei an, indem Sie eine positive ganze Zahl, z. B. 3, in dem Ausdruck eingeben.  
  
 Weitere Informationen zu Eigenschaftenausdrücken und zum Schreiben von Ausdrücken finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md) und [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="options"></a>Tastatur  
  
|Begriff|Definition|  
|----------|----------------|  
|**Variablen**|Erweitern Sie den Ordner **Variablen** , und ziehen Sie die gewünschten Variablen in das Feld **Ausdruck** .|  
|**Mathematische Funktionen**<br /><br /> **Zeichenfolgenfunktionen**<br /><br /> **Datum/Uhrzeit-Funktionen**<br /><br /> **NULL-Funktionen**<br /><br /> **Typumwandlungen**<br /><br /> **Operatoren**|Erweitern Sie die entsprechenden Ordner, und ziehen Sie die gewünschten Funktionen, Typumwandlungen und Operatoren in das Feld **Ausdruck** .|  
|**Ausdruck**|Geben Sie einen Ausdruck ein, oder bearbeiten Sie einen Ausdruck.|  
|**Ausgewerteter Wert**|Listet das Ergebnis der Ausdrucksauswertung auf.|  
|**Ausdruck auswerten**|Klicken Sie auf **Ausdruck auswerten** , um das Auswertungsergebnis des Ausdrucks anzuzeigen.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Eigenschaftsausdrucks-Editor](../../integration-services/expressions/property-expressions-editor.md)   
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Systemvariablen](../../integration-services/system-variables.md)  
  
  
