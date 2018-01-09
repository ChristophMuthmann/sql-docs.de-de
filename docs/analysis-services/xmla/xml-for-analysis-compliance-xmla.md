---
title: "XML for Analysis-Kompatibilität (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: efd2d4cfd7adb6185abdd383a261494495817ec5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="xml-for-analysis-compliance-xmla"></a>XML for Analysis-Kompatibilität (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]XML for Analysis 1.1-Spezifikation beschreibt einen offenen Standard, der den Datenzugriff auf Datenquellen im World Wide Web unterstützt. In diesem Thema detailliert den Grad der Kompatibilität mit der XML for Analysis 1.1-Spezifikation, die vom unterstützt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="compliant-items"></a>Kompatible Elemente  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist mit allen verbindlichen Elementen, die in der XML for Analysis 1.1-Spezifikation aufgelistet sind, kompatibel. Außerdem implementiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das folgende optionale Element, das in der XML for Analysis 1.1-Spezifikation beschrieben ist.  
  
|Element|Spezifikation|Implementierung|  
|----------|-------------------|--------------------|  
|Session Support|Die SOAP-Headerelemente, die im Abschnitt "Support for Statefulness in XML for Analysis" der XML for Analysis 1.1-Spezifikation aufgelistet werden.|Alle aufgelisteten SOAP-Header-Elemente werden gemäß der Spezifikation von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt.|  
  
## <a name="extensions"></a>Erweiterungen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verlängert außerdem die XML for Analysis 1.1-Spezifikation, um die folgenden weiteren Funktionen und Fähigkeiten zu unterstützen.  
  
|Element|Spezifikation|Implementierung|  
|----------|-------------------|--------------------|  
|Protokollaushandlung|Die XML for Analysis 1.1-Spezifikation enthält keine Informationen.|ProtocolCapabilities-Header-Element hinzugefügt, indem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Aushandlung von Protokollfunktionen zu unterstützen.|  
|XML for Analysis-Befehle (XMLA) werden von der Discover-Methode unterstützt.|Die folgenden Befehle werden von der XML for Analysis 1.1-Spezifikation unterstützt:<br /><br /> [Statement-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Die folgenden Befehle werden von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt:<br /><br /> [Alter-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [Backup-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [Batch-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Cancel-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [Erstellen Sie-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [Löschen Sie-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Drop-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [INSERT-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Lock-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [MergePartitions-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Process-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restore-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Statement-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Subscribe-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [Synchronisieren Sie-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [Unlock-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Update-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|Spaltenfehler in tabellarischen Rowsets|Nicht in der XML for Analysis 1.1-Spezifikation aufgelistet.|Die [Fehler](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) Element dient der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] um Fehler in Spaltenelementen, die einem [Zeile](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) Element.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Referenz &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
