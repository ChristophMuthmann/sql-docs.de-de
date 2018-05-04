---
title: Ausblenden oder Einfrieren von Spalten | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.hideunhidecolumnsdb.f1
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4a98f96292409b3a5fc23ff1727eb1ea34efdeff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="hide-or-freeze-columns"></a>Ausblenden oder Einfrieren von Spalten 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Wenn es im Modell-Designer Spalten gibt, die Sie nicht in einer Tabelle anzeigen möchten, können Sie diese zeitweise ausblenden. Durch das Ausblenden einer Spalte erhalten Sie mehr Platz auf dem Bildschirm, um neue Spalten hinzuzufügen oder nur mit relevanten Datenspalten zu arbeiten. Sie können Spalten über das Menüband **Spalte** im Modell-Designer und über das Kontextmenü der einzelnen Spaltenüberschriften aus- und einblenden. Um einen Bereich eines Modells sichtbar zu halten, während Sie einen Bildlauf zu einem anderen Bereich des Modells ausführen, können Sie bestimmte Spalten in einem Bereich sperren, indem Sie sie fixieren.  
  
> [!IMPORTANT]  
>  Die Möglichkeit, Spalten auszublenden, dient nicht der Datensicherheit, sondern nur zur Vereinfachung und Kürzung der Spaltenliste im Modell-Designer oder in Berichten. Um Daten zu sichern, können Sie Sicherheitsrollen definieren. Durch Rollen können die anzeigbaren Metadaten und Daten auf die in der Rolle definierten Objekte eingeschränkt werden. Weitere Informationen finden Sie unter [Rollen](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
 Wenn Sie mit ausgeblendeten Spalten arbeiten, haben Sie die Möglichkeit, eine Spalte auszublenden, während Sie im Modell-Designer oder in Berichten arbeiten. Wenn Sie alle Spalten ausblenden, wird die gesamte Tabelle im Modell-Designer leer angezeigt.  
  
> [!NOTE]  
>  Wenn Sie viele Spalten ausblenden müssen, können Sie eine Perspektive erstellen, statt Spalten aus- und einzublenden. Eine Perspektive ist eine benutzerdefinierte Sicht der Daten, die das Arbeiten mit Teilmengen verknüpfter Daten erleichtert. Weitere Informationen finden Sie unter [erstellen und Verwalten von Perspektiven](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)  
  
### <a name="to-hide-an-individual-column"></a>So blenden Sie eine einzelne Spalte aus  
  
1.  Wählen Sie im Modell-Designer die Tabelle aus, die die auszublendende Spalte enthält.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Spalte, und klicken Sie dann auf **Spalten ausblenden**und auf **Aus Designer und aus Berichten**, **Aus Berichten**oder **Aus Designer**.  
  
### <a name="to-hide-multiple-columns"></a>So blenden Sie mehrere Spalten aus  
  
1.  Wählen Sie im Modell-Designer die Tabelle aus, die die auszublendenden Spalten enthält.  
  
2.  Klicken Sie auf das Menü **Spalten** , und klicken Sie dann auf **Aus- und einblenden**.  
  
3.  Suchen Sie im Dialogfeld **Spalten aus- und einblenden** diejenigen Spalten, die Sie ausblenden möchten, und deaktivieren Sie dann **In Designer** bzw. **In Berichten**.  
  
4.  Klicken Sie auf **OK**.  
  
### <a name="to-freeze-columns"></a>So fixieren Sie Spalten  
  
1.  Wählen Sie im Modell-Designer die Tabelle aus, die die zu fixierenden Spalten enthält.  
  
2.  Wählen Sie eine oder mehrere Spalten zum Fixieren aus.  
  
3.  Klicken Sie auf das Menü **Spalten** , und klicken Sie dann auf **Fixieren**.  
  
    > [!NOTE]  
    >  Wenn Spalten fixiert sind, werden Sie im Designer in der Tabelle nach links (bzw. nach vorne) verschoben. Wenn Sie die Fixierung der Spalte aufheben, wird diese nicht an ihre ursprüngliche Position zurückverschoben.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Spalten](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Perspektiven](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
