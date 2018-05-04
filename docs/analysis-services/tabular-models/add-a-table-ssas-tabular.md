---
title: Hinzufügen einer Tabelle | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d713c432-db99-4983-acc1-52b0fdd58bd6
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a08da48e4b116d9a2fe00f16e49fc2bee66b1552
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="add-a-table"></a>Hinzufügen einer Tabelle
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Dieser Artikel beschreibt, wie eine Tabelle aus einer Datenquelle hinzufügen, von dem Sie Daten bereits in das Modell importiert haben. Um eine Tabelle aus derselben Datenquelle hinzuzufügen, können Sie die vorhandene Datenquellenverbindung verwenden. Es wird empfohlen, immer eine einzelne Verbindung zu verwenden, wenn Sie eine beliebige Anzahl von Tabellen aus einer einzelnen Datenquelle importieren.  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>So fügen Sie eine Tabelle aus einer vorhandenen Datenquelle hinzu  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Menü **Modell** auf **Vorhandene Verbindungen**.  
  
2.  Wählen Sie auf der Seite **Vorhandene Verbindungen** die Verbindung mit der Datenquelle aus, die über die hinzuzufügende Tabelle verfügt, und klicken Sie dann auf **Öffnen**.  
  
3.  Wählen Sie auf der Seite **Tabellen und Sichten auswählen** die Tabelle aus der Datenquelle aus, die Sie dem Modell hinzufügen möchten.  
  
    > [!NOTE]  
    >  Die Seite **Tabellen und Sichten auswählen** enthält keine Tabellen, die zuvor als überprüft importiert wurden.  Wenn Sie eine Tabelle auswählen, die zuvor mithilfe dieser Verbindung importiert wurde, und Sie der Tabelle keinen anderen Anzeigenamen gegeben haben, wird eine 1 an den Anzeigenamen angefügt. Tabellen, die zuvor mithilfe dieser Verbindung importiert wurden, müssen nicht erneut ausgewählt werden.  
  
4.  Verwenden Sie ggf. **Vorschau und Filter**, um nur bestimmte Spalten auszuwählen bzw. Filter auf die zu importierenden Daten anzuwenden.  
  
5.  Klicken Sie auf **Fertig stellen** , um die neue Tabelle zu importieren.  
  
> [!NOTE]  
>  Wenn Sie mehrere Tabellen gleichzeitig aus einer einzelnen Datenquelle importieren, werden im Modell automatisch die Tabellenbeziehungen erstellt, die in der Datenquelle vorhanden waren. Wenn Sie später eine Tabelle hinzufügen, kann es jedoch erforderlich sein, manuell Beziehungen zwischen den neu hinzugefügten und den zuvor importierten Tabellen im Modell zu erstellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Importieren von Daten](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Löschen einer Tabelle](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
