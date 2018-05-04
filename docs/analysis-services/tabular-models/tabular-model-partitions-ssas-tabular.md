---
title: Tabellenmodellpartitionen | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.ssms.partitions.partitionmgr.imbi.f1
ms.assetid: 041c269f-a229-4a41-8794-6ba4b014ef83
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e41f3d5e459e852b9f7323fc1631b149c7b77faa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tabular-model-partitions"></a>Tabellenmodellpartitionen 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Durch Partitionen wird eine Tabelle logisch unterteilt. Jede Partition kann unabhängig von anderen Partitionen verarbeitet (aktualisiert) werden. Während der Modellerstellung werden die für ein Modell definierten Partitionen in ein bereitgestelltes Modell dupliziert. Nach der Bereitstellung können Sie diese Partitionen mit dem Dialogfeld **Partitionen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mithilfe eines Skripts verwalten. In diesem Thema werden Partitionen in einer Datenbank für bereitgestellte tabellarische Modelle beschrieben. Weitere Informationen zum Erstellen und Verwalten von Partitionen während der Modellerstellung finden Sie unter [Partitionen](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
 Abschnitte in diesem Thema:  
  
-   [Vorteile](#bkmk_benefits)  
  
-   [Berechtigungen](#bkmk_permissions)  
  
-   [Partitionen verarbeiten](#bkmk_process_partitions)  
  
-   [Parallelverarbeitung](#bkmk_parallelProc)  
  
-   [Verwandte Aufgaben](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Vorteile  
 Bei einem effizienten Modellentwurf werden Partitionen genutzt, um unnötige Verarbeitungsschritte und die daraus resultierende Belastung der Analysis Services-Serverprozessoren zu eliminieren und gleichzeitig sicherzustellen, dass bestimmte Daten so häufig verarbeitet und aktualisiert werden, dass immer die neuesten Daten aus den Datenquellen bereitgestellt werden.  
  
 Ein tabellarisches Modell kann beispielsweise über eine Sales-Tabelle verfügen, die Umsatzzahlen für das laufende Geschäftsjahr 2011 und jedes vorangehende Geschäftsjahr umfasst. Die Sales-Tabelle des Modells verfügt über die folgenden drei Partitionen:  
  
|Partition|Daten aus|  
|---------------|---------------|  
|Sales2011|Aktuelles Geschäftsjahr|  
|Sales2010-2001|Geschäftsjahre 2001, 2002, 2003, 2004, 2005, 2006. 2007, 2008, 2009, 2010|  
|SalesOld|Alle Geschäftsjahre vor den letzten zehn Jahren.|  
  
 Während neue Umsatzzahlen für das laufende Geschäftsjahr 2011 hinzugefügt werden, müssen die Daten täglich verarbeitet werden, damit sie in der Umsatzanalyse für das laufende Geschäftsjahr entsprechend berücksichtigt werden; die Partition "Sales2011" wird folglich nachts verarbeitet.  
  
 Im Unterschied dazu ist es nicht erforderlich, die Daten der Partition "Sales2010-2001" nachts zu verarbeiten. Da sich die Umsatzzahlen für die vorangegangenen zehn Geschäftsjahre aufgrund von Produktrücksendungen und anderen Anpassungen jedoch ändern können, müssen sie immer noch regelmäßig verarbeitet werden. Die Daten in der Partition "Sales2010-2001" werden folglich monatlich verarbeitet. Die Daten in der Partition "SalesOld" ändern sich nie und werden daher nur jährlich verarbeitet.  
  
 Wenn Sie das Geschäftsjahr 2012 eingeben, wird der Sales-Tabelle des Modells die neue Partition "Sales2012" hinzugefügt. Die Partition "Sales2011" kann dann mit der Partition "Sales2010-2001" zusammengeführt und in "Sales2011-2002" umbenannt werden. Die Daten aus dem Geschäftsjahr 2001 werden aus der neuen Partition "Sales2011-2002" entfernt und in die Partition "SalesOld" verschoben. Alle Partitionen werden daraufhin verarbeitet, damit die Änderungen berücksichtigt werden.  
  
 Wie ein Unternehmen eine Partitionsstrategie für seine tabellarischen Modelle implementiert, hängt im Wesentlichen von den Verarbeitungsanforderungen für die jeweiligen Modelldaten und den verfügbaren Ressourcen ab.  
  
##  <a name="bkmk_permissions"></a> Berechtigungen  
 Damit Sie Partitionen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen, verwalten und verarbeiten können, müssen die entsprechenden Analysis Services-Berichtigungen in einer Sicherheitsrolle definiert sein. Jede Sicherheitsrolle verfügt über eine der folgenden Berechtigungen:  
  
|Berechtigung|Aktionen|  
|----------------|-------------|  
|Administrator|Lesen, Verarbeiten, Erstellen, Kopieren, Zusammenführen, Löschen|  
|Verarbeiten|Lesen, Verarbeiten|  
|Schreibgeschützt|Lesen|  
  
 Weitere Informationen zum Erstellen von Rollen während der Modellerstellung mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], finden Sie unter [Rollen](../../analysis-services/tabular-models/roles-ssas-tabular.md). Weitere Informationen zum Verwalten von Rollenmitglieder Rollen tabellarischer Modelle mithilfe von "bereitgestellt" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], finden Sie unter [Rollen für tabellarische Modelle](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
##  <a name="bkmk_parallelProc"></a> Parallelverarbeitung  
Analysis Services enthält die parallele Verarbeitung für Tabellen mit zwei oder mehr Partitionen, sodass die verarbeitungsleistung erhöht. Für die Parallelverarbeitung gibt es keine Konfigurationseinstellungen (siehe Hinweise). Die Parallelverarbeitung erfolgt standardmäßig bei der Verarbeitung von Tabellen bzw. wenn Sie für die gleiche Tabelle und den gleichen Prozess mehrere Partitionen auswählen. Dennoch können Sie die Partitionen einer Tabelle weiterhin auch einzeln verarbeiten.  
  
> [!NOTE]  
>  Sie können die Eigenschaftsoption **maxParallism** mit dem [Sequence-Befehl (TMSL)](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)verwenden, um anzugeben, ob Aktualisierungsvorgänge sequenziell oder parallel auszuführen sind.

> [!NOTE]  
>  Bei Feststellung einer erneuten Codierung kann die Parallelverarbeitung die Systemressourcen erheblich beanspruchen, da verschiedene Operationen auf den Partitionen unterbrochen und mit der neuen Codierung parallel neu gestartet werden müssen.  
  
##  <a name="bkmk_process_partitions"></a> Partitionen verarbeiten  
 Partitionen können in **mithilfe des Dialogfelds** Partitionen [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder mithilfe eines Skripts unabhängig von anderen Partitionen verarbeitet (bzw. aktualisiert) werden. Folgende Optionen stehen für die Verarbeitung zur Verfügung:  
  
|Mode|Description|  
|----------|-----------------|  
|Standard verarbeiten|Erkennt den Verarbeitungsstatus eines Partitionsobjekts und führt die Verarbeitung durch, durch die nicht oder teilweise verarbeitete Partitionsobjekte in den Status "Vollständig verarbeitet" versetzt werden. Daten für leere Tabellen und Partitionen werden geladen, Hierarchien, berechnete Spalten und Beziehungen werden erstellt oder neu erstellt.|  
|Vollständig verarbeiten|Verarbeitet ein Partitionsobjekt und alle darin enthaltenen Objekte. Wenn die Verarbeitungsmethode "Vollständig verarbeiten" für ein bereits verarbeitetes Objekt ausgeführt wird, löscht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Daten im Objekt und verarbeitet anschließend das Objekt. Diese Art der Verarbeitung ist erforderlich, wenn eine Änderung an der Objektstruktur vorgenommen wurde.|  
|Daten verarbeiten|Lädt Daten in eine Partition oder Tabelle, ohne Hierarchien oder Beziehungen neu zu erstellen bzw. berechnete Spalten und Measures neu zu berechnen.|  
|Löschung verarbeiten|Entfernt alle Daten aus einer Partition.|  
|Hinzufügung verarbeiten|Aktualisiert die Partition inkrementell mit neuen Daten.|  
  
##  <a name="bkmk_related_tasks"></a> Verwandte Aufgaben  
  
|Task|Description|  
|----------|-----------------|  
|[Erstellen und Verwalten von Tabellenmodellpartitionen](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)|Beschreibt, wie Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Partitionen in einem bereitgestellten tabellarischen Modell erstellen und verwalten.|  
|[Verarbeiten von Tabellenmodellpartitionen](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)|Beschreibt, wie Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Partitionen in einem bereitgestellten tabellarischen Modell verarbeiten.|  
  
  
