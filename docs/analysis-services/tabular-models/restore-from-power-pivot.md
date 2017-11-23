---
title: Wiederherstellen von PowerPivot | Microsoft Docs
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
f1_keywords: sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 88cd0379f0d23f819ab362a273c58bb40db81fa9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="restore-from-power-pivot"></a>Wiederherstellen von PowerPivot
  Sie können die Funktion „Von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] wiederherstellen“ in SQL Server Management Studio verwenden, um eine neue Datenbank für tabellarische Modelle auf einer (im Tabellenmodus ausgeführten) Analysis Services-Instanz zu erstellen oder um eine vorhandene Datenbank aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe (.xlsx) wiederherzustellen.  
  
> [!NOTE]  
>  Die Projektvorlage „Aus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] importieren“ in SQL Server Data Tools verfügt über ähnliche Funktionen. Weitere Informationen finden Sie unter [Importieren aus PowerPivot &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md).  
  
 Folgendes sollte bei Verwendung der Funktion „Von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]wiederherstellen“ beachtet werden:  
  
-   Um die Funktion „Von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]wiederherstellen“ zu verwenden, müssen Sie als Mitglied der Rolle Serveradministrator bei der Analysis Services-Instanz angemeldet sein.  
  
-   Das Dienstkonto der Analysis Services-Instanz muss über Leseberechtigungen für die Arbeitsmappendatei verfügen, aus der Daten wiederhergestellt werden.  
  
-   Wenn Sie eine Datenbank von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]wiederherstellen, ist die Eigenschaft Identitätswechselinformationen der Datenquelle der Datenbank für tabellarische Modelle auf den Standardwert festgelegt, der dem Dienstkonto der Analysis Services-Instanz entspricht. Es wird empfohlen, die Identitätswechsel-Anmeldeinformationen in den Datenbankeigenschaften in ein Windows-Benutzerkonto zu ändern. Weitere Informationen finden Sie unter [Identitätswechsel &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
-   Daten im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenmodell werden in eine vorhandene oder neue Datenbank für tabellarische Modelle auf der Analysis Services-Instanz kopiert. Wenn die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe verknüpfte Tabellen enthält, werden sie ähnlich wie eine Tabelle, die mit In neue Tabelle einfügen erstellt wurde, als Tabelle ohne Datenquelle neu erstellt.  
  
### <a name="to-restore-from-power-pivot"></a>So führen Sie eine Wiederherstellung aus PowerPivot aus  
  
1.  Klicken Sie in SSMS auf der Active Directory-Instanz, auf der die Wiederherstellung erfolgen soll, mit der rechten Maustaste auf **Datenbanken**, und klicken Sie anschließend auf **Von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] wiederherstellen**.  
  
2.  Klicken Sie im Dialogfeld **Von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] wiederherstellen** unter **Wiederherstellungsquelle** in **Sicherungsdatei** auf **Durchsuchen**, und wählen Sie anschließend eine ABF- oder XSLX-Datei aus, aus der Daten wiederhergestellt werden sollen.  
  
3.  Geben Sie in **Datenbank wiederherstellen** unter **Wiederherstellungsziel** den Namen einer neuen oder vorhandenen Datenbank ein. Wenn Sie keinen Namen angeben, wird der Name der Arbeitsmappe verwendet.  
  
4.  Klicken Sie unter **Speicherort**auf **Durchsuchen**, und wählen Sie anschließend einen Ort zum Speichern der Datenbank aus.  
  
5.  Lassen Sie unter **Optionen**das Kontrollkästchen **Sicherheitsinformationen einschließen** aktiviert. Diese Einstellung gilt nicht beim Wiederherstellen von Daten aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellarische Modelldatenbanken &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)   
 [Importieren aus PowerPivot &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)  
  
  
