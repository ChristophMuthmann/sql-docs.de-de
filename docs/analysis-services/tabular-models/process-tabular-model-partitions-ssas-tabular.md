---
title: Verarbeiten von Tabellenmodellpartitionen | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1e4440fad2c2132cfec851c2d55779a11c141145
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="process-tabular-model-partitions"></a>Verarbeiten von Tabellenmodellpartitionen 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Durch Partitionen wird eine Tabelle logisch unterteilt. Jede Partition kann unabhängig von anderen Partitionen verarbeitet (aktualisiert) werden. In den Tasks in diesem Thema wird beschrieben, wie Partitionen in einer Modelldatenbank mithilfe des Dialogfelds **Partition(en) verarbeiten** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verarbeitet werden.  
  
###  <a name="bkmk_create_new"></a> So verarbeiten Sie eine Partition  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]mit der rechten Maustaste auf die Tabelle, die die zu verarbeitenden Partitionen enthält, und klicken Sie anschließend auf **Partitionen**.  
  
2.  Klicken Sie im Dialogfeld **Partitionen** unter **Partitionen**auf die Schaltfläche Verarbeiten.  
  
3.  Wählen Sie im Dialogfeld **Partition(en) verarbeiten** im Listenfeld **Modus** einen der folgenden Verarbeitungsmodi aus:  
  
    |Modus|Description|  
    |----------|-----------------|  
    |**Standard verarbeiten**|Erkennt den Verarbeitungsstatus eines Partitionsobjekts und führt die Verarbeitung durch, durch die nicht oder teilweise verarbeitete Partitionsobjekte in den Status "Vollständig verarbeitet" versetzt werden. Daten für leere Tabellen und Partitionen werden geladen, Hierarchien, berechnete Spalten und Beziehungen werden erstellt oder neu erstellt.|  
    |**Vollständig verarbeiten**|Verarbeitet ein Partitionsobjekt und alle darin enthaltenen Objekte. Wenn die Verarbeitungsmethode "Vollständig verarbeiten" für ein bereits verarbeitetes Objekt ausgeführt wird, löscht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Daten im Objekt und verarbeitet anschließend das Objekt. Diese Art der Verarbeitung ist erforderlich, wenn eine Änderung an der Objektstruktur vorgenommen wurde.|  
    |**Daten verarbeiten**|Lädt Daten in eine Partition oder Tabelle, ohne Hierarchien oder Beziehungen neu zu erstellen bzw. berechnete Spalten und Measures neu zu berechnen.|  
    |**Löschung verarbeiten**|Entfernt alle Daten aus einer Partition.|  
    |**Hinzufügung verarbeiten**|Aktualisiert die Partition inkrementell mit neuen Daten.|  
  
4.  Wählen Sie in der Spalte der Kontrollkästchen unter **Verarbeiten** die Partitionen aus, die im ausgewählten Modus verarbeitet werden sollen, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenmodellpartitionen](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Erstellen und Verwalten von Tabellenmodellpartitionen](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
