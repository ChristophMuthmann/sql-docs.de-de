---
title: "Optionen für Verlaufsattribute fest (von langsam veränderlichen Dimensions-Assistent) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2867e5173235520c521ca70952f50d1fa7bc8487
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>Optionen für Verlaufsattribute (Assistent für langsam veränderliche Dimensionen)
  Mithilfe des Dialogfelds **Optionen für Verlaufsattribute** können Sie Verlaufsattribute nach Anfangs- und Enddatum anzeigen oder sie in einer speziell zu diesem Zweck erstellten Spalte aufzeichnen.  
  
 Weitere Informationen zu diesem Assistenten finden Sie unter [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>enthalten  
 **Einzelne Spalte zum Anzeigen der aktuellen und abgelaufenen Datensätze verwenden**  
 Wenn Sie eine einzelne Spalte für zum Aufzeichnen des Status von Verlaufsattributen verwenden, sind folgende Optionen verfügbar:  
  
|Option|Description|  
|------------|-----------------|  
|**Spalte mit Indikator für aktuellen Datensatz**|Wählen Sie eine Spalte aus, in der der aktuelle Datensatz angezeigt werden soll.|  
|**Wert, wenn aktuell**|Verwenden Sie entweder **True** oder **Current** , um anzuzeigen, dass der Datensatz aktuell ist.|  
|**Wert, wenn abgelaufen**|Verwenden Sie entweder **False** oder **Abgelaufen** , um anzuzeigen, dass der Datensatz ein abgelaufener Wert ist.|  
  
 **Start- und Enddatum zum Identifizieren aktueller und abgelaufener Datensätze verwenden**  
 Die Dimensionstabelle für diese Option muss eine Datumsspalte enthalten. Wenn Sie die Verlaufsattribute nach Start- und Enddatum anzeigen, sind folgende Optionen verfügbar:  
  
|Option|Description|  
|------------|-----------------|  
|**Spalte mit Startdatum**|Wählen Sie die Spalte in der Dimensionstabelle aus, die das Startdatum enthalten soll.|  
|**Spalte mit Enddatum**|Wählen Sie die Spalte in der Dimensionstabelle aus, die das Enddatum enthalten soll.|  
|**Variable zum Festlegen von Datumswerten**|Wählen Sie eine Variable für die Datumswerte aus der Liste aus.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  

