---
title: "Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- items [Reporting Services], expressions
- data [Reporting Services], expressions
- expressions [Reporting Services], about expressions
- expressions [Reporting Services]
- SSRS, expressions
- formulas [Reporting Services]
- data manipulation [Reporting Services]
- SQL Server Reporting Services, expressions
ms.assetid: ae8a0166-2ccc-45f4-8d28-c150da7b73de
caps.latest.revision: 77
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc8491006425de79f8e96be1affb10687a1553f9
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs"></a>Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer (SSRS)
  Sie können in einem Bericht eingebettetem, benutzerdefiniertem Code oder benutzerdefinierten Assemblys, die Sie erstellen und auf dem Computer speichern und auf dem Berichtsserver bereitstellen. Verwenden Sie eingebetteten Code für benutzerdefinierte Konstanten, komplexe Funktionen oder für Funktionen, die mehrfach in demselben Bericht verwendet werden. Verwenden Sie benutzerdefinierte Codeassemblys, um Code an einer einzelnen Stelle zu verwalten und ihn zur Verwendung in mehreren Berichten freizugeben. In benutzerdefiniertem Code können neue benutzerdefinierte Konstanten, Variablen, Funktionen oder Unterroutinen eingeschlossen werden. Sie können schreibgeschützte Verweise in integrierte Auflistungen, wie die Parameter-Auflistung, einbeziehen. An benutzerdefinierte Funktionen können jedoch keine Sätze von Berichtsdatenwerten übergeben werden, insbesondere werden keine benutzerdefinierten Aggregate unterstützt.  
  
> [!IMPORTANT]  
>  Für zeitempfindliche Berechnungen, die einmal zur Laufzeit ausgewertet werden und während der Berichtsverarbeitung denselben Wert behalten sollen, bietet sich eventuell die Verwendung einer Berichts- oder Gruppenvariablen an. Weitere Informationen finden Sie unter [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md).  
  
 Berichts-Designer ist die bevorzugte Erstellungsumgebung für das Hinzufügen von benutzerdefiniertem Code zu einem Bericht. Berichts-Generator unterstützt das Verarbeiten von Berichten, die über gültige Ausdrücke verfügen, oder die Verweise auf benutzerdefinierte Assemblys auf einem Berichtsserver einschließen. Berichts-Generator bietet keine Möglichkeit, einen Verweis auf eine benutzerdefinierte Assembly hinzuzufügen.  
  
> [!NOTE]  
>  Während des Upgrades eines Berichtsservers erfordern Berichte, die von benutzerdefinierten Assemblys abhängig sind, unter Umständen weitere Schritte zum Abschließen des Upgrades.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RB3"></a> Arbeiten mit benutzerdefiniertem Code in Berichts-Generator  
 In Berichts-Generator können Sie einen Bericht von einem Berichtsserver öffnen, der Verweise auf benutzerdefinierte Assemblys einschließt. Sie können z. B. Berichte bearbeiten, die mit Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellt und bereitgestellt werden. Die benutzerdefinierten Assemblys müssen auf dem Berichtsserver bereitgestellt werden.  
  
 Sie können nicht die folgenden Schritte ausführen:  
  
1.  Hinzufügen von Verweisen oder Klassenmemberinstanzen zu einem Bericht.  
  
2.  Anzeigen eines Berichts in der Vorschau mit Verweisen auf benutzerdefinierte Assemblys im lokalen Modus.  
  
