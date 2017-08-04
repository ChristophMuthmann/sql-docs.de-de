---
title: ODBC-Ziel-Editor (Seite Fehlerausgabe) | Microsoft Docs
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
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e0fa59290399f3c3f7fc42b1f74b6a42c573f7d2
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-destination-editor-error-output-page"></a>Ziel-Editor für ODBC (Seite "Fehlerausgabe")
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Ziel-Editor für ODBC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
 Weitere Informationen zum ODBC-Ziel finden Sie unter [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **So öffnen Sie die Seite "Fehlerausgabe" des Ziel-Editors für ODBC**  
  
## <a name="task-list"></a>Aufgabenliste  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das das ODBC-Ziel enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ODBC-Ziel.  
  
-   Klicken Sie im **Ziel-Editor für ODBC**auf **Fehlerausgabe**.  
  
## <a name="options"></a>enthalten  
  
### <a name="inputoutput"></a>Eingabe/Ausgabe  
 Zeigt den Namen der Datenquelle an.  
  
### <a name="column"></a>Column  
 Wird nicht verwendet.  
  
### <a name="error"></a>Fehler  
 Wählen Sie aus, wie das ODBC-Ziel Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### <a name="truncation"></a>Abschneiden  
 Wählen Sie aus, wie das ODBC-Ziel Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### <a name="description"></a>Description  
 Zeigt eine Beschreibung des Fehlers an.  
  
### <a name="set-this-value-to-selected-cells"></a>Diesen Wert für ausgewählte Zellen festlegen  
 Wählen Sie aus, wie das ODBC-Ziel im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### <a name="apply"></a>Anwenden  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
## <a name="error-handling-options"></a>Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie das ODBC-Ziel Fehler und Kürzungen behandelt.  
  
### <a name="fail-component"></a>Fehler bei Komponente  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
### <a name="ignore-failure"></a>Fehler ignorieren  
 Der Fehler oder die Kürzung wird ignoriert.  
  
### <a name="redirect-flow"></a>Zeile umleiten  
 Die Zeile, die den Fehler oder die Kürzung verursacht, wird an die Fehlerausgabe des ODBC-Ziels umgeleitet. Weitere Informationen finden Sie unter "ODBC-Ziel".  
  
## <a name="see-also"></a>Siehe auch  
 [Ziel-Editor für ODBC &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [Ziel-Editor für ODBC &#40; Seite "Zuordnungen" &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  
