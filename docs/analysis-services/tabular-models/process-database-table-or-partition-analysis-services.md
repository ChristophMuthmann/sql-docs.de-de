---
title: Verarbeiten von Datenbank, Tabelle oder Partition (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ASVS.SSMS.PARTITIONS.PROCESSINGOPTIONS.IMBI.F1
ms.assetid: 307d69c3-cabb-4dfa-b90c-9852492c1213
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 77ae5703b9a45a9f15eddfd4eb933fed62a9ab1a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="process-database-table-or-partition-analysis-services"></a>Verarbeiten von Datenbank, Tabelle oder Partition (Analysis Services)
  Die Aufgaben in diesem Thema wird beschrieben, wie eine tabellarische Modelldatenbank, Tabelle oder Partitionen mithilfe manuell verarbeitet die **Prozess \<Objekt >** im Dialogfeld [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Weitere Informationen zur Verarbeitung von tabellarischen Modellen finden Sie unter [Verarbeiten von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="bkmk_process_tasks"></a> Aufgaben  
  
###  <a name="bkmk_process_db"></a> So verarbeiten Sie eine Datenbank  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]mit der rechten Maustaste auf die Datenbank, die Sie verarbeiten möchten, und klicken Sie anschließend auf **Datenbank verarbeiten**.  
  
2.  Wählen Sie im Dialogfeld **Datenbank verarbeiten** im Listenfeld **Modus** einen der folgenden Verarbeitungsmodi aus:  
  
    |Modus|Description|  
    |----------|-----------------|  
    |**Standard verarbeiten**|Erkennt den Verarbeitungsstatus von Datenbankobjekten und führt die Verarbeitung durch, mit der nicht verarbeitete oder teilweise verarbeitete Objekte in den vollständig verarbeiteten Status versetzt werden. Daten für leere Tabellen und Partitionen werden geladen, Hierarchien, berechnete Spalten und Beziehungen werden erstellt oder neu erstellt (neu berechnet).|  
    |**Vollständig verarbeiten**|Verarbeitet eine Datenbank und alle in ihr enthaltenen Objekte. Wenn die Verarbeitungsmethode "Vollständig verarbeiten" für ein bereits verarbeitetes Objekt ausgeführt wird, löscht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Daten im Objekt und verarbeitet anschließend das Objekt. Diese Art der Verarbeitung ist erforderlich, wenn eine Änderung an der Objektstruktur vorgenommen wurde. Diese Option erfordert die meisten Ressourcen.|  
    |**Löschung verarbeiten**|Entfernt alle Daten aus Datenbankobjekten.|  
    |**Neuberechnung verarbeiten**|Aktualisiert und berechnet Hierarchien, Beziehungen und berechnete Spalten neu.|  
  
3.  Wählen Sie in der Spalte der Kontrollkästchen unter **Verarbeiten** die Partitionen aus, die im ausgewählten Modus verarbeitet werden sollen, und klicken Sie dann auf **OK**.  
  
###  <a name="bkmk_process_table"></a> So verarbeiten Sie eine Tabelle  
  
1.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in der tabellarischen Modelldatenbank, die die zu verarbeitende Tabelle enthält, den Knoten **Tabellen** , klicken Sie mit der rechten Maustaste auf die zu verarbeitende Tabelle, und klicken Sie anschließend auf **Tabelle verarbeiten**.  
  
2.  Wählen Sie im Dialogfeld **Tabelle verarbeiten** im Listenfeld **Modus** einen der folgenden Verarbeitungsmodi aus:  
  
    |Modus|Description|  
    |----------|-----------------|  
    |**Standard verarbeiten**|Erkennt den Verarbeitungsstatus eines Tabellenobjekts und führt die Verarbeitung durch, die nicht verarbeitete oder teilweise verarbeitete Objekte in den Status Vollständig verarbeitet bringt. Daten für leere Tabellen und Partitionen werden geladen, Hierarchien, berechnete Spalten und Beziehungen werden erstellt oder neu erstellt (neu berechnet).|  
    |**Vollständig verarbeiten**|Verarbeitet ein Tabellenobjekt und alle darin enthaltenen Objekte. Wenn die Verarbeitungsmethode "Vollständig verarbeiten" für ein bereits verarbeitetes Objekt ausgeführt wird, löscht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Daten im Objekt und verarbeitet anschließend das Objekt. Diese Art der Verarbeitung ist erforderlich, wenn eine Änderung an der Objektstruktur vorgenommen wurde. Diese Option erfordert die meisten Ressourcen.|  
    |**Daten verarbeiten**|Lädt Daten in eine Tabelle, ohne Hierarchien oder Beziehungen neu zu erstellen bzw. berechnete Spalten und Measures neu zu berechnen.|  
    |**Löschung verarbeiten**|Entfernt alle Daten aus einer Tabelle und vorhandenen Tabellenpartitionen.|  
    |**Defragmentierung verarbeiten**|Defragmentiert die Indizes der Erweiterungstabellen.|  
  
3.  Überprüfen Sie in der Spalte der Kontrollkästchen die Tabelle und wählen Sie optional zusätzlich zu verarbeitende Tabellen aus, und klicken Sie dann auf **OK**.  
  
###  <a name="bkmk_process_partition"></a> So verarbeiten Sie eine oder mehrere Partitionen  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]mit der rechten Maustaste auf die Tabelle, die die zu verarbeitenden Partitionen enthält, und klicken Sie anschließend auf **Partitionen**.  
  
2.  Klicken Sie im Dialogfeld **Partitionen** unter den Partitionen auf die Schaltfläche **Verarbeiten**.  
  
3.  Wählen Sie im Dialogfeld **Partition verarbeiten** im Listenfeld **Modus** einen der folgenden Verarbeitungsmodi aus:  
  
    |Modus|Description|  
    |----------|-----------------|  
    |**Standard verarbeiten**|Erkennt den Verarbeitungsstatus eines Partitionsobjekts und führt die Verarbeitung durch, durch die nicht oder teilweise verarbeitete Partitionsobjekte in den Status "Vollständig verarbeitet" versetzt werden. Daten für leere Tabellen und Partitionen werden geladen, Hierarchien, berechnete Spalten und Beziehungen werden erstellt oder neu erstellt (neu berechnet).|  
    |**Vollständig verarbeiten**|Verarbeitet ein Partitionsobjekt und alle darin enthaltenen Objekte. Wenn die Verarbeitungsmethode "Vollständig verarbeiten" für ein bereits verarbeitetes Objekt ausgeführt wird, löscht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Daten im Objekt und verarbeitet anschließend das Objekt. Diese Art der Verarbeitung ist erforderlich, wenn eine Änderung an der Objektstruktur vorgenommen wurde.|  
    |**Daten verarbeiten**|Lädt Daten in eine Partition oder Tabelle, ohne Hierarchien oder Beziehungen neu zu erstellen bzw. berechnete Spalten und Measures neu zu berechnen.|  
    |**Löschung verarbeiten**|Entfernt alle Daten aus einer Partition.|  
    |**Hinzufügung verarbeiten**|Aktualisiert die Partition inkrementell mit neuen Daten.|  
  
4.  Wählen Sie in der Spalte der Kontrollkästchen unter **Verarbeiten** die Partitionen aus, die im ausgewählten Modus verarbeitet werden sollen, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenmodellpartitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Erstellen und Verwalten von Tabellenmodellpartitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
