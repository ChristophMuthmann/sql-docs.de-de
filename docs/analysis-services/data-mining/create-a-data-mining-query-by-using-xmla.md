---
title: "Erstellen einer Data Mining-Abfrage mit XMLA | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Inhaltsabfragen [DMX]"
ms.assetid: 8f6b6008-006c-4792-9bd1-64c30dc3fd41
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 11
---
# Erstellen einer Data Mining-Abfrage mit XMLA
  Abfragen für Data Mining-Objekte können Sie mithilfe von AMO, DMX oder XML/A erstellen.  
  
 XML wird für die Kommunikation zwischen dem Analysis Services-Server und allen Clients benötigt. Obwohl Inhaltsabfragen im Allgemeinen einfacher mit DMX erstellt werden können, können Sie Abfragen mit der DISCOVER- und der COMMAND-Anweisung in XML/A schreiben, indem Sie entweder einen Client verwenden, der das SOAP-Protokoll unterstützt, oder indem Sie eine XML/A-Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen.  
  
 In diesem Thema wird beschrieben, wie Sie mit in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügbaren XML/A-Vorlagen eine Modellinhaltsabfrage für ein Miningmodell erstellen, das auf dem aktuellen Server gespeichert ist.  
  
## Abfragen der Data Mining-Schemarowsets mit XML/A  
  
#### So öffnen Sie eine XML/A-Vorlage  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Ansicht** auf **Vorlagen-Explorer**.  
  
2.  Klicken Sie auf das Cubesymbol, um die Liste mit den Analysis-Services-Vorlagen zu öffnen.  
  
3.  Erweitern Sie in der Liste der Vorlagenkategorien den Eintrag **XMLA**, erweitern Sie **Schemarowsets**, und doppelklicken Sie auf **Discover Schema Rowsets**, um die Vorlage im zugehörigen Code-Editor zu öffnen.  
  
4.  Vervollständigen Sie im Dialogfeld **Verbindung mit Analysis Services herstellen** die Verbindungseinstellungen, und klicken Sie dann auf **Verbinden**. Ein neues Fenster des Abfrage-Editors wird mit der Vorlage **Discover Schema Rowsets** geöffnet.  
  
#### So ermitteln Sie Spaltennamen aus dem MINING MODEL CONTENT-Schemarowset  
  
1.  Klicken Sie bei geöffneter **Discover Schema Rowsets** -Vorlage auf **Ausführen**.  
  
     Eine Liste der Schemarowsets wird im Fenster **Ergebnisse** zurückgegeben. Diese Liste enthält die Rowsetnamen und Rowsetspalten für alle in der aktuellen Instanz verfügbaren Rowsets.  
  
2.  Positionieren Sie den Cursor im Fenster **Abfrage** hinter **\<Restriction List>**, und drücken Sie die EINGABETASTE, um eine neue Zeile hinzuzufügen.  
  
3.  Setzen Sie den Cursor auf die leere Zeile, und geben Sie **\<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName>** ein.  
  
     Der vollständige Abschnitt für Einschränkungen sollte wie folgt angezeigt werden:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  Klicken Sie auf **Ausführen**.  
  
     Im Fenster **Ergebnisse** wird eine Liste der Spaltennamen für das angegebene Schemarowset angezeigt.  
  
#### So erstellen Sie eine Inhaltsabfrage mit dem MINING MODEL CONTENT-Schemarowset  
  
1.  Ändern Sie in der Vorlage **Discover Schema Rowsets** den Anforderungstyp, indem Sie den Text innerhalb der Tags für den Anforderungstyp ersetzen.  
  
     Ersetzen Sie die Zeile:  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     mit der folgenden Zeile:  
  
     **\<RequestType>DMSCHEMA_MINING_MODEL_CONTENT\</RequestType>**  
  
2.  Ändern Sie die Einschränkungsliste, um ein Miningmodell mit Namen anzugeben, indem Sie eine neue Bedingung zu den Einschränkungslisten hinzufügen.  
  
3.  Positionieren Sie den Cursor in der Vorlage hinter `<Restriction List>` , und drücken Sie die Eingabetaste, um eine neue Zeile hinzuzufügen.  
  
4.  Setzen Sie den Cursor in die leere Zeile, und geben Sie **<MODEL_NAME>My model name</MODEL_NAME>** ein.  
  
     Der vollständige Abschnitt für Einschränkungen sollte wie folgt angezeigt werden:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  Klicken Sie auf **Ausführen**.  
  
     Im Ergebnisbereich wird die Schemadefinition zusammen mit den Werten für das angegebene Modell angezeigt.  
  
## Siehe auch  
 [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Data Mining-Schemarowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  