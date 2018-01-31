---
title: Bezeichner (SSIS) | Microsoft-Dokumentation
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
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e012e6c3c6b20c2a7f07b29c85b94dc127019d37
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="identifiers-ssis"></a>Bezeichner (SSIS)
  In Ausdrücken sind Bezeichner Spalten und Variablen, die für den Vorgang verfügbar sind. Reguläre und qualifizierte Bezeichner können in Ausdrücken verwendet werden.  
  
## <a name="regular-identifiers"></a>Reguläre Bezeichner  
 Ein regulärer Bezeichner erfordert keine zusätzlichen Qualifizierer. Beispielsweise ist **MiddleName**ein regulärer Bezeichner. Dabei handelt es sich um eine Spalte in der **Contacts** -Tabelle der **AdventureWorks** -Datenbank.  
  
 Die Namen von regulären Bezeichnern müssen den folgenden Regeln entsprechen:  
  
-   Das erste Zeichen des Namens muss ein Buchstabe gemäß Unicode-Standard 2.0 sein oder ein Unterstrich (_).  
  
-   Nachfolgende Zeichen können Buchstaben oder Zahlen gemäß Unicode-Standard 2.0, ein Unterstrich (_) oder die Zeichen @, $ und # sein.  
  
> [!IMPORTANT]  
>  Nur die aufgeführten eingebetteten Zeichen und Sonderzeichen sind in regulären Bezeichnern gültig. Für die Verwendung von Leerzeichen und Sonderzeichen müssen Sie anstelle eines regulären Bezeichners einen qualifizierten Bezeichner verwenden.  
  
## <a name="qualified-identifiers"></a>Qualifizierte Bezeichner  
 Ein qualifizierter Bezeichner wird durch eckige Klammern getrennt. Für einen Bezeichner kann ein Trennzeichen erforderlich sein, weil der Name des Bezeichners Leerzeichen einschließt oder weil das erste Zeichen des Bezeichnernamens kein Buchstabe oder ein Unterstrich ist. Beispielsweise muss der Spaltenname **Middle Name** mit eckigen Klammern qualifiziert und in einem Ausdruck als „[Middle Name]“ eingegeben werden.  
  
 Wenn der Name des Bezeichners Leerzeichen einschließt oder wenn der Name kein gültiger Name für einen regulären Bezeichner ist, muss der Bezeichner qualifiziert werden. Die Ausdrucksauswertung verwendet öffnende und schließende eckige Klammern ([]), um Bezeichner zu qualifizieren. Die eckigen Klammern befinden sich an der ersten und letzten Position der Zeichenfolge. Beispielsweise wird der Bezeichner 5$> zu [5$>]. Eckige Klammern können für Spaltennamen, Variablennamen und Funktionsnamen verwendet werden.  
  
 Falls Sie Ausdrücke mithilfe der Dialogfelder des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers erstellen, werden reguläre Bezeichner automatisch in eckige Klammern eingeschlossen. Eckige Klammern sind jedoch nur erforderlich, wenn der Name ungültige Zeichen enthält. Beispielsweise ist die Spalte mit dem Namen **MiddleName** auch ohne eckige Klammern gültig.  
  
 In Ausdrücken kann nicht auf Spaltennamen verwiesen werden, die eckige Klammern einschließen. Beispielsweise kann der Spaltenname **Column[1]** nicht in einem Ausdruck verwendet werden. Der Spaltenname müsste ansonsten in einen Ausdruck ohne eckige Klammern umbenannt werden.  
  
