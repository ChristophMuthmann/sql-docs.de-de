---
title: Erstellen einer Verbindungszeichenfolge | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ce4aad7a961d79d9a59b6d41e3f539ec3912174
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="creating-a-connection-string"></a>Erstellen einer Verbindungszeichenfolge
Eine Verbindungszeichenfolge besteht aus einer Liste von Argument-Wert-Paaren (d. h. Parameter), die durch Semikolons getrennt sind. Beispiel:  
  
```  
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 Alle Parameter müssen vom ADO- oder den angegebenen Anbieter erkannt werden.  
  
 ADO erkennt die folgenden fünf Argumente in einer Verbindungszeichenfolge.  
  
|Argument|Description|  
|--------------|-----------------|  
|*Provider*|Gibt den Namen eines Anbieters für die Verbindung verwenden.|  
|*Dateiname*|Gibt den Namen einer anbieterspezifischen-Datei (z. B. eine persistente Datenquellenobjekt), die voreingestellte Verbindungsinformationen enthält.|  
|*URL*|Gibt die Verbindungszeichenfolge als eine absolute URL identifiziert eine Ressource, z. B. eine Datei oder ein Verzeichnis an.|  
|*Remoteanbieter*|Gibt den Namen eines Anbieters beim Öffnen einer clientseitigen Verbindung verwenden. (Nur remote Data Service.)|  
|*Remoteserver*|Gibt den Pfadnamen des Servers, der beim Öffnen einer clientseitigen Verbindung verwenden. (Nur remote Data Service.)|  
  
 Andere Argumente werden an den Anbieter mit dem Namen der *Anbieter* Argument ohne Verarbeitung von ADO.  
  
 Die Anwendung HelloData in [HelloData: eine einfache ADO-Anwendung](../../../ado/guide/data/hellodata-a-simple-ado-application.md) verwendet die folgende Verbindungszeichenfolge:  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 In dieser Verbindungszeichenfolge ADO erkennt nur die `"Provider=SQLOLEDB"` -Parameter, der Microsoft OLE DB-Anbieter für SQL Server als ADO-Datenquelle angibt. Das Argument/Wert-Paaren, die restlichen `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`, werden für diesen Anbieter wörtliche übergeben. Der Typ und die Gültigkeit des solche Parameter sind anbieterspezifischen. Informationen zu gültigen Parametern, die in der Verbindungszeichenfolge übergeben werden können, finden Sie in den einzelnen Anbieter-Dokumentation.  
  
 Gemäß der OLE DB-Provider für SQL Server-Dokumentation können Sie "Server" ersetzen, für die *Datenquelle* Parameter und "Database" für die *Anfangskatalog* Parameter. Daher erzeugt die folgende Verbindungszeichenfolge identisch mit dem Kennwort, die oben genannten Ergebnisse:  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
