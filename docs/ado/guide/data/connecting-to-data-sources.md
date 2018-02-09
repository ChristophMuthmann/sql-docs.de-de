---
title: Herstellen einer Verbindung mit Datenquellen | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f09a5d0fb07b9af4db1f801252359f8b77039d74
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="connecting-to-data-sources"></a>Herstellen einer Verbindung mit Datenquellen
Ein ADO **Verbindung** -Objekt stellt eine eindeutige Sitzung mit einer Datenquelle, z. B. ein DBMS, einen Speicher oder eine durch Trennzeichen getrennte Textdatei dar. Im Fall von einem Client/Server-Datenbanksystem kann die ADO-Verbindung eine tatsächliche Netzwerk-Verbindung mit dem Server sein.  
  
 Die **Verbindung** Objekt unterstützt verschiedene [Eigenschaften und Methoden](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) zum Angeben von verbindungskonfigurationen, öffnen und Schließen von Verbindungen, erstellen und Ausführen von Befehlen für die Datenquelle , und Bereitstellen von Informationen über den Entwurf der zugrunde liegenden Datenquelle in Form von Schemarowsets, usw. Abhängig von den Funktionen, die vom Anbieter, einige Auflistungen, Methoden oder Eigenschaften des unterstützt eine **Verbindung** Objekt möglicherweise nicht zur Verfügung.  
  
 Eine Verbindung herstellen, mit einer Datenquelle mithilfe einer **Verbindung** -Objekts oder mithilfe einer **Recordset** Objekt.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Verwenden eines Verbindungsobjekts](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Verwenden eines Recordset-Objekts](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Erstellen einer Verbindungszeichenfolge](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Angeben von Verbindungseigenschaften](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Steuern von Transaktionen](../../../ado/guide/data/controlling-transactions-ado.md)
