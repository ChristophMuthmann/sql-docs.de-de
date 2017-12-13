---
title: Feature Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQMSupportEnabled property
- ComUdfEnabled property
- LinkToOtherInstanceEnabled property
- ManagedCodeEnabled property
- ConnStringEncryptionEnabled property
- LinkFromOtherInstanceEnabled property
- LinkInsideInstanceEnabled property
- UseCachedPageAllocators property
ms.assetid: a34d046a-6562-4d98-b827-37cebc6d77b4
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5c78b965e827ad4b355563c7c698db2b8f063c78
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="feature-properties"></a>Funktionseigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Funktionseigenschaften beziehen sich auf Produktfunktionen, die meisten sind erweiterte Eigenschaften zum Steuern der Verbindungen zwischen Serverinstanzen.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt die in der folgenden Tabelle aufgeführten Servereigenschaften. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** Nur mehrdimensionaler Servermodus  
  
## <a name="properties"></a>Eigenschaften  
  
|Eigenschaft|Standardwert|Description|  
|--------------|-------------|-----------------|  
|**ManagedCodeEnabled**|1|Eine boolesche Eigenschaft, die anzeigt, ob CLR-gespeicherte Prozeduren aktiviert sind.|  
|**LinkInsideInstanceEnabled**|1|Eine boolesche Eigenschaft, die anzeigt, ob innerhalb derselben Serverinstanz ein verknüpftes Objekt erstellt werden kann.|  
|**LinkToOtherInstanceEnabled**|0|Eine boolesche Eigenschaft, die anzeigt, ob ein Link mit Objekten auf Remoteservern möglich ist.|  
|**LinkFromOtherInstanceEnabled**|0|Eine boolesche Eigenschaft, die anzeigt, ob von anderen Serverinstanzen aus ein Link mit Objekten möglich ist.|  
|**ConnStringEncryptionEnabled**|1|Eine boolesche Eigenschaft, die anzeigt, ob die Verbindungszeichenfolge in der Serverkonfigurationsdatei verschlüsselt wird.|  
|**UseCachedPageAllocators**|0|Eine boolesche Eigenschaft, die anzeigt, ob zwischengespeicherte Seitenzuordnungen aktiviert sind.|  
|**ComUdfEnabled**|0|Eine boolesche Eigenschaft, die angibt, ob benutzerdefinierte Funktionen, die als COM-Objekte definiert sind, aktiviert sind.|  
|**SQMSupportEnabled**|1|Eine boolesche Eigenschaft, die anzeigt, ob Fehler- und Funktionsverwendungsberichte automatisch an [!INCLUDE[msCoName](../../includes/msconame-md.md)] gesendet werden.|  
|**ResourceMonitoringEnabled**|1|Eine boolesche Eigenschaft, die angibt, ob Leistungsindikatoren für interne Ressourcen aktiviert sind. Diese Eigenschaft ist standardmäßig aktiviert. Wenn sie aktiviert ist, können Leistungsindikatoren Verwendungsdaten zu CPU, Arbeitsspeicher und E/A-Aktivität erfassen.<br /><br /> Leistungsindikatoren für interne Ressourcen werden von dynamischen Verwaltungssichten (DMV) verwendet, die die Ressourcennutzung protokollieren. Wenn Sie diese Eigenschaft deaktivieren, werden die DMV-Abfragen zwar immer noch ausgeführt, aber das Resultset ist ungültig. DMVs, die von dieser Eigenschaft abhängig sind, schließen Folgendes ein:<br /><br /> **DISCOVER_OBJECT_ACTIVITY**<br /><br /> **DISCOVER_COMMAND_OBJECTS**<br /><br /> **DISCOVER_SESSIONS** (für SESSION_READS, SESSION_WRITES, SESSION_CPU_TIME_MS)<br /><br /> <br /><br /> Hinweis: Auf einem Multikern-System mit NUMA-Architektur kann durch Deaktivieren dieser Eigenschaft die Abfrageleistung verbessert werden, insbesondere für hohe Mehrbenutzerarbeitsauslastungen. Sie müssen Vergleichstests ausführen, um zu bestimmen, ob die Abfrageleistung durch Ändern dieser Eigenschaft verbessert wird. Best Practices zum Ausführen von Vergleichstests, einschließlich des Löschens des Caches und des Vermeidens von häufigen Fehlern, finden Sie im [SQL Server 2008 R2 Analysis Services-Vorgangshandbuch](http://go.microsoft.com/fwlink/?LinkID=225539).|  
  
## <a name="see-also"></a>Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Verwenden von dynamischen Verwaltungssichten &#40;DMVs&#41; zum Überwachen von Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
