---
title: Cachetransformation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.cachetrans.f1
- sql13.dts.designer.cachetranscon.f1
- sql13.dts.designer.cachetransmap.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 819aa38bc5c974b4d6f295ad99e1224a4aae9369
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="cache-transform"></a>Cachetransformation
  Die Transformation für Cachetransformation generiert ein Verweisdataset für die Transformation für Suche, indem Daten aus einer verbundenen Datenquelle im Datenfluss in einen Cacheverbindungs-Manager geschrieben werden. Die Transformation für Suche führt Suchvorgänge aus, indem Daten in Eingabespalten aus einer verbundenen Datenquelle mit Spalten in der Verweisdatenbank verknüpft werden.  
  
 Sie können den Cacheverbindungs-Manager verwenden, wenn Sie die Transformation für Suche für die Ausführung im Vollcachemodus konfigurieren möchten. In diesem Modus wird das Verweisdataset in den Cache geladen, bevor die Transformation für Suche ausgeführt wird.  
  
 Anweisungen dazu, wie die Transformation für Suche im Vollcachemodus mit dem Cacheverbindungs-Manager und der Transformation für Cachetransformation konfiguriert wird, finden Sie unter [Implementieren einer Suchtransformation im Vollcachemodus mit dem Cacheverbindungs-Manager](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md).  
  
 Weitere Informationen zum Zwischenspeichern des Verweisdatasets finden Sie unter [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
> [!NOTE]  
>  Die Cachetransformation schreibt nur eindeutige Zeilen in den Cacheverbindungs-Manager.  
  
 In einem einzelnen Paket kann nur eine Cachetransformation Daten in den gleichen Cacheverbindungs-Manager schreiben. Wenn das Paket mehrere Cachetransformationen enthält, schreibt die erste beim Ausführen des Pakets aufgerufene Cachetransformation die Daten in den Verbindungs-Manager. Bei den Schreibvorgängen nachfolgender Cachetransformationen treten Fehler auf.  
  
 Weitere Informationen finden Sie unter [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) (Cacheverbindungs-Manager).  
  
## <a name="configuration-of-the-cache-transform"></a>Konfiguration der Cachetransformation  
 Sie können den Cacheverbindungs-Manager so konfigurieren, dass die Daten in einer Cachedatei (.caw) gespeichert werden.  
  
 Es gibt folgende Möglichkeiten, die Cachetransformation zu konfigurieren:  
  
-   Geben Sie den Cacheverbindungs-Manager an.  
  
-   Ordnen Sie die Eingabespalten in der Cachetransformation den Zielspalten im Cacheverbindungs-Manager zu.  
  
    > [!NOTE]  
    >  Jede Eingabespalte muss einer Zielspalte zugeordnet werden, und die Spaltendatentypen müssen übereinstimmen. Andernfalls zeigt der [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Designer eine Fehlermeldung an.  
  
     Sie können den **Cacheverbindungs-Manager-Editor** verwenden, um Spaltendatentypen, Namen und andere Spalteneigenschaften zu ändern.  
  
 Eigenschaften können Sie mit dem [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Designer festlegen. Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Erweiterter Editor** festlegen können, finden Sie unter [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="cache-transformation-editor-connection-manager-page"></a>Cachetransformations-Editor (Seite 'Verbindungs-Manager')
  Mithilfe der Registerkarte **Verbindungs-Manager** des Dialogfelds **Cachetransformations-Editor** können Sie einen vorhandenen Cacheverbindungs-Manager auswählen oder einen neuen erstellen.  
  
 Weitere Informationen zum Cacheverbindungs-Manager finden Sie unter [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
### <a name="options"></a>Tastatur  
 **Cache connection manager**  
 Wählen Sie einen vorhandenen Cacheverbindungs-Manager aus dem Listenfeld aus, oder erstellen Sie mithilfe der Schaltfläche **Neu** eine neue Verbindung.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds Editor für den Cacheverbindungs-Manager eine neue Verbindung.  
  
 **Bearbeiten**  
 Ändern einer vorhandenen Verbindung.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)  
  
  
