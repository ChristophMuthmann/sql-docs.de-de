---
title: SAP BW Quellen-Editor (Seite erweitert) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ac7757987c169f803f3b0adda7f27c94f090d7db
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-source-editor-advanced-page"></a>Quellen-Editor für SAP BW (Seite Erweitert)
  Verwenden Sie die Seite **Erweitert** des **Quellen-Editors für SAP BW** , um die Zeichenkonvertierungsregel und den Timeoutzeitraum anzugeben sowie um den Status einer bestimmten Anforderungs-ID zurückzusetzen.  
  
 Weitere Informationen zur SAP BW-Quellkomponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW finden Sie unter [SAP BW-Quelle](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
> [!IMPORTANT]  
>  Das Extrahieren von Daten aus SAP NetWeaver BW erfordert zusätzliche SAP-Lizenzen. Stimmen Sie diese Anforderungen mit SAP ab.  
  
 **So öffnen Sie die Seite "Verbindungs-Manager"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem die SAP BW-Quelle enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die SAP BW-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für SAP BW**auf **Erweitert** , um die Seite **Erweitert** des Editors zu öffnen.  
  
## <a name="options"></a>enthalten  
  
> [!NOTE]  
>  Wenn Sie nicht alle Werte kennen, die zur Konfiguration der Quelle erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 **Zeichenfolgenkonvertierung**  
 Geben Sie die Regel an, die für die Zeichenfolgenkonvertierung angewendet werden soll.  
  
|Option|Description|  
|------------|-----------------|  
|**Automatische Zeichenfolgenkonvertierung**|Konvertieren Sie alle Zeichenfolgen in **nvarchar** , wenn das SAP NetWeaver BW-System ein Unicode-System ist. Konvertieren Sie andernfalls alle Zeichenfolgen in **varchar**.|  
|**Zeichenfolgen in varchar konvertieren**|Konvertieren Sie alle Zeichenfolgen in **varchar**.|  
|**Zeichenfolgen in nvarchar konvertieren**|Konvertieren Sie alle Zeichenfolgen in **nvarchar**.|  
  
 **Timeout (Sekunden)**  
 Geben Sie die maximale Anzahl von Sekunden an, die die Quelle warten soll.  
  
> [!NOTE]  
>  Diese Option ist nur gültig, wenn Sie auf der Seite **Verbindungs-Manager** des Editors **W – Benachrichtigung abwarten** als Wert für den **Ausführungsmodus** ausgewählt haben. Informationen hierzu finden Sie unter [Quellen-Editor für SAP BW &#40;Seite Verbindungs-Manager&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md).  
  
 **Anforderungs-ID**  
 Geben Sie die Anforderungs-ID an, deren Status Sie auf „G – Grün“ zurücksetzen möchten, wenn Sie auf **Zurücksetzen**klicken.  
  
 **Zurücksetzen**  
 Mit dieser Option können Sie den Status der angegebenen Anforderungs-ID auf G - Grün zurücksetzen, nachdem Ihre Bestätigung angefordert wurde. Dies kann hilfreich sein, wenn ein Problem aufgetreten ist und das SAP NetWeaver BW-System die Anforderung mit einem gelben oder roten Status gekennzeichnet hat.  
  
## <a name="see-also"></a>Siehe auch  
 [Quellen-Editor für SAP BW &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Quellen-Editor für SAP BW &#40; Seite "Spalten" &#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Quellen-Editor für SAP BW &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

