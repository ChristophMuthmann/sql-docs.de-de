---
title: Sperren und Entsperren von Datenbanken (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2fbc606d5eb93796ef03e62d07be0f70b5d3f807
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="locking-and-unlocking-databases-xmla"></a>Sperren und Entsperren von Datenbanken (XMLA)
  Sperren und Entsperren von Datenbanken verwenden, bzw. die [Sperre](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) und [Unlock](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) -Befehle in XML for Analysis (XMLA). In der Regel sperren und entsperren andere XMLA-Befehle Objekte je nach Bedarf automatisch, um den Befehl während der Ausführung abschließen zu können. Kann explizit sperren oder Entsperren Sie eine Datenbank, um mehrere Befehle innerhalb einer einzelnen Transaktion auszuführen, beispielsweise eine [Batch](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) Befehl, während andere Anwendungen eine Schreibtransaktion in der Datenbank verhindert.  
  
## <a name="locking-databases"></a>Sperren von Datenbanken  
 Der **Lock** -Befehl sperrt die gemeinsame oder exklusive Nutzung eines Objekts im Rahmen der derzeit aktiven Transaktion. Eine Sperre in einem Objekt verhindert, dass ein Commit für Transaktionen ausgeführt wird, bevor die Sperre entfernt wurde. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt zwei Arten von Sperren: gemeinsame Sperren und exklusive Sperren. Weitere Informationen zu den von unterstützten Typen von Sperren [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], finden Sie unter [Mode-Element & #40; XMLA & #41; ](../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ermöglicht nur die Sperrung von Datenbanken. Die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Element muss einen Objektverweis auf enthalten eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank. Wenn das **Object** -Element nicht angegeben ist oder wenn das **Object** -Element auf ein Objekt verweist, bei dem es sich nicht um eine Datenbank handelt, tritt ein Fehler auf.  
  
> [!IMPORTANT]  
>  Nur Datenbankadministratoren oder Serveradministratoren können explizit einen **Lock** -Befehl ausgeben.  
  
 Andere Befehle geben implizit eine **Sperre** Befehl eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank. Jeder Vorgang, Daten oder Metadaten aus einer Datenbank, z. B. alle einliest [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) Methode oder ein [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) externen ausgeführte Methode ein [Anweisung](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) Befehl, gibt implizit eine gemeinsame für die Datenbank zu sperren. Jede Transaktion, die Änderungen an Daten oder Metadaten zu einem Objekt auf ein Commit ausgeführt wird ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank, z. B. ein **Execute** externen ausgeführte Methode ein [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) Befehl, gibt implizit eine exklusive Sperre für die die Datenbank.  
  
## <a name="unlocking-objects"></a>Objekte entsperren  
 Der Befehl **Unlock** entfernt eine innerhalb des Kontexts der gerade aktiven Transaktion begründete Sperre.  
  
> [!IMPORTANT]  
>  Nur Datenbankadministratoren oder Serveradministratoren können explizit einen **Unlock** -Befehl ausgeben.  
  
 Alle Sperren werden im Kontext der aktuellen Transaktion abgehalten. Wenn die aktuelle Transaktion ausgeführt oder für diese ein Rollback durchgeführt wird, werden alle Sperren, die innerhalb der Transaktion definiert sind, automatisch aufgehoben.  
  
## <a name="see-also"></a>Siehe auch  
 [Element sperren &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [Unlock-Element & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
