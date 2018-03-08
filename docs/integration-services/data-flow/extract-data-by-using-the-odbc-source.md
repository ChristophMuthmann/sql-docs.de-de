---
title: Extrahieren von Daten mithilfe der ODBC-Quelle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83e5422eca9042594ab5234e84d9a9d5da3c2aa2
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="extract-data-by-using-the-odbc-source"></a>Extrahieren von Daten mithilfe der ODBC-Quelle
  In diesem Verfahren wird beschrieben, wie Sie Daten mithilfe einer ODBC-Quelle extrahieren. Um eine ODBC-Quelle hinzuzufügen und zu konfigurieren, muss das Paket bereits mindestens einen Datenflusstask enthalten.  
  
### <a name="to-extract-data-using-an-odbc-source"></a>So extrahieren Sie Daten mithilfe einer ODBC-Quelle  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das gewünschte [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket.  
  
2.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie die ODBC-Quelle dann aus der **Toolbox**auf die Entwurfsoberfläche.  
  
3.  Doppelklicken Sie auf die ODBC-Quelle.  
  
4.  Wählen Sie im Dialogfeld **Quellen-Editor für ODBC** auf der Seite **Verbindungs-Manager** einen vorhandenen ODBC-Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen.  
  
5.  Wählen Sie die Datenzugriffsmethode aus.  
  
    -   **Tabellenname**: Wählen Sie in der Datenbank eine Tabelle oder Sicht aus, oder geben Sie einen regulären Ausdruck ein, um die Tabelle zu identifizieren, mit der der ODBC-Verbindungs-Manager eine Verbindung herstellt.  
  
         Diese Liste enthält nur die ersten 1000 Tabellen. Wenn die Datenbank mehr als 1000 Tabellen enthält, können Sie den Anfang eines Tabellennamens eingeben oder das Platzhalterzeichen (*) verwenden, um einen beliebigen Teil des Namens einzugeben und die gewünschten Tabellen anzuzeigen.  
  
    -   **SQL-Befehl**: Geben Sie einen SQL-Befehl ein, oder klicken Sie auf **Durchsuchen** , um die SQL-Abfrage aus einer Textdatei zu laden.  
  
6.  Sie können auf **Vorschau** klicken, um bis zu 200 Datenzeilen anzuzeigen, die von der ODBC-Quelle extrahiert werden.  
  
7.  Um die Zuordnung zwischen externen Spalten und Ausgabespalten zu aktualisieren, klicken Sie auf **Spalten** und wählen in der Liste **Externe Spalte** verschiedene Spalten aus.  
  
8.  Aktualisieren Sie bei Bedarf die Namen von Ausgabespalten, indem Sie Werte in der Liste **Ausgabespalte** bearbeiten.  
  
9. Klicken Sie auf **Fehlerausgabe**, um die Fehlerausgabe zu konfigurieren.  
  
10. Klicken Sie auf **OK**.  
  
11. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Quellen-Editor für ODBC &#40;Seite Verbindungs-Manager&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Quellen-Editor für ODBC &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)   
 [Quellen-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  
