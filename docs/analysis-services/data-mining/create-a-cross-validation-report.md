---
title: "Erstellen von Berichten f&#252;r Kreuzvalidierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überprüfen von Data Mining-Modellen"
  - "Miningstrukturen [Analysis Services], Themen zur Vorgehensweise"
  - "Kreuzvalidierung [Data Mining]"
  - "Statistische Standardabweichung"
ms.assetid: 7b1fec4c-7053-41eb-b030-5179257967a4
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 17
---
# Erstellen von Berichten f&#252;r Kreuzvalidierung
  In diesem Thema wird die Erstellung eines Kreuzvalidierungsberichts auf der Registerkarte "Genauigkeitsdiagramm" im Data Mining-Designer erläutert. Allgemeine Informationen zum Aussehen eines Kreuzvalidierungsberichts und zu den statistischen Measures, die er enthält, finden Sie unter [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).  
  
 Ein Kreuzvalidierungsbericht unterscheidet sich grundlegend von einem Genauigkeitsdiagramm, z. B. ein Prognosegütediagramm oder eine Klassifikationsmatrix.  
  
-   Bei der Kreuzvalidierung wird die Gesamtverteilung von Daten bewertet, die in einem Modell oder einer Struktur verwendet werden. Daher wird auch kein Testdataset angegeben. Bei der Kreuzvalidierung werden immer nur die ursprünglichen Daten verwendet, mit denen das Modell oder die Miningstruktur trainiert wurde.  
  
-   Kreuzvalidierung kann nur hinsichtlich eines einzelnen vorhersagbaren Ergebnisses ausgeführt werden. Wenn die Struktur Modelle unterstützt, die über andere vorhersagbare Attribute verfügen, müssen Sie separate Berichte für jede vorhersagbare Ausgabe erstellen.  
  
-   Nur Modelle, die mit der gerade ausgewählten Struktur verknüpft werden, sind für die Kreuzvalidierung verfügbar.  
  
-   Wenn die derzeit ausgewählte Struktur eine Kombination aus Clustering- und Nicht-Clusteringmodellen unterstützt, lädt die gespeicherte Kreuzvalidierungsprozedur nach einem Klick auf **Ergebnisse abrufen** automatisch Modelle, die über die gleiche vorhergesagte Spalte verfügen. Clusteringmodelle, die nicht das gleiche vorhersagbare Attribut verwenden, werden ignoriert.  
  
-   Sie können einen Kreuzvalidierungsbericht für ein Clusteringmodell erstellen, das nur dann nicht über ein vorhersagbares Attribut verfügt, wenn die Miningstruktur keine anderen vorhersagbaren Attribute unterstützt.  
  
### Auswählen einer Miningstruktur  
  
1.  Öffnen Sie den Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Öffnen Sie in Projektmappen-Explorer die Datenbank, die die Struktur oder das Modell enthält, für das Sie einen Bericht erstellen möchten.  
  
3.  Doppelklicken Sie im Data Mining-Designer auf die Miningstruktur, um die Struktur und die zugehörigen Modelle zu öffnen.  
  
4.  Klicken Sie auf die Registerkarte **Mininggenauigkeitsdiagramm** .  
  
5.  Klicken Sie auf die Registerkarte **Kreuzvalidierung** .  
  
### Festlegen von Kreuzvalidierungsoptionen  
  
1.  Klicken Sie auf der Registerkarte **Kreuzvalidierung** für **Foldanzahl**auf den Pfeil nach unten, um eine Zahl zwischen 1 und 10 auszuwählen. Der Standardwert lautet 10.  
  
     Die **Foldanzahl** stellt die Anzahl von Partitionen dar, die innerhalb des ursprünglichen Datasets erstellt werden. Wenn Sie die Foldanzahl auf 1 festgelegt haben, wird der Trainingssatz ohne Partitionierung verwendet.  
  
