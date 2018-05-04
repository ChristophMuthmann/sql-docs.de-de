---
title: Erstellen Sie eine Singleton-Abfrage aus einer Vorlage | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d88b4abff562214ec971410835ec1978232302f9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>Erstellen einer SINGLETON-Vorhersageabfrage aus einer Vorlage
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine SINGLETON-Abfrage ist für Modelle hilfreich, die Sie für Vorhersagen verwenden möchten, ohne sie jedoch einem externen Eingabedataset zuzuordnen oder sie für Massenvorhersagen zu verwenden. Mit einer SINGLETON-Abfrage können Sie einen Wert oder Werte für das Modell bereitstellen und sofort den vorhergesagten Wert anzeigen.  
  
 Zum Beispiel stellt die folgende DMX-Abfrage eine SINGLETON-Abfrage für das als Ziel verwendete Mailingmodell dar (TM_Decision_Tree).  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 In der folgenden Vorgehensweise wird beschrieben, wie die Abfrage mit dem Vorlagen-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] rasch erstellt wird.  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>So öffnen Sie die Analysis Services-Vorlagen in SQL Server Management Studio  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Ansicht** auf **Vorlagen-Explorer**.  
  
2.  Klicken Sie auf das Cubesymbol, um die **Analysis-Server**-Vorlagen zu öffnen.  
  
### <a name="to-open-a-prediction-query-template"></a>So öffnen Sie eine Vorhersageabfragevorlage  
  
1.  Erweitern Sie im **Vorlagen-Explorer**in der Liste der Analysis-Server-Vorlagen **DMX**, und erweitern Sie dann **Vorhersageabfragen**.  
  
2.  Doppelklicken Sie auf **Singleton-Vorhersage**.  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Analysis Services herstellen** den Namen des Servers ein, auf dem sich die Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] befindet, die das abzufragende Miningmodell enthält.  
  
4.  Klicken Sie auf **Verbinden**.  
  
5.  Die Vorlage wird in der angegebenen Datenbank geöffnet, zusammen mit einem Miningmodell-Objektkatalog, der Data Mining-Funktionen und eine Liste von Data Mining-Strukturen und zugehörige Modelle enthält.  
  
### <a name="to-customize-the-singleton-query-template"></a>So passen Sie die SINGLETON-Abfragevorlage an  
  
1.  Klicken Sie in der Vorlage auf die Dropdownliste **Verfügbare Datenbanken** , und wählen Sie in der Liste eine Instanz von Analysis Service aus.  
  
2.  Wählen Sie in der Liste **Miningmodell** das Miningmodell aus, das Sie abfragen möchten.  
  
     Die Liste der Spalten im Miningmodell wird im Bereich **Metadaten** des Objektkatalogs angezeigt.  
  
3.  Wählen Sie im Menü **Abfrage** die Option **Werte für Vorlagenparameter angeben**aus.  
  
4.  Geben Sie in der Zeile **Liste auswählen** das Platzhalterzeichen * ein, um alle Spalten zurückzugeben, oder geben Sie eine durch Komma getrennte Liste von Spalten und Ausdrücken ein, um bestimmte Spalten zurückzugeben.  
  
     Wenn Sie * eingeben, wird die vorhersagbare Spalte zurückgegeben sowie alle Spalten, für die Sie in Schritt 6 neue Werte eingegeben haben.  
  
     In dem Beispielcode am Beginn dieses Themas wurde * in die Zeile **Liste auswählen** eingegeben.  
  
5.  Geben Sie in der Zeile **Miningmodell** den Namen eines Miningmodells aus der Liste der Miningmodelle im **Objekt-Explorer**ein.  
  
     In dem Beispielcode am Beginn dieses Themas wurde für die Zeile **Miningmodell** der Name **TM_Decision_Tree**eingegeben.  
  
6.  Geben Sie in der Zeile **Wert** den neuen Datenwert ein, für den Sie eine Vorhersage machen möchten.  
  
     In dem Beispielcode am Beginn dieses Themas wurde **2** in die Zeile **Wert** eingegeben, um das Kaufverhalten bezüglich Fahrrädern auf der Grundlage der vorhandenen Kinder vorherzusagen.  
  
7.  Geben Sie in der Zeile **Spalte** den Namen der Spalte im Miningmodell ein, der die neuen Daten zugeordnet werden sollen.  
  
     In dem Beispielcode am Beginn dieses Themas wurde **Number Children at Home** in die Zeile **Spalte**eingegeben.  
  
    > [!NOTE]  
    >  Wenn Sie das Dialogfeld **Werte für Vorlagenparameter angeben** verwenden, müssen Sie den Spaltennamen nicht in eckige Klammern einzuschließen. Die Klammern werden automatisch hinzugefügt.  
  
8.  Behalten Sie den Wert **t** für **Eingabealias**bei.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Suchen Sie im Abfragetextbereich nach einer roten Wellenlinie unter dem Komma und den Auslassungspunkten, die Syntaxfehler anzeigt. Löschen Sie die Auslassungspunkte, und fügen Sie alle weiteren gewünschten Abfragebedingungen hinzu. Wenn Sie keine weiteren Bedingungen hinzufügen, löschen Sie das Komma.  
  
     In dem Beispielcode am Beginn dieses Themas wurde für die zusätzliche Abfragebedingung **'45' as [Age]** eingegeben.  
  
11. Klicken Sie auf **Ausführen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Vorhersagen & #40; Lernprogramm zu Datamining-Lernprogramm & #41;](http://msdn.microsoft.com/library/a8410ed2-bb98-4d51-a9eb-b239be1201c2)  
  
  
