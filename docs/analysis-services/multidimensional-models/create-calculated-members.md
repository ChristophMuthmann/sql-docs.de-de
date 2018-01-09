---
title: Erstellen von berechneten Elementen | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculated members [Analysis Services]
- custom measures [Analysis Services]
- members [Analysis Services], calculated
- calculations [Analysis Services], calculated members
ms.assetid: 820e4b18-9c3a-4b12-a126-ca16d8364a00
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 92d18934426772d34d4b63e087d235fe6c48dfe3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="create-calculated-members"></a>Erstellen von berechneten Elementen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können benutzerdefinierte Measures oder Dimensionselemente, so genannte berechnete Elemente durch Kombinieren von Cubedaten, arithmetischen Operatoren, Zahlen und Funktionen erstellen. Sie können z. B. ein berechnetes Element mit dem Namen Euros erstellen, das Dollar in Euro konvertiert, indem ein vorhandenes Dollar-Measure mit einem Umrechnungskurs multipliziert wird. Euros kann Endbenutzern dann in einer eigenen Zeile oder Spalte angezeigt werden.  
  
 Definitionen berechneter Elemente werden zwar gespeichert, ihre Werte sind jedoch nur im Arbeitsspeicher vorhanden. Im vorherigen Beispiel werden die Werte für Euros für Endbenutzer angezeigt, aber nicht als Cubedaten gespeichert.  
  
 Sie können berechnete Elemente in Cubes erstellen. Um ein berechnetes Element zu erstellen, klicken Sie im Cube-Designer auf der Registerkarte **Berechnungen** auf der Symbolleiste auf das Symbol **Neues berechnetes Element** . Mit diesem Befehl wird ein Formular zum Angeben der folgenden Optionen für das berechnete Element angezeigt:  
  
 **Name**  
 Wählen Sie den Namen des berechneten Elements aus. Dieser Name wird als Spalten- oder Zeilenüberschrift für die berechneten Elementwerte angezeigt, wenn Endbenutzer den Cube durchsuchen.  
  
 **Übergeordnete Hierarchie**  
 Wählen Sie die übergeordnete Hierarchie aus, die in das berechnete Element aufgenommen werden soll. Hierarchien sind beschreibende Kategorien einer Dimension, über die die numerischen Daten (Measures) in einem Cube für die Analyse getrennt werden können. In tabellarischen Browsern stellen Hierarchien die Spalten- und Zeilenüberschriften bereit, die Endbenutzern angezeigt werden, wenn sie die Daten in einem Cube anzeigen. (In grafischen Browsern stellen sie andere Arten von beschreibenden Bezeichnungen bereit, erfüllen jedoch dieselbe Funktion wie in tabellarischen Browsern.) Ein berechnetes Element stellt eine neue Überschrift (oder Bezeichnung) in der von Ihnen ausgewählten übergeordneten Dimension bereit.  
  
 Alternativ dazu können Sie das berechnete Element in die Measures statt in eine Dimension aufnehmen. Diese Option stellt auch eine neue Spalten- oder Zeilenüberschrift bereit, wird jedoch im Browser an Measures angefügt.  
  
 **Übergeordnetes Element**  
 Klicken Sie auf **Ändern** , um ein übergeordnetes Element auszuwählen, das das berechnete Element enthalten soll. Diese Option ist nicht verfügbar, wenn Sie eine Hierarchie mit einer einzelnen Ebene oder MEASURES als übergeordnete Dimension auswählen.  
  
 Hierarchien werden in Ebenen unterteilt, die Elemente enthalten. Jedes Element erzeugt eine Überschrift. Während des Anzeigens der Daten in einem Cube können Endbenutzer einen Drilldown von einer ausgewählten Überschrift zu zuvor nicht angezeigten untergeordneten Überschriften ausführen. Die Überschrift für das berechnete Element wird zu der Ebene hinzugefügt, die sich direkt unter dem von Ihnen ausgewählten übergeordneten Element befindet.  
  
 **Ausdruck**  
 Geben Sie den Ausdruck an, der die Werte des berechneten Elements erzeugt. Dieser Ausdruck kann in MDX (Multidimensional Expressions) geschrieben sein. Der Ausdruck kann Folgendes enthalten:  
  
