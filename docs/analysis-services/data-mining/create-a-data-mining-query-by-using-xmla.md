---
title: Erstellen Sie eine Datamining-Abfrage mithilfe von XMLA | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8732b3f366d5805f6321b4e07fe0de1dbc73fb42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>Erstellen einer Data Mining-Abfrage mit XMLA
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Abfragen für Data Mining-Objekte können Sie mithilfe von AMO, DMX oder XML/A erstellen.  
  
 XML wird für die Kommunikation zwischen dem Analysis Services-Server und allen Clients benötigt. Obwohl Inhaltsabfragen im Allgemeinen einfacher mit DMX erstellt werden können, können Sie Abfragen mit der DISCOVER- und der COMMAND-Anweisung in XML/A schreiben, indem Sie entweder einen Client verwenden, der das SOAP-Protokoll unterstützt, oder indem Sie eine XML/A-Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen.  
  
 In diesem Thema wird beschrieben, wie Sie mit in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügbaren XML/A-Vorlagen eine Modellinhaltsabfrage für ein Miningmodell erstellen, das auf dem aktuellen Server gespeichert ist.  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>Abfragen der Data Mining-Schemarowsets mit XML/A  
  
#### <a name="to-open-an-xmla-template"></a>So öffnen Sie eine XML/A-Vorlage  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Ansicht** auf **Vorlagen-Explorer**.  
  
2.  Klicken Sie auf das Cubesymbol, um die Liste mit den Analysis-Services-Vorlagen zu öffnen.  
  
3.  Erweitern Sie in der Liste der Vorlagenkategorien den Eintrag **XMLA**, erweitern Sie **Schemarowsets**, und doppelklicken Sie auf **Discover Schema Rowsets** , um die Vorlage im zugehörigen Code-Editor zu öffnen.  
  
4.  Vervollständigen Sie im Dialogfeld **Verbindung mit Analysis Services herstellen** die Verbindungseinstellungen, und klicken Sie dann auf **Verbinden**. Ein neues Fenster des Abfrage-Editors wird mit der Vorlage **Discover Schema Rowsets** geöffnet.  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>So ermitteln Sie Spaltennamen aus dem MINING MODEL CONTENT-Schemarowset  
  
1.  Klicken Sie bei geöffneter **Discover Schema Rowsets** -Vorlage auf **Ausführen**.  
  
     Eine Liste der Schemarowsets wird im Fenster **Ergebnisse** zurückgegeben. Diese Liste enthält die Rowsetnamen und Rowsetspalten für alle in der aktuellen Instanz verfügbaren Rowsets.  
  
2.  In der **Abfrage** Bereich, platzieren Sie den Cursor nach  **\<Einschränkungsliste >** , und drücken Sie EINGABETASTE, um eine neue Zeile hinzuzufügen.  
  
3.  Platzieren Sie den Cursor auf die leere Zeile, und geben  **\<SchemaName > DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName >**  
  
     Der vollständige Abschnitt für Einschränkungen sollte wie folgt angezeigt werden:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  Klicken Sie auf **Ausführen**.  
  
     Im Fenster **Ergebnisse** wird eine Liste der Spaltennamen für das angegebene Schemarowset angezeigt.  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>So erstellen Sie eine Inhaltsabfrage mit dem MINING MODEL CONTENT-Schemarowset  
  
1.  Ändern Sie in der Vorlage **Discover Schema Rowsets** den Anforderungstyp, indem Sie den Text innerhalb der Tags für den Anforderungstyp ersetzen.  
  
     Ersetzen Sie die Zeile:  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     mit der folgenden Zeile:  
  
     **\<RequestType > DMSCHEMA_MINING_MODEL_CONTENT\</RequestType >**  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodellinhalt & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Datamining-Schemarowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