##  <a name="Common"></a> Einschließen von Verweisen auf häufig verwendete Funktionen  
 Verwenden Sie das Dialogfeld **Ausdruck** , um eine kategorisierte Liste allgemeiner, in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]integrierter Funktionen anzuzeigen. Wenn Sie **Allgemeine Funktionen** erweitern und auf eine Kategorie klicken, wird im Bereich **Element** die Liste der Funktionen angezeigt, die Sie in einen Ausdruck einschließen. Die gängigsten Funktionen umfassen Klassen aus der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Math> und <xref:System.Convert> Namespaces und [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Laufzeitbibliotheksfunktionen. Die gängigsten Funktionen sind im Dialogfeld **Ausdruck** nach Kategorie sortiert aufgeführt: Text, Datum und Uhrzeit, Mathematische Funktionen, Qualitätskontrolle, Programmfluss, Aggregat, Finanzen, Konvertierung und Sonstiges. Weniger häufig verwendete Funktionen werden nicht in der Liste angezeigt, können jedoch auch in einem Ausdruck verwendet werden.  
  
 Um eine integrierte Funktion zu verwenden, doppelklicken Sie auf den Funktionsnamen im Bereich Element. Im Bereich Beschreibung wird eine Beschreibung der Funktion angezeigt, und ein Beispiel des Funktionsaufrufs finden Sie im Bereich Beispiel. Wenn Sie im Codebereich den Funktionsnamen und anschließend eine linke Klammer **(**eingeben, zeigt die IntelliSense-Hilfe jede gültige Syntax für diesen Funktionsaufruf an. Zur Berechnung des Höchstwerts für ein Feld mit dem Namen `Quantity` in einer Tabelle fügen Sie dem Codebereich beispielsweise den einfachen Ausdruck `=Max(` hinzu und zeigen mithilfe der Smarttags alle gültigen Syntaxmöglichkeiten für den Funktionsaufruf an. Um dieses Beispiel zu vervollständigen, geben Sie `=Max(Fields!Quantity.Value)`ein.  
  
 Weitere Informationen über die einzelnen Funktionen finden Sie unter <xref:System.Math>, <xref:System.Convert>, und [Member der Visual Basic-Laufzeitbibliothek](http://go.microsoft.com/fwlink/?LinkId=198941) auf MSDN.  
  
##  <a name="NotCommon"></a> Einschließen von Verweisen auf weniger häufig verwendete Funktionen  
 Um einen Verweis auf andere, weniger häufig verwendete CLR-Namespaces einzuschließen, müssen Sie z. B. einen vollqualifizierten Verweis verwenden <xref:System.Text.StringBuilder>. IntelliSense wird für die seltener verwendeten Funktionen im Codebereich des Dialogfelds **Ausdruck** nicht unterstützt.  
  
 Weitere Informationen finden Sie unter [Member der Visual Basic-Laufzeitbibliothek](http://go.microsoft.com/fwlink/?LinkId=198941) bei MSDN.  
  
##  <a name="External"></a> Einschließen von Verweisen auf externe Assemblys  
 Sie müssen die Assembly identifizieren, damit der Berichtsprozessor einen Verweis auf eine Klasse in eine externe Assembly einschließt. Geben Sie den vollqualifizierten Namen der Assembly, die dem Bericht hinzugefügt werden soll, auf der Seite **Verweise** des Dialogfelds **Berichtseigenschaften** an. Im Ausdruck müssen Sie den vollqualifizierten Namen für die Klasse in der Assembly verwenden. Klassen in einer externen Assembly werden nicht im Dialogfeld **Ausdruck** angezeigt. Geben Sie für diese Klassen den entsprechenden Namen an. Ein vollqualifizierter Name umfasst den Namespace, den Klassennamen und den Elementnamen.  
  
##  <a name="Embedded"></a> Einschließen von eingebettetem Code  
 Auf der Registerkarte **Code** des Dialogfelds Berichtseigenschaften können Sie einem Bericht eingebetteten Code hinzufügen. Der erstellte Codeblock kann mehrere Methoden enthalten. Methoden in eingebettetem Code müssen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] geschrieben und instanzbasiert sein. Vom Berichtsprozessor werden automatisch Verweise für den System.Convert-Namespace und den System.Math-Namespace hinzugefügt. Fügen Sie zusätzliche Assemblyverweise auf der Seite **Verweise** des Dialogfelds **Berichtseigenschaften** hinzu. Weitere Informationen finden Sie unter [Hinzufügen eines Assemblyverweises zu einem Bericht &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Die Methoden im eingebetteten Code stehen über ein global definiertes **Code** -Element zur Verfügung. Zum Zugriff auf die Methoden verweisen Sie auf das **Code** -Element und den Methodennamen. Im folgenden Beispiel wird die Methode **ToUSD**aufgerufen, die den Wert des `StandardCost` -Felds in einen Dollarwert konvertiert:  
  
```  
=Code.ToUSD(Fields!StandardCost.Value)  
```  
  
 Um in Ihrem benutzerdefinierten Code auf integrierte Sammlungen verweisen zu können, müssen Sie einen Verweis auf das integrierte **Berichts** -Objekt hinzufügen:  
  
```  
=Report.Parameters!Param1.Value  
```  
  
 In den folgenden Beispielen wird veranschaulicht, wie einige benutzerdefinierte Konstanten und Variablen definiert werden können.  
  
```  
Public Const MyNote = "Authored by Bob"  
Public Const NCopies As Int32 = 2  
Public Dim  MyVersion As String = "123.456"  
Public Dim MyDoubleVersion As Double = 123.456  
```  
  
 Obwohl benutzerdefinierte Konstanten nicht in der **Konstanten** -Kategorie des Dialogfelds **Ausdruck** angezeigt werden (in der nur integrierte Konstanten angezeigt werden), können Sie Verweise darauf über einen beliebigen Ausdruck hinzufügen (wie in den folgenden Beispielen veranschaulicht). In einem Ausdruck wird eine benutzerdefinierte Konstante als **Variant**behandelt.  
  
```  
=Code.MyNote  
=Code.NCopies  
=Code.MyVersion  
=Code.MyDoubleVersion  
```  
  
 In den folgenden Beispielen sind sowohl der Codeverweis als auch die Codeimplementierung der Funktion **FixSpelling**enthalten, mit der der Text `"Bicycle"` für alle Vorkommen des Texts „Bike“ im `SubCategory` -Feld ersetzt wird.  
  
 `=Code.FixSpelling(Fields!SubCategory.Value)`  
  
 Mit dem folgenden Code wird eine Implementierung der **FixSpelling** -Methode veranschaulicht, wenn er in den Codeblock einer Berichtsdefinition eingebettet ist. In diesem Beispiel wird gezeigt, wie ein vollqualifizierter Verweis auf die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **StringBuilder** -Klasse angewandt wird.  
  
```vb  
Public Function FixSpelling(ByVal s As String) As String  
   Dim strBuilder As New System.Text.StringBuilder(s)  
   If s.Contains("Bike") Then  
      strBuilder.Replace("Bike", "Bicycle")  
      Return strBuilder.ToString()  
      Else : Return s  
   End If  
End Function  
```  
  
 Weitere Informationen zu integrierten Objektsammlungen und die Initialisierung finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md) und [Initialisieren von Objekten benutzerdefinierter Assemblys](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md).  
  
##  <a name="Parameters"></a> Einschließen von Verweisen auf Parameter von Code  
 Sie können auf die globale Parameters-Auflistung per benutzerdefinierten Code über einen Codeblock der Berichtsdefinition oder über eine von Ihnen bereitgestellte benutzerdefinierte Assembly verweisen. Die Parameters-Auflistung ist schreibgeschützt und verfügt über keine öffentlichen Iteratoren. Es ist nicht möglich, eine [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **für jedes** Konstrukt zu verwenden, um die Auflistung zu durchlaufen. Sie benötigen den in der Berichtsdefinition definierten Namen des Parameters, um in Ihrem Code auf ihn verweisen zu können. Allerdings ist es möglich, alle Werte eines mehrwertigen Parameters zu durchlaufen.  
  
 Die folgende Tabelle enthält Beispiele für Verweise auf die integrierte `Parameters` -Sammlung von benutzerdefiniertem Code:  
  
 **Übergeben einer vollständigen globalen Parameters-Sammlung an benutzerdefinierten Code.**Diese Funktion gibt den Wert eines bestimmten Berichtsparameters *MyParameter*zurück.  
  
 Verweis in Ausdruck `=Code.DisplayAParameterValue(Parameters)`  
  
 Benutzerdefinierte Codedefinition  
  
```  
Public Function DisplayAParameterValue(ByVal parameters as Parameters) as Object  
Return parameters("MyParameter").Value  
End Function  
```  
  
 **Übergeben eines einzelnen Parameters an benutzerdefinierten Code.**  
  
 Verweis in Ausdruck `=Code.ShowParametersValues(Parameters!DayOfTheWeek)`  
  
 In diesem Beispiel wird der Wert des übergebenen Parameters zurückgegeben. Entspricht der Parameter einem mehrwertigen Parameter, ist die Rückgabezeichenfolge eine Verkettung aller Werte.  
  
 Benutzerdefinierte Codedefinition  
  
```  
Public Function ShowParameterValues(ByVal parameter as Parameter)  
 as String  
   Dim s as String   
   If parameter.IsMultiValue then  
      s = "Multivalue: "   
      For i as integer = 0 to parameter.Count-1  
         s = s + CStr(parameter.Value(i)) + " "   
      Next  
   Else  
      s = "Single value: " + CStr(parameter.Value)  
   End If  
   Return s  
End Function  
```  
  
##  <a name="Custom"></a> Einschließen von Verweisen auf Code von benutzerdefinierten Assemblys  
 Wenn Sie in einem Bericht benutzerdefinierte Assemblys verwenden möchten, müssen Sie zunächst die Assembly erstellen und für den Berichts-Designer zur Verfügung stellen. Anschließend fügen Sie im Bericht einen Verweis auf die Assembly hinzu und verwenden dann im Bericht einen Ausdruck, der auf die Methoden in dieser Assembly verweist. Beim Bereitstellen des Berichts auf dem Berichtsserver müssen Sie dort auch die benutzerdefinierte Assembly bereitstellen.  
  
 Informationen zum Erstellen einer benutzerdefinierten Assembly und zu ihrer Verwendung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]finden Sie unter [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md).  
  
 Wenn Sie in einem Ausdruck auf benutzerdefinierten Code verweisen möchten, müssen Sie das Klassenelement in der Assembly aufrufen. Die Vorgehensweise hängt davon ab, ob es sich um eine statische oder um eine instanzbasierte Methode handelt. Statische Methoden in einer benutzerdefinierten Assembly stehen global im Bericht zur Verfügung. Auf statische Methoden können Sie in Ausdrücken durch Angeben des Namespace, der Klasse und des Methodennamens zugreifen. Im folgenden Beispiel wird die **ToGBP**-Methode aufgerufen, die den Wert des **StandardCost** -Felds von Dollar in Pfund Sterling konvertiert:  
  
```  
=CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
```  
  
 Instanzbasierte Methoden sind über ein global definiertes **Code** -Element verfügbar. Zum Zugriff auf die Methoden verweisen Sie auf das **Code** -Element und anschließend auf die Instanz und den Methodennamen. Im folgenden Beispiel wird die **ToEUR**-Instanzmethode aufgerufen, die den Wert des **StandardCost** -Felds von Dollar in Euro konvertiert:  
  
```  
=Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
```  
  
> [!NOTE]  
>  Im Berichts-Designer wird eine benutzerdefinierte Assembly einmal geladen und erst beim Schließen von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]entladen. Wenn Sie einen Bericht in der Vorschau anzeigen, dann Änderungen an einer im Bericht verwendeten benutzerdefinierten Assembly vornehmen und anschließend die Vorschau des Berichts erneut anzeigen, werden diese Änderungen in der zweiten Vorschau nicht angezeigt. Zum erneuten Laden der Assembly müssen Sie [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] schließen und neu öffnen und dann die Vorschau des Berichts anzeigen.  
  
 Weitere Informationen zum Zugreifen auf Ihren Code finden Sie unter [Accessing Custom Assemblies Through Expressions](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
##  <a name="collections"></a> Übergeben von integrierten Auflistungen in benutzerdefinierte Assemblys  
 Um integrierte Sammlungen wie die *Globals* - oder *Parameters* -Sammlung zur Verarbeitung an eine benutzerdefinierte Assembly zu übergeben, fügen Sie einen Assemblyverweis im Codeprojekt der Assembly hinzu, die die integrierten Auflistungen definiert, und greifen Sie auf den korrekten Namespace zu. Abhängig davon, ob Sie die benutzerdefinierte Assembly für einen auf einem Berichtsserver ausgeführten Bericht (Serverbericht) oder einen in einer .NET-Anwendung lokal ausgeführten Bericht (lokaler Bericht) entwickeln, unterscheidet sich jeweils die zu referenzierende Assembly. Weitere Details siehe unten.  
  
-   **Namespace** : Microsoft.ReportingServices.ReportProcessing.ReportObjectModel  
  
-   **Assembly (lokaler Bericht):** Microsoft.ReportingServices.ProcessingObjectModel.dll  
  
-   **Assembly (Serverbericht):** Microsoft.ReportViewer.ProcessingObjectModel.dll  
  
 Da sich der Inhalt der *Fields* - und *ReportItems* -Sammlung zur Laufzeit dynamisch ändern kann, sollten Sie über die Aufrufe in der benutzerdefinierten Assembly hinaus nicht daran festhalten (z.B. in einer Elementvariablen). Die gleiche Empfehlung gilt im Allgemeinen für alle integrierten Auflistungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen von Code zu einem Bericht &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)   
 [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Hinzufügen eines Assemblyverweises zu einem Bericht &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md)   
 [Reporting Services-Tutorials &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Berichtsbeispiele (Berichts-Generator und SSRS)](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
  
