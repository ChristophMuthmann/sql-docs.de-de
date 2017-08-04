---
title: "Quellen-Editor (Spaltenseite) für Flatfiles | Microsoft Docs"
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
- sql13.dts.designer.flatfilesourceadapter.columns.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a34e304d72b80412f5527dcb75f00b6dcb2fcbb2
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-source-editor-columns-page"></a>Quellen-Editor für Flatfiles (Seite Spalten)
  Mithilfe des Knotens **Spalten** des Dialogfelds **Quellen-Editor für Flatfiles** können Sie jeder externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
> [!NOTE]  
>  Die **FileNameColumnName** -Eigenschaft der Flatfilequelle und die **FastParse** -Eigenschaft ihrer Ausgabespalten sind nicht im **Quellen-Editor für Flatfiles**verfügbar, sie können jedoch mithilfe des Dialogfelds **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Flatfilequelle von [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Weitere Informationen zur Flatfilequelle finden Sie unter [Flat File Source](../../integration-services/data-flow/flat-file-source.md).  
  
## <a name="options"></a>enthalten  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der Reihenfolge an, in der sie von dem Task gelesen werden. Sie können die Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der Tabelle löschen. Wählen Sie anschließend die externen Spalten in einer anderen Reihenfolge aus der Liste aus.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Quellen-Editor für Flatfiles &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/flat-file-source-editor-connection-manager-page.md)   
 [Quellen-Editor für Flatfiles &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/flat-file-source-editor-error-output-page.md)   
 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