## <a name="lineage-identifiers"></a>Herkunftsbezeichner  
 In Ausdrücken kann mit Herkunftsbezeichnern auf Spalten verwiesen werden. Die Herkunftsbezeichner werden automatisch zugewiesen, wenn Sie das Paket erstellen. Den Herkunftsbezeichner für eine Spalte können Sie im **-Designer im Dialogfeld** Erweiterter Editor **auf der Registerkarte** Spalteneigenschaften [!INCLUDE[ssIS](../../includes/ssis-md.md)] anzeigen.  
  
 Wenn Sie mithilfe des Herkunftsbezeichners auf eine Spalte verweisen, muss der Bezeichner das Nummernzeichenpräfix (#) einschließen. Beispielsweise muss eine Spalte mit dem Herkunftsbezeichner 147 als #147 dargestellt werden.  
  
 Falls ein Ausdruck erfolgreich analysiert wird, ersetzt die Ausdrucksauswertung den Herkunftsbezeichner durch Spaltennamen im Dialogfeld.  
  
## <a name="unique-column-names"></a>Eindeutige Spaltennamen  
 Mehrere in einem Paket verwendete Komponenten können Spalten mit demselben Namen verfügbar machen. Falls diese Spalten in Ausdrücken verwendet werden, muss sichergestellt werden, dass sie nicht mehrdeutig sind, damit die Ausdrücke erfolgreich analysiert werden können. Die Ausdrucksauswertung unterstützt die punktierte Schreibweise zum Identifizieren der Spaltenquelle. Beispielsweise werden zwei Spalten mit dem Namen **Age** zu **FlatFileSource.Age** und **OLEDBSource.Age**. Daran ist erkennbar, dass FlatFileSource und OLEDBSource die Quellen sind. Der Parser behandelt den vollqualifizierten Namen als einen einzelnen Spaltennamen.  
  
 Die Namen von Spaltenkomponenten und Spalten werden separat qualifiziert. Die folgenden Beispiele veranschaulichen die gültige Verwendung von eckigen Klammern in einer gepunkteten Schreibweise:  
  
-   Der Name der Quellkomponente schließt Leerzeichen ein.  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   Das erste Zeichen im Spaltennamen ist ungültig.  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   Die Namen der Quellkomponente und der Spalte enthalten ungültige Zeichen.  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  Falls beide Elemente in gepunkteter Schreibweise in eckige Klammern eingeschlossen sind, interpretiert die Ausdrucksauswertung das Klammernpaar als einen einzelnen Bezeichner, und nicht als eine Kombination aus Quelle und Spalte.  
  
## <a name="variables-in-expressions"></a>Variablen in Ausdrücken  
 Wenn in Ausdrücken auf Variablen verwiesen wird, muss das @-Präfix verwendet werden. Beispielsweise wird auf die **Counter**-Variable mit @Counter verwiesen. Das @-Zeichen ist nicht Bestandteil des Variablennamens, sondern identifiziert die Variable nur gegenüber der Ausdrucksauswertung. Wenn Sie Ausdrücke mithilfe der Dialogfelder des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers erstellen, wird dem Variablennamen automatisch das @-Zeichen hinzugefügt. Leerzeichen sind zwischen dem @-Zeichen und dem Variablennamen nicht zulässig.  
  
 Für Variablennamen gelten dieselben Regeln wie für andere reguläre Bezeichner:  
  
-   Das erste Zeichen des Namens muss ein Buchstabe gemäß Unicode-Standard 2.0 sein oder ein Unterstrich (_).  
  
-   Nachfolgende Zeichen können Buchstaben oder Zahlen gemäß Unicode-Standard 2.0, ein Unterstrich (_) oder die Zeichen @, $ und # sein.  
  
 Enthält ein Variablenname andere als die aufgeführten Zeichen, muss die Variable in eckige Klammern eingeschlossen werden. Beispielsweise müssen Variablennamen mit Leerzeichen in eckige Klammern eingeschlossen werden. Die öffnende eckige Klammer folgt auf das @-Zeichen. Beispielsweise wird auf die **My Name** -Variable mit „@[My Name]“ verwiesen. Leerzeichen sind zwischen dem Variablennamen und den eckigen Klammern nicht zulässig.  
  
> [!NOTE]  
>  Die Namen von benutzerdefinierten und Systemvariablen unterscheiden nach Groß-/Kleinschreibung.  
  
## <a name="unique-variable-names"></a>Eindeutige Variablennamen  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt benutzerdefinierte Variablen und stellt eine Reihe von Systemvariablen bereit. Standardmäßig gehören benutzerdefinierte Variablen zum Namespace **User** und Systemvariablen zum Namespace **System** . Sie können zusätzliche Namespaces für benutzerdefinierte Variablen erstellen und die Namespacenamen entsprechend den Anforderungen Ihrer Anwendung aktualisieren. Im Ausdrucks-Generator werden bereichsinterne Variablen in allen Namespaces aufgeführt.  
  
 Alle Variablen weisen einen Bereich auf und gehören zu einem Namespace. Eine Variable weist einen Paketbereich oder den Bereich eines Containers oder Tasks im Paket auf. Im Ausdrucks-Generator des [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designers werden nur die bereichsinternen Variablen aufgeführt. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
 Für Variablen, die in Ausdrücken verwendet werden, sind eindeutige Namen erforderlich, damit die Ausdrucksauswertung den Ausdruck ordnungsgemäß auswertet. Falls ein Paket mehrere gleichnamige Variablen verwendet, müssen deren Namespaces unterschiedlich sein. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt einen Namespace-Auflösungsoperator bereit, bestehend aus zwei Doppelpunkten (::), um eine Variable mit ihrem Namespace zu qualifizieren. Beispielsweise verwenden die folgenden Ausdrücke zwei Variablen mit dem Namen **Count**. Eine Variable gehört zum Namespace **User** und die andere zum Namespace **MyNamespace** .  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  Sie müssen die Kombination aus Namespace und qualifiziertem Variablennamen in eckige Klammern einschließen, damit die Ausdrucksauswertung die Variable erkennt.  
  
 Falls der Wert von **Count** im Namespace **User** 10 und der Wert von **Count** in **MyNamespace** 2 ist, wird der Ausdruck zu **TRUE** ausgewertet, weil die Ausdrucksauswertung zwei unterschiedliche Variablen erkennt.  
  
 Wenn Variablennamen nicht eindeutig sind, wird kein Fehler gemeldet. Die Ausdrucksauswertung verwendet stattdessen nur eine Instanz der Variablen zum Auswerten des Ausdrucks und gibt ein falsches Ergebnis zurück. Beispielsweise war der folgende Ausdruck für den Vergleich der Werte (10 und 2) zweier separater **Count** -Variablen vorgesehen. Der Ausdruck wird jedoch zu **FALSE** ausgewertet, da die Ausdrucksauswertung dieselbe Instanz der **Count** -Variablen zweimal verwendet.  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Technischer Artikel, [SSIS Expression Cheat Sheet](http://go.microsoft.com/fwlink/?LinkId=746575), auf pragmaticworks.com  
  
  
