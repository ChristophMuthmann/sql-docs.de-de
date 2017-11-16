---
title: "Anfügen und Trennen von Analysis Services-Datenbanken | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.AttachDatabase.f1
- sql13.asvs.ssms.attachdatabase.f1
- sql13.asvs.ssmsimbi.DetachDatabase.f1
- sql13.asvs.ssms.detachdatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f4c193def48b92245c1e2f2955262d3fb0850957
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="attach-and-detach-analysis-services-databases"></a>Anfügen und Trennen von Analysis Services-Datenbanken
  Es gibt häufig Situationen, in denen ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankadministrator (DBA) eine Datenbank für eine bestimmte Zeit offline schalten und die Datenbank später auf derselben oder einer anderen Serverinstanz wieder online schalten möchte. Diese Situationen hängen in der Regel von Geschäftsforderungen ab, z. B. wenn die Datenbank zur Leistungssteigerung auf einen anderen Datenträger verschoben werden soll, wenn bei Datenbankzuwachs Platz geschaffen werden muss oder wenn ein Produkt aktualisiert werden soll. Für diese und weitere Fälle ermöglichen die Befehle **Attach** und **Detach** dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankadministrator, die Datenbank mit wenig Aufwand offline und später wieder online zu schalten.  
  
## <a name="attach-and-detach-commands"></a>Die Befehle "Attach" und "Detach"  
 Mit dem **Attach** -Befehl können Sie eine Datenbank, die offline geschaltet wurde, wieder online schalten. Sie können die Datenbank an die ursprüngliche Serverinstanz oder eine andere Instanz anfügen. Wenn Sie eine Datenbank anfügen, kann der Benutzer die **ReadWriteMode** -Einstellung für die Datenbank angeben. Mit dem **Detach** -Befehl können Sie eine Datenbank vom Server offline schalten.  
  
## <a name="attach-and-detach-usage"></a>Verwendung der Befehle "Attach" und "Detach"  
 Der **Attach** -Befehl wird verwendet, um eine vorhandene Datenbankstruktur online zu schalten. Wenn die Datenbank im **ReadWrite** -Modus angefügt wird, kann sie nur einmal an eine Serverinstanz angefügt werden. Wird die Datenbank hingegen im **ReadOnly** -Modus angefügt, kann sie mehrfach an verschiedene Serverinstanzen angefügt werden. Die gleiche Datenbank kann jedoch nicht mehr als einmal an die gleiche Serverinstanz angefügt werden. Bei dem Versuch, die gleiche Datenbank mehr als einmal anzufügen, wird ein Fehler ausgegeben, auch wenn die Daten in separate Ordner kopiert wurden.  
  
> [!IMPORTANT]  
>  Wenn für das Trennen der Datenbank ein Kennwort erforderlich ist, ist für das Anfügen der Datenbank das gleiche Kennwort erforderlich.  
  
 Der **Detach** -Befehl wird verwendet, um eine vorhandene Datenbankstruktur offline zu schalten. Geben Sie beim Trennen einer Datenbank ein Kennwort an, um vertrauliche Metadaten zu schützen.  
  
> [!IMPORTANT]  
>  Verwenden Sie zum Schutz des Inhalts der Datendateien eine Zugriffssteuerungsliste für den Ordner, die Unterordner und die Datendateien.  
  
 Wenn Sie eine Datenbank trennen, führt der Server folgende Schritte aus.  
  
|Trennen einer Datenbank mit Lese-/Schreibzugriff|Trennen einer schreibgeschützten Datenbank|  
|--------------------------------------|-------------------------------------|  
|1) Der Server gibt eine Anforderung für eine CommitExclusive-Sperre für die Datenbank aus.<br /><br /> 2) Der Server wartet, bis für alle laufenden Transaktionen ein Commit oder ein Rollback ausgeführt wird.<br /><br /> 3) Der Server erstellt alle Metadaten, die zum Trennen der Datenbank erforderlich sind.<br /><br /> 4) Die Datenbank wird als gelöscht markiert.<br /><br /> 5) Der Server führt einen Commit für die Transaktion aus.|1) Die Datenbank wird als gelöscht markiert.<br /><br /> 2) Der Server führt einen Commit für die Transaktion aus.<br /><br /> Hinweis: Das Kennwort für die Trennung kann für eine schreibgeschützte Datenbank nicht geändert werden. Wenn der Kennwortparameter für eine angefügte Datenbank, die bereits ein Kennwort enthält, angegeben wird, wird ein Fehler ausgegeben.|  
  
 Die Befehle **Attach** und **Detach** müssen als einzelne Vorgänge ausgeführt werden. Sie können nicht in der gleichen Transaktion mit anderen Vorgängen kombiniert werden. Außerdem sind die Befehle **Attach** und **Detach** unteilbare Transaktionsbefehle. Dies bedeutet, dass der Vorgang entweder erfolgreich ist oder fehlschlägt. Keine Datenbank wird in einem unvollendeten Status belassen.  
  
> [!IMPORTANT]  
>  Zum Ausführen des **Detach** -Befehls sind Server- oder Datenbankadministratorberechtigungen erforderlich.  
  
> [!IMPORTANT]  
>  Zum Ausführen des **Attach** -Befehls sind Serveradministratorberechtigungen erforderlich.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Verschieben einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Datenbank-ReadWriteModes](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Umschalten Sie in einer Analysis Services-Datenbank zwischen Schreib-und Lesemodus](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Detach-Element](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Attach-Element](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  

