---
title: Quellen-Editor (Verbindungsseite) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6bb7a97ddbcae4868ee7b737358d4b30608e4df2
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="odata-source-editor-connection-page"></a>Quellen-Editor für OData (Seite 'Verbindung')
  Auf der Seite **Verbindung** des Dialogfelds **Quellen-Editor für OData** wählen Sie den OData-Verbindungs-Manager für die OData-Quelle aus. Auf dieser Seite können Sie außerdem eine Auflistung oder einen Ressourcenpfad sowie beliebige Abfrageoptionen angeben, mit denen die aus der OData-Quelle abzurufenden Daten bestimmt werden. Weitere Informationen zur OData-Quelle finden Sie unter [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="static-options"></a>Statische Optionen  
 **OData-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 Nach dem Auswählen oder Erstellen eines Verbindungs-Managers wird im Dialogfeld die vom Verbindungs-Manager verwendete OData-Protokollversion angezeigt.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OData-Verbindungs-Manager-Editor** einen neuen Verbindungs-Manager.  
  
 **Auflistung oder Ressourcenpfad verwenden**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Description|  
|------------|-----------------|  
|Auflistung|Rufen Sie mithilfe eines Auflistungsnamens Daten aus der OData-Quelle ab.|  
|Ressourcenpfad|Rufen Sie mithilfe eines Ressourcenpfads Daten aus der OData-Quelle ab.|  
  
 **Abfrageoptionen**  
 Geben Sie Optionen für die Abfrage an.  Beispiel: $top=5  
  
 **Feed-URL**  
 Zeigt die schreibgeschützte Feed-URL auf Grundlage der Optionen an, die Sie in diesem Dialogfeld ausgewählt haben.  
  
 **Vorschau**  
 Zeigt mithilfe des Dialogfelds **Vorschau** eine Vorschau der Ergebnisse an. In der**Vorschau** können bis zu 20 Zeilen angezeigt werden.  
  
## <a name="dynamic-options"></a>Dynamische Optionen  
  
### <a name="use-collection-or-resource-path--collection"></a>Auflistung oder Ressourcenpfad verwenden = Auflistung  
 **Auflistung**  
 Wählen Sie eine Auflistung aus dem Dropdownlistenfeld aus.  
  
### <a name="use-collection-or-resource-path--resource-path"></a>Auflistung oder Ressourcenpfad verwenden = Ressourcenpfad  
 **Resource path**  
 Geben Sie einen Ressourcenpfad ein. Beispiel: Mitarbeiter  
  
## <a name="see-also"></a>Siehe auch  
 [OData-Quellen-Editor &#40; Seite "Spalten" &#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)   
 [OData-Quellen-Editor &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)   
 [OData-Verbindungs-Manager](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
