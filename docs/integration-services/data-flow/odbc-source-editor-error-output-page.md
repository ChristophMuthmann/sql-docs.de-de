---
title: "Quellen-Editor für ODBC (Seite Fehlerausgabe) | Microsoft Docs"
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
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 86f1fa7d2408fe43f5f76a3d5470f9eb295145d6
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-source-editor-error-output-page"></a>Quellen-Editor für ODBC (Seite Fehlerausgabe)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für ODBC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
 Weitere Informationen zur ODBC-Quelle finden Sie unter [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Fehlerausgabe" des Quellen-Editors für ODBC**  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die ODBC-Quelle enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ODBC-Quelle.  
  
-   Klicken Sie im **Quellen-Editor für ODBC**auf **Fehlerausgabe**.  
  
## <a name="options"></a>enthalten  
  
### <a name="inputoutput"></a>Eingabe/Ausgabe  
 Zeigt den Namen der Datenquelle an.  
  
### <a name="column"></a>Column  
 Wird nicht verwendet.  
  
### <a name="error"></a>Fehler  
 Wählen Sie aus, wie die ODBC-Quelle Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### <a name="truncation"></a>Abschneiden  
 Wählen Sie aus, wie die ODBC-Quelle Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### <a name="description"></a>Description  
 Wird nicht verwendet.  
  
### <a name="set-this-value-to-selected-cells"></a>Diesen Wert für ausgewählte Zellen festlegen  
 Wählen Sie aus, wie die ODBC-Quelle im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### <a name="apply"></a>Anwenden  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
## <a name="error-handling-options"></a>Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie die ODBC-Quelle Fehler und Kürzungen behandelt.  
  
### <a name="fail-component"></a>Fehler bei Komponente  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
### <a name="ignore-failure"></a>Fehler ignorieren  
 Der Fehler oder die Kürzung wird ignoriert.  
  
### <a name="redirect-flow"></a>Zeile umleiten  
 Die Zeile, die den Fehler oder die Kürzung verursacht, wird an die Fehlerausgabe der ODBC-Quelle umgeleitet. Weitere Informationen finden Sie unter [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Quellen-Editor für ODBC &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Quellen-Editor für ODBC &#40; Seite "Spalten" &#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
  
