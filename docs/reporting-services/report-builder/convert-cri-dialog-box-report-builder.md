---
title: Konvertieren des CRI Dialogfelds (Berichts-Generator) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f532d0e554e85c7e302f3c8f9e61130179d51483
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="convert-cri-dialog-box-report-builder"></a>CRI konvertieren (Dialogfeld) (Berichts-Generator)
  Dieser Bericht enthält benutzerdefinierte Berichtselemente (Custom Report Item, CRI) mit nicht unterstützten Funktionen. CRIs sind Erweiterungen der Berichtsdefinitionssprache (Report Definition Language, RDL) zur Unterstützung benutzerdefinierter Objekte, die Daten in einem Bericht anzeigen. CRIs umfassen Entwurfszeit- und Laufzeitkomponenten, die von Drittanbietern bereitgestellt werden.  
  
> [!NOTE]  
>  Die Entscheidung, benutzerdefinierte Berichtselemente auf einem Berichtsserver zuzulassen, wird vom Systemadministrator getroffen. Zum Anzeigen von CRIs in einem Bericht müssen die CRI-Komponenten auf dem Berichterstellungsserver installiert sein, um einen Bericht als Vorschau anzuzeigen, und auf dem Berichtsserver, um einen veröffentlichten oder hochgeladenen Bericht anzuzeigen.  
  
 Einige CRIs können im neuen Berichtsdefinitionsformat in Berichtselemente konvertiert werden. Sie werden beim Öffnen des Berichts gefragt, ob Sie ein Upgrade durchführen möchten. Entscheiden Sie anhand der folgenden Informationen, ob die CRIs in diesem Bericht konvertiert werden sollen:  
  
-   **Ja** Wählen Sie **Ja** aus, um nach Möglichkeit alle CRIs im Bericht zu konvertieren. Nicht unterstützte Funktionen in den CRIs können nicht aktualisiert werden und werden aus der Berichtsdefinitionsdatei entfernt. Die Liste der nicht unterstützten Funktionen finden Sie unter [Upgraden von Berichten](../../reporting-services/install-windows/upgrade-reports.md). Bei der Anzeige des Berichts werden möglicherweise Unterschiede in der Darstellung der CRIs im Bericht deutlich.  
  
-   **Nein** Wählen Sie **Nein** aus, wenn die CRIs im Bericht nicht konvertiert werden sollen. Diese CRIs können vom Berichtsprozessor nicht in ihrer aktuellen Version angezeigt werden. Wenn der Systemadministrator die Installation einer neuen CRI-Version von einem Softwaredrittanbieter plant, die mit dem neuen Berichtsdefinitionsformat kompatibel ist, sollten Sie **Nein**auswählen. Bis neue Versionen zur Verfügung stehen, werden die CRIs im Bericht als leere Textfelder mit einem roten X dargestellt.  
  
 In beiden Fällen wird der Bericht auf das neue Berichtsdefinitionsformat aktualisiert, und eine Sicherungskopie des ursprünglichen Berichts wird als „*\<Berichtsname>* `-` Backup.rdl“ gespeichert. Wenn Sie den Bericht im Berichterstellungstool speichern, wird der aktualisierte Bericht im neuen Berichtsdefinitionsformat gespeichert. Beim Veröffentlichen des Berichts wird dieser zuerst auf Ihrem Computer gespeichert und dann auf dem Berichtsserver veröffentlicht. Sie veröffentlichen die aktualisierte Version des Berichts auf dem Berichtsserver.  
  
 Wenn Sie den Bericht nicht speichern, bleibt der ursprüngliche Bericht unverändert. Sie können diesen Bericht jedoch nicht in der [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - oder höheren Version von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder in einer Berichterstellungsumgebung bearbeiten, für die dieses Berichterstellungsformat verwendet wird. Die ursprüngliche Version des Berichts kann weiterhin ausgeführt werden, indem Sie diese im Berichts-Manager auf einen [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver hochladen. Weitere Informationen finden Sie unter [Hochladen einer Datei oder eines Berichts &#40;Berichts-Manager&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
 Bei Berichten, die Sie hochladen, statt sie auf einem Berichtsserver zu veröffentlichen, bestimmt der Berichtsprozessor, ob der Bericht bei der ersten Verwendung aktualisiert werden kann. Berichte, die nicht aktualisiert werden können, werden im Abwärtskompatibilitätsmodus verarbeitet und weiterhin wie in der früheren Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]angezeigt. Weitere Informationen finden Sie unter [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
 Informationen zum Ermitteln des aktuellen Berichtsdefinitionsformats für einen Bericht, einen Berichtsserver oder die Berichterstellungsumgebung finden Sie unter [Suchen der Berichtsdefinitions-Schemaversion (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Hilfe zu Dialogfeldern, Bereichen und Assistenten in Berichts-Generator](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)  
  
  
