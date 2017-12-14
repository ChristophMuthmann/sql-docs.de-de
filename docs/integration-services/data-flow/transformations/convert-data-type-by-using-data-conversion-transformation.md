---
title: "Konvertieren des Datentyps mithilfe der Transformation für Datenkonvertierung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
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
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fcae6a724feb11400c8b6c3d4e149bc6b87504c9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="convert-data-type-by-using-data-conversion-transformation"></a>Konvertieren des Datentyps mithilfe der Transformation für Datenkonvertierung
  Um eine Transformation für Datenkonvertierung hinzuzufügen und zu konfigurieren, muss das Paket bereits mindestens einen Datenflusstask und eine Quelle enthalten.  
  
### <a name="to-convert-data-to-a-different-data-type"></a>So konvertieren Sie Daten in einen anderen Datentyp  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Bereich **Toolbox**die Transformation für Datenkonvertierung auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für Datenkonvertierung mit dem Datenfluss, indem Sie einen Konnektor von der Quelle oder der vorherigen Transformation auf die Transformation für Datenkonvertierung ziehen.  
  
5.  Doppelklicken Sie auf die Transformation für Datenkonvertierung.  
  
6.  Aktivieren Sie im Dialogfeld **Transformations-Editor für Datenkonvertierung** in der Tabelle **Verfügbare Eingabespalten** das Kontrollkästchen neben den Spalten, deren Datentyp Sie konvertieren möchten.  
  
    > [!NOTE]  
    >  Für eine Eingabespalte können mehrere Datenkonvertierungen angewendet werden.  
  
7.  Optional können die Standardwerte in der **Ausgabealias** -Spalte geändert werden.  
  
8.  Wählen Sie in der Liste **Datentyp** den neuen Datentyp für die Spalte aus. Der Standarddatentyp ist der Datentyp der Eingabespalte.  
  
9. Aktualisieren Sie optional in Abhängigkeit vom ausgewählten Datentyp die Werte in den Spalten **Länge**, **Genauigkeit**, **Dezimalstellen**und **Codepage** .  
  
10. Um die Fehlerausgabe zu konfigurieren, klicken Sie auf **Fehlerausgabe konfigurieren**. Weitere Informationen finden Sie unter [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
11. Klicken Sie auf **OK**.  
  
12. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services Paths](../../../integration-services/data-flow/integration-services-paths.md)  (Integration Services-Pfade)  
 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)  (Integration Services-Datentypen)  
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  
