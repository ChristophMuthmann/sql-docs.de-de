---
title: Datenbank-ReadWriteModes | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], read/write
- databases [Analysis Services], read-only
ms.assetid: 03d7cb5c-7ff0-4e15-bcd2-7075d1b0dd69
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b7c48381d6f4cc1c7c92802f2028c73f8afb402d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="database-readwritemodes"></a>Datenbank-ReadWriteModes
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Es gibt häufig Situationen, wenn ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbankadministrator (Dba) eine Datenbank Lese-/Schreibzugriff in eine schreibgeschützte Datenbank ändern möchte oder umgekehrt. Diese Situationen hängen in der Regel von Unternehmensanforderungen ab, z.&nbsp;B. der Freigabe des Datenbankordners für mehrere Server zum dezentralen Skalieren einer Projektmappe und zur Verbesserung der Leistung. Die **ReadWriteMode** -Datenbankeigenschaft ermöglicht es dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -DBA, den Betriebsmodus der Datenbank in solchen Fällen problemlos zu ändern.  
  
## <a name="readwritemode-database-property"></a>ReadWriteMode-Datenbankeigenschaft  
 Die **ReadWriteMode** -Datenbankeigenschaft gibt an, ob sich die Datenbank im Lese-/Schreibmodus oder im schreibgeschützter Modus befindet. Hierbei handelt es sich um die beiden einzigen möglichen Werte der Eigenschaft. Wenn sich die Datenbank im schreibgeschützten Modus befindet, können keine Änderungen oder Updates für die Datenbank übernommen werden. Im Lese-/Schreibmodus können hingegen Änderungen und Updates vorgenommen werden. Die Datenbankeigenschaft **ReadWriteMode** wird als schreibgeschützte Eigenschaft definiert. Sie kann nur über einen **Attach** -Befehl festgelegt werden.  
  
 Wenn sich eine Datenbank im schreibgeschützten Modus befindet, gelten einige Beschränkungen, die sich auf die herkömmlichen für die Datenbank zulässigen Vorgänge auswirken können. Die eingeschränkten Vorgänge finden Sie in der folgenden Tabelle.  
  
|Schreibgeschützter Modus|Eingeschränkte Vorgänge|  
|-------------------|---------------------------|  
|XML/A-Befehle<br /><br /> <br /><br /> Hinweis: Beim Ausführen eines dieser Befehle wird ein Fehler ausgegeben.|**Create**<br /><br /> **Alter**<br /><br /> **Delete**<br /><br /> **Verarbeiten**<br /><br /> **MergePartitions**<br /><br /> **DesignAggregations**<br /><br /> **CommitTransaction**<br /><br /> **Restore**<br /><br /> **Synchronize**<br /><br /> **Insert**<br /><br /> **Update**<br /><br /> **Drop**<br /><br /> <br /><br /> Hinweis: Das Zellenrückschreiben ist in schreibgeschützten Datenbanken zulässig. Für die Änderungen kann jedoch kein Commit ausgeführt werden.|  
|MDX-Anweisungen<br /><br /> <br /><br /> Hinweis: Beim Ausführen einer dieser Anweisungen wird ein Fehler ausgegeben.|**COMMIT TRAN**<br /><br /> **CREATE SESSION CUBE**<br /><br /> **ALTER CUBE**<br /><br /> **ALTER DIMENSION**<br /><br /> **CREATE DIMENSION MEMBER**<br /><br /> **DROP DIMENSION MEMBER**<br /><br /> **ALTER DIMENSION**<br /><br /> <br /><br /> Hinweis: Excel-Benutzer können die Gruppenfunktion in Pivottabellen nicht verwenden, da diese Funktion intern mit den **CREATE SESSION CUBE** -Befehlen implementiert wird.|  
|DMX-Anweisungen<br /><br /> <br /><br /> Hinweis: Beim Ausführen einer dieser Anweisungen wird ein Fehler ausgegeben.|**CREATE [SESSION] MINING STRUCTURE**<br /><br /> **ALTER MINING STRUCTURE**<br /><br /> **DROP MINING STRUCTURE**<br /><br /> **CREATE [SESSION] MINING MODEL**<br /><br /> **DROP MINING MODEL**<br /><br /> **IMPORT**<br /><br /> **SELECT INTO**<br /><br /> **INSERT**<br /><br /> **UPDATE**<br /><br /> **DELETE**|  
|Hintergrundoperationen|Alle Hintergrundoperationen, die die Datenbank ändern würden, werden deaktiviert. Dies schließt die verzögerte Verarbeitung und proaktives Zwischenspeichern ein.|  
  
## <a name="readwritemode-usage"></a>Verwendung von ReadWriteMode  
 Die **ReadWriteMode** -Datenbankeigenschaft sollte im Rahmen eines **Attach** -Datenbankbefehls verwendet werden. Mit dem **Attach** -Befehl kann die Datenbankeigenschaft entweder auf **ReadWrite** oder auf **ReadOnly**festgelegt werden. Der **ReadWriteMode** -Datenbankeigenschaftswert kann nicht direkt aktualisiert werden, da die Eigenschaft als schreibgeschützt definiert ist. Datenbanken werden mit einer auf **ReadWriteMode** festgelegten **ReadWrite**-Eigenschaft erstellt. Eine Datenbank kann nicht im schreibgeschützten Modus erstellt werden.  
  
 Sie müssen eine Sequenz von **Detach/Attach** -Befehlen ausgeben, um die Datenbankeigenschaft **ReadWriteMode** von **ReadWrite**auf **ReadOnly** umzustellen.  
  
 Mit allen Datenbankvorgängen, mit Ausnahme von **Attach**, wird der aktuelle Status der **ReadWriteMode** -Datenbankeigenschaft beibehalten. Mit Vorgängen wie **Alter**, **Backup**, **Restore**und **Synchronize** wird beispielsweise der **ReadWriteMode** -Wert beibehalten.  
  
> [!NOTE]  
>  Lokale Cubes können aus einer schreibgeschützten Datenbank erstellt werden.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Verschieben einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Detach-Element](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Attach-Element](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  