-   Datenausdrücke, die für die Komponenten des Cubes stehen, wie Dimensionen, Ebenen, Measures usw.  
  
-   Arithmetische Operatoren  
  
-   Zahlen  
  
-   Funktionen  
  
 Sie können Cubekomponenten aus der Registerkarte **Metadaten** im Bereich **Berechnungstools** ziehen oder kopieren, um sie schnell zu einem Ausdruck hinzuzufügen.  
  
> [!IMPORTANT]  
>  Ein berechnetes Element, das im Wertausdruck eines anderen berechneten Elements verwendet wird, muss vor dem berechneten Element erstellt werden, in dem es verwendet wird.  
  
 Formatzeichenfolge  
 Gibt das Format der Zellenwerte an, die auf dem berechneten Element basieren. Die Eigenschaft nimmt dieselben Werte an wie die **Display Format** -Eigenschaft für Measures. Weitere Informationen zu Anzeigeformaten finden Sie unter [Konfigurieren von Measureeigenschaften](../../analysis-services/multidimensional-models/configure-measure-properties.md).  
  
 Sichtbar  
 Bestimmt, ob das berechnete Element beim Abrufen von Cubemetadaten sichtbar oder ausgeblendet ist. Wenn das berechnete Element ausgeblendet ist, kann es trotzdem in MDX-Ausdrücken, -Anweisungen und -Skripts verwendet werden, aber es wird nicht als auswählbares Objekt in Clientbenutzeroberflächen angezeigt.  
  
 Verhalten für nicht leere Elemente  
 Speichert die Namen von Measures, die zum Auflösen von NON EMPTY-Abfragen in MDX verwendet werden. Wenn diese Eigenschaft leer ist, muss das berechnete Element wiederholt ausgewertet werden, um zu ermitteln, ob ein Element leer ist. Wenn diese Eigenschaft den Namen eines oder mehrerer Measures enthält, wird das berechnete Element als leeres Element behandelt, wenn alle angegebenen Measures leer sind. Diese Eigenschaft ist ein Optimierungshinweis für Analysis Services, dass nur Datensätze ungleich NULL zurückgegeben werden sollen. Wenn nur Datensätze ungleich NULL zurückgegeben werden, wird die Leistung von MDX-Abfragen verbessert, für die der Operator NON EMPTY oder die NonEmpty-Funktion verwendet wird oder für die die Berechnung von Zellwerten erforderlich ist. Geben Sie nach Möglichkeit nur ein einzelnes Element an, um bei der Zellberechnung eine optimale Leistung zu erzielen.  
  
 Farbausdrücke  
 Gibt MDX-Ausdrücke an, die die Vorder- und Hintergrundfarbe von Zellen dynamisch basierend auf dem Wert des berechneten Elements festlegen. Diese Eigenschaft wird ignoriert, wenn sie von Clientanwendungen nicht unterstützt wird.  
  
 Schriftartausdrücke  
 Gibt MDX-Ausdrücke an, die Schriftart, Schriftgrad und Schriftattribute für Zellen dynamisch basierend auf dem Wert des berechneten Elements festlegen. Diese Eigenschaft wird ignoriert, wenn sie von Clientanwendungen nicht unterstützt wird.  
  
 Sie können Cubekomponenten aus der Registerkarte **Metadaten** im Bereich **Berechnungstools** in das Feld **Ausdruck** im Bereich für Berechnungsausdrücke kopieren oder ziehen. Sie können Funktionen aus der Registerkarte **Funktionen** im Bereich **Berechnungstools** in das Feld **Ausdruck** im Bereich für Berechnungsausdrücke kopieren oder ziehen.  
  
## <a name="addressing-calculated-members"></a>Adressieren von berechneten Elementen  
 Wenn Sie ein berechnetes Element im **Cube-Designer** auf der Registerkarte **Berechnungen**erstellen, geben Sie die übergeordnete Hierarchie an, in der das berechnete Element gespeichert wird. Die übergeordnete Hierarchie bestimmt anhand der folgenden Regeln, wie ein berechnetes Element adressiert werden kann:  
  
-   Wenn ein berechnetes Element in der Measuredimension erstellt wird, ist das berechnete Element in dieser Dimension adressierbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
