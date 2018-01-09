---
title: "Wählen Sie eine Genauigkeit Diagrammtyp und einen Satz Diagrammoptionen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- Mining Accuracy Chart [Analysis Services]
- mining models [Analysis Services], validating
- classification accuracy [data mining]
- accuracy testing [data mining]
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dd7b16d8d707b05a57313c526ec721083d610db3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>Auswählen eines Genauigkeitsdiagrammtyps Festlegen von Diagrammoptionen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt mehrere Methoden zum Bestimmen der Gültigkeit Ihrer Miningmodelle bereit. Der Typ des Genauigkeitsdiagramms, das Sie für jedes Modell oder jede Struktur erstellen können, hängt von diesen Faktoren ab:  
  
-   Dem Algorithmustyp, der verwendet wurde, um das Modell zu erstellen  
  
-   Dem Datentyp des vorhersagbaren Attributs  
  
-   Der Anzahl der zu messenden vorhersagbaren Attribute  
  
 In diesem Thema findet sich eine Übersicht über die verschiedenen Genauigkeitsdiagramme.  
  
 **Hinweis** Diagramme und ihre Definitionen werden nicht gespeichert. Wenn Sie das Fenster schließen, das ein Diagramm enthält, müssen Sie das Diagramm erneut erstellen.  
  
## <a name="accuracy-chart-types"></a>Genauigkeitsdiagrammtypen  
 Abhängig vom ausgewählten Diagrammtyp können Sie weitere Optionen konfigurieren, um das Diagramm zu durchsuchen oder das Diagramm in die Zwischenablage zu kopieren und mit den Daten in Excel zu arbeiten.  
  
#### <a name="lift-chart"></a>Prognosegütediagramm  
 Nachdem Sie die Optionen für das Modell konfiguriert und die Daten getestet haben, klicken Sie auf die Registerkarte **Prognosegütediagramm** , um die Ergebnisse anzuzeigen. Sie können das Diagramm auch in die Zwischenablage kopieren oder Details einzelner Trendlinien oder Datenpunkte in der Mininglegende anzeigen.  
  
#### <a name="profit-chart"></a>Gewinndiagramm  
 Nachdem Sie die Optionen für das Modell und die Testdaten konfiguriert haben, klicken Sie auf die Registerkarte **Prognosegütediagramm** , wählen Sie **Gewinndiagramm** in der Liste **Diagrammtyp** aus, um die Optionen für das Gewinndiagramm festzulegen, und klicken Sie anschließend auf **OK** , um die Ergebnisse anzuzeigen.  
  
 Sie können das Dialogfeld **Gewinndiagrammeinstellungen** beliebig oft verwenden, um verschiedene Kostenoptionen auszuprobieren und das Diagramm erneut anzuzeigen. Die Mininglegende enthält ausführliche Informationen über den geschätzten Gewinn für jedes Modell. Sie können auch das Diagramm und den Inhalt der Mininglegende in die Zwischenablage kopieren, um in Excel damit zu arbeiten.  
  
#### <a name="scatter-plot"></a>Punktdiagramm  
 Wenn Sie den entsprechenden Modelltyp ausgewählt haben, ist bei Klicken auf die Registerkarte **Prognosegütediagramm** als Diagrammtyp automatisch **Punktdiagramm** festgelegt, und ein Punktdiagramm wird angezeigt. Eine weitere Konfiguration ist nicht möglich. Sie können das Diagramm auch in die Zwischenablage kopieren und als Grafik in Excel oder in eine andere Anwendung einfügen.  
  
#### <a name="classification-matrix"></a>Klassifikationsmatrix  
 Für eine Klassifikationsmatrix wählen Sie auf der Registerkarte **Eingabeauswahl** die Modelle und Testdaten aus und klicken anschließend auf die Registerkarte **Klassifikationsmatrix** , um die Ergebnisse anzuzeigen.  
  
 Der Inhalt einer Klassifikationsmatrix ist bei allen Modelltypen gleich und kann nicht konfiguriert werden. Sie können die Daten im Diagramm in die Zwischenablage kopieren, um sie in Excel zu verwenden.  
  
#### <a name="cross-validation-report"></a>Bericht für die übergreifende Überprüfung  
 Um einen Kreuzvalidierungsbericht zu erstellen, wählen Sie zunächst eine Miningstruktur oder ein Miningmodell im Projektmappen-Explorer aus. Klicken Sie anschließend auf die Registerkarte **Kreuzvalidierung** , konfigurieren Sie alle relevanten Optionen, und klicken Sie dann auf **Ergebnisse abrufen** , um den Bericht zu generieren. Eine weitere Konfiguration ist nicht möglich.  
  
 Das Format des Kreuzvalidierungsberichts ist bei allen Modelltypen gleich und kann nicht konfiguriert werden. Der Inhalt des Berichts ist jedoch abhängig vom analysierten Modelltyp und vom Datentyp des vorhersagbaren Attributs unterschiedlich. Sie können die Ergebnisse des Berichts auch in die Zwischenablage kopieren, um in Excel mit den Daten zu arbeiten.  
  
  