2.  Klicken Sie für **Zielattribut**auf den Pfeil nach unten, und wählen Sie eine Spalte aus der Liste aus. Wenn das Modell ein Clustermodell ist, wählen Sie **#Cluster**, um anzugeben, dass das Modell nicht über ein vorhersagbares Attribut verfügt. Beachten Sie, dass der Wert **#Cluster** nur verfügbar ist, wenn die Miningstruktur keine anderen vorhersagbaren Attributtypen unterstützt.  
  
     Sie können nur ein vorhersagbares Attribut pro Bericht auswählen. Standardmäßig sind alle zugehörigen Modelle, die über das gleiche vorhersagbare Attribut verfügen, im Bericht enthalten.  
  
3.  Geben Sie für **Maximale Anzahl von Fällen**eine Zahl ein, die groß genug ist, um eine repräsentative Stichprobe von Daten bereitzustellen, wenn die Daten auf die angegebene Anzahl von Aufteilungen aufgeteilt wird. Wenn Sie eine Zahl angeben, die größer ist als die Anzahl der tatsächlichen Fälle im Trainingssatz des Modells, werden alle Fälle verwendet.  
  
     Wenn der Trainingsdatensatz sehr groß ist, können Sie über den unter **Maximale Anzahl von Fällen** eingegebenen Wert die Gesamtzahl der verarbeiteten Fälle einschränken. Der Bericht kann so schneller beendet werden. Sie sollten jedoch keinen zu kleinen Wert für **Maximale Anzahl von Fällen** eingeben, da ansonsten möglicherweise nicht genügend Daten zur Kreuzvalidierung zur Verfügung stehen.  
  
4.  Geben Sie optional für **Zielstatus**den Wert des vorhersagbaren Attributs ein, das Sie modellieren möchten. Wenn zum Beispiel die Spalte [Fahrradkäufer] zwei mögliche Werte enthält, nämlich 1 (Ja) und 2 (Nein), können Sie den Wert 1 eingeben, um die Genauigkeit des Modells nur für das gewünschte Ergebnis zu bewerten.  
  
    > [!NOTE]  
    >  Wenn Sie keinen Wert eingeben, ist die Option **Zielschwellenwert** nicht verfügbar, und das Modell wird für alle möglichen Werte des vorhersagbaren Attributs bewertet.  
  
5.  Geben Sie optional für **Zielschwellenwert**eine Dezimalzahl zwischen 0 und 1 ein, um anzugeben, welche Mindestwahrscheinlichkeit eine Vorhersage erreichen muss, damit sie als genau gelten kann.  
  
     Zusätzliche Tipps zur Festlegung von Wahrscheinlichkeitsschwellenwerten finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
6.  Klicken Sie auf **Ergebnisse abrufen**.  
  
### Drucken des Kreuzvalidierungsberichts  
  
1.  Klicken Sie auf der Registerkarte **Kreuzvalidierung** mit der rechten Maustaste auf den abgeschlossenen Bericht.  
  
2.  Wählen Sie aus dem Kontextmenü die Option **Drucken** oder **Seitenansicht** , um zunächst den Bericht zu überprüfen.  
  
### Erstellen einer Kopie des Berichts in Microsoft Excel  
  
1.  Klicken Sie auf der Registerkarte **Kreuzvalidierung** mit der rechten Maustaste auf den abgeschlossenen Bericht.  
  
2.  Wählen Sie im Kontextmenü die Option **Alles auswählen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den ausgewählten Text, und wählen Sie **Kopieren**.  
  
4.  Fügen Sie die Auswahl in eine geöffnete Excel-Arbeitsmappe ein. Wenn Sie die Option **Einfügen** verwenden, wird der Bericht als HTML in Excel eingefügt. Auf diese Weise werden Zeilen- und Spaltenformatierung beibehalten. Wenn Sie den Bericht mit den Optionen für **Inhalte einfügen** für Text oder Unicode-Text einfügen, wird der Bericht im nach Zeilen getrennten Format eingefügt.  
  
## Siehe auch  
 [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)  
  
  