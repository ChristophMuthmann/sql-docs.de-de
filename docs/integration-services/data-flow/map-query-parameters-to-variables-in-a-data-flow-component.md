---
title: Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 25f7da499f4ee62a6cdc8093c92d8d9002897edb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente
  Wenn Sie die OLE DB-Quelle so konfigurieren, dass parametrisierte Abfragen verwendet werden, können Sie die Parameter Variablen zuordnen.  
  
 Die OLE DB-Quelle verwendet parametrisierte Abfragen zum Filtern von Daten verwenden, wenn die Quelle eine Verbindung zu einer Datenquelle herstellt.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>So ordnen Sie einer Variablen einen Abfrageparameter zu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Bereich **Toolbox**die OLE DB-Quelle mit der Maus auf die Entwurfsoberfläche.  
  
4.  Klicken Sie mit der rechten Maustaste auf die OLE DB-Quelle, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Wählen Sie im **Quellen-Editor für OLE DB**einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung mit der Datenquelle aus, oder klicken Sie auf **Neu** , um einen neuen OLE DB-Verbindungs-Manager zu erstellen.  
  
6.  Wählen Sie die Option **SQL-Befehl** als Datenzugriffsmodus aus, und geben Sie im Bereich **SQL-Befehlstext** eine parametrisierte Abfrage ein.  
  
7.  Klicken Sie auf **Parameter**.  
  
8.  Ordnen Sie im Dialogfeld **Abfrageparameter festlegen** alle Parameter in der Liste **Parameter** einer Variablen in der Liste **Variablen** zu, oder klicken Sie auf **\<Neue Variable>**, um eine neue Variable zu erstellen. Klicken Sie auf **OK**.  
  
    > [!NOTE]  
    >  Nur Systemvariablen und benutzerdefinierte Variablen im Bereich des Pakets, ein übergeordneter Container (z. B. eine Foreach-Schleife) oder der Datenflusstask, in dem die Datenflusskomponente enthalten ist, können zugeordnet werden. Die Variable muss einen Datentyp aufweisen, der mit der Spalte in der WHERE-Klausel kompatibel ist, der der Parameter zugewiesen wird.  
  
9. Sie können auf **Vorschau** klicken, um bis zu 200 Zeilen der von der Abfrage zurückgegebenen Daten anzuzeigen.  
  
10. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Quelle](../../integration-services/data-flow/ole-db-source.md)   
 [Transformation für Suche](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
