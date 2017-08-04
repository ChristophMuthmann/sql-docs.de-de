---
title: Fuzzy Lookup Transformations-Editor (Registerkarte Verweistabelle) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 083e8bbb2791cf8ac72dfde6b11ab93570a5990b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>Transformations-Editor für Fuzzysuche (Registerkarte Verweistabelle)
  Auf der Registerkarte **Verweistabelle** des Dialogfelds **Transformations-Editor für Fuzzysuche** können Sie die Quelltabelle und den Index für die Suche angeben. Bei der Verweisdatenquelle muss es sich um eine Tabelle in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank handeln.  
  
> [!NOTE]  
>  Durch die Transformation für die Fuzzysuche wird eine Arbeitskopie der Verweistabelle erstellt. Die nachfolgend beschriebenen Indizes werden für diese Arbeitstabelle mithilfe einer Spezialtabelle erstellt, und nicht mit einem normalen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Index. Durch die Transformation werden die vorhandenen Quelltabellen nicht verändert, sofern Sie nicht **Gespeicherten Index beibehalten**auswählen. In diesem Fall wird ein Trigger für die Verweistabelle erstellt, der die Arbeitstabelle und die Suchindextabelle auf der Grundlage von Änderungen an der Verweistabelle aktualisiert.  
  
> [!NOTE]  
>  Die **Exhaustive** - und **MaxMemoryUsage** -Eigenschaften der Transformation für Fuzzysuche sind im **Transformations-Editor für Fuzzysuche**nicht verfügbar, können jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Darüber hinaus kann ein Wert größer als 100 für **MaxOutputMatchesPerInput** nur im Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Transformation für Fuzzysuche von [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Weitere Informationen zur Transformation für Fuzzysuche finden Sie unter [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
## <a name="options"></a>enthalten  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen OLE DB-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** eine neue Verbindung.  
  
 **Neuen Index generieren**  
 Geben Sie an, dass die Transformation einen neuen Index erstellen soll, der für die Suche verwendet wird.  
  
 **Name der Verweistabelle**  
 Wählen Sie die vorhandene Tabelle aus, die als Verweis-(Such-)Tabelle verwendet werden soll.  
  
 **Neuen Index speichern**  
 Wählen Sie diese Option aus, wenn Sie den neuen Suchindex speichern möchten.  
  
 **Name des neuen Indexes**  
 Wenn Sie den neuen Suchindex speichern möchten, geben Sie einen beschreibenden Namen für den Index ein.  
  
 **Gespeicherten Index beibehalten**  
 Wenn Sie den neuen Suchindex speichern möchten, geben Sie an, ob der Index auch in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] beibehalten werden soll.  
  
> [!NOTE]  
>  Wenn Sie **Gespeicherten Index beibehalten** auf der Registerkarte **Verweistabelle** des Dialogfelds **Transformations-Editor für Fuzzysuche**wählen, verwendet die Transformation verwaltete gespeicherte Prozeduren zum Verwalten des Index. Diese verwalteten gespeicherten Prozeduren verwenden die Common Language Runtime-Integrationsfunktion (CLR) in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Standardmäßig ist die CLR-Integration in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht aktiviert. Um die Funktion **Gespeicherten Index beibehalten** zu verwenden, müssen Sie die CLR-Integration aktivieren. Weitere Informationen finden Sie unter [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Da die Option **Gespeicherten Index beibehalten** die CLR-Integration erfordert, kann diese Funktion nur verwendet werden, wenn Sie in einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eine Verweistabelle auswählen, für die die CLR-Integration aktiviert ist.  
  
 **Vorhandenen Index verwenden**  
 Gibt an, dass bei der Transformation ein vorhandener Index für die Suche verwendet werden soll.  
  
 **Name eines vorhandenen Indexes**  
 Wählen Sie einen zu einem früheren Zeitpunkt erstellten Index aus der Liste aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Fuzzy Lookup Transformations-Editor &#40; Registerkarte "Spalten" &#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Fuzzy Lookup Transformations-Editor &#40; Registerkarte "Erweitert" &#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
