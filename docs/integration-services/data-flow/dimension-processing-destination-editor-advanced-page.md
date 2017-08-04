---
title: Dimension Ziel-Editor (Seite erweitert) | Microsoft Docs
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
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81e97a5a5e653fb02f0e8a1ccc5741bb3e86acf1
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="dimension-processing-destination-editor-advanced-page"></a>Ziel-Editor für Dimensionsverarbeitung (Seite Erweitert)
  Verwenden Sie zum Konfigurieren der Fehlerbehandlung die Seite **Erweitert** im Dialogfeld **Ziel-Editor für Dimensionsverarbeitung** .  
  
 Weitere Informationen zum Ziel für Dimensionsverarbeitung finden Sie unter [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>enthalten  
 **Standardfehlerkonfiguration verwenden**  
 Gibt an, ob die Standardfehlerbehandlung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet werden soll. Standardmäßig ist dieser Wert **True**.  
  
 **Schlüsselfehleraktion**  
 Gibt an, wie Datensätze behandelt werden, die unzulässige Schlüsselwerte aufweisen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|Konvertiert den unzulässigen Schlüsselwert in den Wert **UnknownMember** .|  
|**DiscardRecord**|Verwirft den Datensatz.|  
  
 **Fehler ignorieren**  
 Gibt an, dass Fehler ignoriert werden sollen.  
  
 **Bei Fehler beenden**  
 Gibt an, dass die Verarbeitung beendet werden soll, wenn ein Fehler auftritt.  
  
 **Anzahl von Fehlern**  
 Gibt den Grenzwert für die Anzahl der Fehler an, bei dem die Verarbeitung beendet werden soll, wenn Sie **Bei Fehler beenden**ausgewählt haben.  
  
 **Aktion bei Fehler**  
 Gibt die Aktion an, die bei Erreichen des Fehlergrenzwertes ausgeführt wird, wenn Sie **Bei Fehler beenden**ausgewählt haben.  
  
|Wert|Description|  
|-----------|-----------------|  
|**StopProcessing**|Beendet die Verarbeitung.|  
|**StopLogging**|Beendet das Protokollieren der Fehler.|  
  
 **Schlüssel nicht gefunden**  
 Gibt die Aktion an, die beim Fehler Schlüssel nicht gefunden ausgeführt werden soll. Standardmäßig ist dieser Wert **ReportAndContinue**.  
  
|Wert|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignoriert den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndContinue**|Berichtet den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndStop**|Berichtet den Fehler, und beendet die Verarbeitung.|  
  
 **Doppelter Schlüssel**  
 Gibt die Aktion an, die beim Fehler Doppelter Schlüssel ausgeführt werden soll. Standardmäßig ist dieser Wert **IgnoreError**.  
  
|Wert|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignoriert den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndContinue**|Berichtet den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndStop**|Berichtet den Fehler, und beendet die Verarbeitung.|  
  
 **NULL-Schlüssel in unbekanntes Element konvertiert**  
 Gibt die Aktion an, die ausgeführt werden soll, wenn ein NULL-Schlüssel in den Wert **UnknownMember** konvertiert wurde. Standardmäßig ist dieser Wert **IgnoreError**.  
  
|Wert|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignoriert den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndContinue**|Berichtet den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndStop**|Berichtet den Fehler, und beendet die Verarbeitung.|  
  
 **NULL-Schlüssel nicht zulässig**  
 Gibt die Aktion an, die ausgeführt wird, wenn NULL-Schlüssel unzulässig sind und ein NULL-Schlüssel entdeckt wurde. Standardmäßig ist dieser Wert **ReportAndContinue**.  
  
|Wert|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignoriert den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndContinue**|Berichtet den Fehler, und setzt die Verarbeitung fort.|  
|**ReportAndStop**|Berichtet den Fehler, und beendet die Verarbeitung.|  
  
 **Fehlerprotokollpfad**  
 Geben Sie den Pfad für das Fehlerprotokoll ein, oder klicken Sie auf die Schaltfläche **Durchsuchen(…)** , um einen Zielpfad festzulegen.  
  
 **Durchsuchen (…)**  
 Wählen Sie einen Pfad für das Fehlerprotokoll aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Ziel-Editor für dimensionsverarbeitung &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/dimension-processing-destination-editor-connection-manager-page.md)   
 [Ziel-Editor für dimensionsverarbeitung &#40; Seite "Zuordnungen" &#41;](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)  
  
  
