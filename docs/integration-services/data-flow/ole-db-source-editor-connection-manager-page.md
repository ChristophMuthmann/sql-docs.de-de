---
title: "Quellen-Editor f&#252;r OLE DB (Seite Verbindungs-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbsourceadapter.connection.f1"
helpviewer_keywords: 
  - "Quellen-Editor für OLE DB"
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Quellen-Editor f&#252;r OLE DB (Seite Verbindungs-Manager)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Quellen-Editor für OLE DB** wählen Sie den OLE DB-Verbindungs-Manager für die Quelle aus. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
> [!NOTE]  
>  Verwenden Sie zum Laden von Daten aus einer Datenquelle, für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 verwendet wird, eine OLE DB-Quelle. Sie können eine Excel-Quelle nicht zum Laden von Daten aus einer Excel 2007-Datenquelle verwenden. Weitere Informationen finden Sie unter [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Verwenden Sie zum Laden von Daten aus einer Datenquelle, für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 oder eine frühere Version verwendet wird, eine Excel-Quelle. Weitere Informationen finden Sie unter [Quellen-Editor für Excel &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft der OLE DB-Quelle ist nicht im **Quellen-Editor für OLE DB**verfügbar, sie kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt Excel-Quelle von [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
 Weitere Informationen zur OLE DB-Quelle finden Sie unter [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
## Öffnen des Quellen-Editors für OLE DB (Seite "Verbindungs-Manager")  
  
1.  Fügen Sie die OLE DB-Quelle dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]hinzu.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Quellkomponente, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Verbindungs-Manager**.  
  
## Statische Optionen  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Description|  
|------------|-----------------|  
|Tabelle oder Sicht|Rufen Sie Daten aus einer Tabelle oder Sicht in der OLE DB-Datenquelle ab.|  
|Variable für Tabellenname oder Sichtname|Gibt den Namen der Tabelle oder Sicht in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md)|  
|SQL-Befehl|Rufen Sie mit SQL-Abfrage Daten aus der OLE DB-Datenquelle ab.|  
|SQL-Befehl aus Variable|Gibt den SQL-Abfragetext in einer Variablen an.|  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der**Vorschau** können bis zu 200 Zeilen angezeigt werden.  
  
> [!NOTE]  
>  In der Datenvorschau enthalten Spalten mit einem CLR-benutzerdefinierten Typ keine Daten. Stattdessen werden die Werte \<Wert zu groß zum Anzeigen> oder System.Byte[] angezeigt. Der erste Wert wird angezeigt, wenn mithilfe des SQL-OLE DB-Anbieters auf die Datenquelle zugegriffen wird. Der zweite Wert wird bei Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieters angezeigt.  
  
## Dynamische Optionen (Datenzugriffsmodus)  
  
### Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Tabelle oder Sicht**  
 Wählen Sie den Namen der Tabelle oder Sicht aus einer Liste der verfügbaren Namen in der Datenquelle aus.  
  
### Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen der Tabelle oder Sicht enthält.  
  
### Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text einer SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen** klicken. Wahlweise können Sie auch nach der Datei suchen, die den Abfragetext enthält, indem Sie auf **Durchsuchen** klicken.  
  
 **Parameter**  
 Wenn Sie eine parametrisierte Abfrage eingeben und im Abfragetext ? als Parameterplatzhalter verwenden, können Sie den Paketvariablen mithilfe des Dialogfelds **Abfrageparameter festlegen** Abfrageeingabeparameter zuordnen.  
  
 **Abfrage erstellen**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
### Datenzugriffsmodus = SQL-Befehl aus Variable  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Text für die SQL-Abfrage enthält.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Quellen-Editor für OLE DB &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)   
 [Quellen-Editor für OLE DB &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)   
 [Extrahieren von Daten mithilfe der OLE DB-Quelle](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)   
 [OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  