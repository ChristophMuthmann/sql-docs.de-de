---
title: Erstellen einer berechneten Spalte | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.as.daxref.CreataCalculatedColumn.f1
ms.assetid: 59440510-2d76-41dc-9b55-edc15259f9da
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0c65bd6bd047a676c87bacb9197e11d3205eeaef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-calculated-column"></a>Erstellen einer berechneten Spalte
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Mithilfe berechneter Spalten können Sie dem Modell neue Daten hinzufügen. Anstatt Werte in die Spalte einzufügen oder zu importieren, erstellen Sie eine DAX-Formel, mit der die Zeilenebenenwerte der Spalte definiert werden. Die Werte in den einzelnen Zeilen einer berechneten Spalte werden berechnet und aufgefüllt, wenn Sie eine gültige Formel erstellen und die EINGABETASTE drücken. Die berechnete Spalte kann anschließend wie jeder andere Datenspalte einer Berichterstellungs- oder Analyseanwendung hinzugefügt werden. Dieser Artikel beschreibt, wie eine neue berechnete Spalte mithilfe der DAX-Bearbeitungsleiste im Modell-Designer erstellt wird.  
  
#### <a name="to-create-a-new-calculated-column"></a>So erstellen Sie eine neue berechnete Spalte  
  
1.  Wählen Sie im Modell-Designer in der Datensicht die Tabelle aus, der Sie eine berechnete Spalte hinzufügen möchten, und klicken Sie dann auf das Menü **Spalte** und auf **Spalte hinzufügen**.  
  
     In der leeren Spalte am äußersten rechten Rand wird**Spalte hinzufügen** hervorgehoben, und der Cursor wird in die Bearbeitungsleiste verschoben.  
  
     Klicken Sie mit der rechten Maustaste auf eine vorhandene Spalte, und klicken Sie dann auf **Spalte einfügen**, um zwischen zwei vorhandenen Spalten eine neue Spalte zu erstellen.  
  
2.  Führen Sie in der Bearbeitungsleiste einen der folgenden Schritte aus:  
  
    -   Geben Sie ein Gleichheitszeichen gefolgt von einer Formel ein.  
  
    -   Geben Sie ein Gleichheitszeichen gefolgt von einer DAX-Funktion, den Argumenten und Parametern ein, die von der Funktion benötigt werden.  
  
    -   Klicken Sie auf die Funktionsschaltfläche (**fx**), und wählen Sie dann im Dialogfeld **Funktion einfügen** eine Kategorie und eine Funktion aus. Klicken Sie abschließend auf **OK**. Geben Sie in der Bearbeitungsleiste die übrigen Argumente und Parameter ein, die von der Funktion benötigt werden.  
  
3.  Drücken Sie die EINGABETASTE, um die Formel zu übernehmen.  
  
     Die gesamte Spalte wird mit der Formel aufgefüllt, d. h., für jede Zeile wird ein Wert berechnet.  
  
> [!TIP]  
>  Sie können AutoVervollständigen für DAX-Formeln auch mitten in einer vorhandenen Formel mit geschachtelten Funktionen verwenden. Ausgehend vom Text unmittelbar vor der Einfügemarke werden Werte in der Dropdownliste angezeigt. Der Text nach der Einfügemarke bleibt unverändert.  
  
## <a name="see-also"></a>Siehe auch  
 [Berechnete Spalten](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Measures](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
