---
title: Abbrechen von Befehlen (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e74ce7bd5b03aa84b6c6580342504148a62a68bf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="canceling-commands-xmla"></a>Abbrechen von Befehlen (XMLA)
  Abhängigkeit von den Administrationsberechtigungen des Benutzers, der den Befehl ausgibt die ["Abbrechen"](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) -Befehl in XML for Analysis (XMLA) einen Befehl, die sich auf eine Sitzung, eine Sitzung, eine Verbindung, einem Serverprozess oder einer zugeordneten Sitzung abbrechen können oder Verbindung.  
  
## <a name="canceling-commands"></a>Abbrechen von Befehlen  
 Ein Benutzer kann den zurzeit ausgeführten Befehl innerhalb des Kontexts der aktuellen expliziten Sitzung abbrechen, indem Sie senden eine **"Abbrechen"** -Befehl ohne festgelegte Eigenschaften.  
  
> [!NOTE]  
>  Ein Befehl, der in einer impliziten Sitzung ausgeführt wird, kann von einem Benutzer nicht abgebrochen werden.  
  
### <a name="canceling-batch-commands"></a>Abbrechen von Batch-Befehlen  
 Wenn ein Benutzer den Vorgang abbricht eine **Batch** Befehl, und klicken Sie dann auf alle verbleibenden Befehle, die noch nicht ausgeführten innerhalb der **Batch** Befehl abgebrochen werden. Wenn die **Batch** -Befehl transaktional war, werden alle Befehle, die ausgeführt wurden, bevor die **"Abbrechen"** Befehl führt ein Rollback.  
  
## <a name="canceling-sessions"></a>Abbrechen von Sitzungen  
 Durch Angabe einer Sitzungs-ID für eine explizite Sitzung in der [SessionID](../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md) Eigenschaft von der **"Abbrechen"** Befehl, ein Datenbank- oder Serveradministrator eine Sitzung abbrechen, einschließlich der derzeit ausgeführten Befehl. Ein Datenbankadministrator kann nur Sitzungen für Datenbanken abbrechen, für die er über Administratorberechtigungen verfügt.  
  
 Ein Datenbankadministrator kann die aktiven Sitzungen für eine festgelegte Datenbank abrufen, indem er das DISCOVER_SESSIONS-Schemarowset abruft. Zum Abrufen des DISCOVER_SESSIONS-Schemarowsets verwendet der Datenbankadministrator die XMLA **Discover** Methode und gibt den entsprechenden Datenbankbezeichner an für die Einschränkungsspalte session_current_database in der [Einschränkungen](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md) Eigenschaft von der **Discover** Methode.  
  
## <a name="canceling-connections"></a>Abbrechen von Verbindungen  
 Durch die Festlegung eines verbindungsbezeichners in der [ConnectionID](../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md) Eigenschaft von der **"Abbrechen"** Befehl, ein Serveradministrator kann alle von einer bestimmten Verbindung, einschließlich aller zugeordneten Sitzungen Abbrechen Ausführen von Befehlen und die Verbindung abbrechen.  
  
> [!NOTE]  
>  Wenn die Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nicht finden und eine Verbindung zugeordneten Sitzungen Abbrechen, z. B. wenn die Datapump mehrere Sitzungen beim Bereitstellen von HTTP-Verbindung geöffnet wird, die Instanz die Verbindung nicht abbrechen. Wenn dieser Fall, während der Ausführung gefunden wird einer **"Abbrechen"** Befehls ein Fehler auftritt.  
  
 Ein Serveradministrator kann die aktiven Verbindungen für Abrufen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz durch das Abrufen von DISCOVER_CONNECTIONS-Schemarowsets mit dem XMLA **Discover** Methode.  
  
## <a name="canceling-server-processes"></a>Abbrechen von Serverprozessen  
 Durch angeben einen Serverprozessbezeichner (SPID) in der [SPID](../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md) Eigenschaft von der **"Abbrechen"** Befehl, ein Serveradministrator kann die einer bestimmten SPID zugeordneten Befehle Abbrechen.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Abbrechen von zugeordneten Sitzungen und Verbindungen  
 Sie können festlegen, die [CancelAssociated](../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md) Eigenschaft auf "true", um die Verbindungen, Sitzungen und die Verbindung, Sitzung oder SPID, die im angegebenen zugeordneten Befehle Abbrechen der **"Abbrechen"** Befehl.  
  
## <a name="see-also"></a>Siehe auch  
 [Discover-Methode &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
