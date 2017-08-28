---
title: DQS-Bereinigung Transformation | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssdqs.designer.cleansing.f1
- sql13.SSDQS.DESIGNER.DQCONNECTION.F1
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 1fc1445538e541926b4ea3e1d593c93c5ac9d5b7
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="dqs-cleansing-transformation"></a>DQS-Bereinigungstransformation
  Die DQS-Bereinigungstransformation korrigiert Daten aus einer verbundenen Datenquelle mithilfe von Data Quality Services (DQS), indem sie genehmigte Regeln anwendet, die für die verbundene Datenquelle oder eine ähnliche Datenquelle erstellt wurden. Weitere Informationen zu Datenkorrekturregeln finden Sie unter [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Weitere Informationen zu DQS finden Sie unter [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Die DQS-Bereinigungstransformation bestimmt, ob die Daten korrigiert werden müssen, indem sie die Daten in einer Eingabespalte verarbeitet. Dabei gelten folgende Bedingungen:  
  
-   Die Spalte ist für die Datenkorrektur ausgewählt.  
  
-   Der Datentyp der Spalte wird in der Datenkorrektur unterstützt.  
  
-   Der Spalte ist eine Domäne mit einem kompatiblen Datentyp zugeordnet.  
  
 Die Transformation umfasst auch eine Fehlerausgabe, die Sie zur Behandlung von Fehlern auf Zeilenebene konfigurieren können. Die Fehlerausgabe wird mit dem **Transformations-Editor für die DQS-Bereinigung**konfiguriert.  
  
 Sie können die [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) in den Datenfluss einschließen, um Zeilen mit Daten zu ermitteln, bei denen es sich wahrscheinlich um Duplikate handelt.  
  
## <a name="data-quality-projects-and-values"></a>Data Quality-Projekte und -Werte  
 Wenn Sie Daten mit der DQS-Bereinigungstransformation verarbeiten, wird ein Bereinigungsprojekt auf dem Data Quality-Server erstellt. Das Projekt wird mit dem Data Quality Client verwaltet. Mit dem Data Quality Client können Sie außerdem die Projektwerte in eine DQS-Wissensdatenbankdomäne importieren. Sie können die Werte nur in eine Domäne (oder verknüpfte Domäne) importieren, für deren Verwendung die DQS-Bereinigungstransformation konfiguriert wurde.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Öffnen von Integration Services-Projekten im Data Quality-Client](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importieren von Bereinigungsprojektwerten in eine Domäne](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Anwenden von Datenqualitätsregeln auf eine Datenquelle](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   Artikel [Bereinigung komplexer Daten unter Verwendung von Verbunddomänen](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)auf social.technet.microsoft.com.  
  
## <a name="dqs-cleansing-transformation-editor-dialog-box"></a>Transformations-Editor für die DQS-Bereinigung (Dialogfeld)
  Im Dialogfeld **Transformations-Editor für die DQS-Bereinigung** können Sie Daten mithilfe von Data Quality Services (DQS) korrigieren. Weitere Informationen finden Sie unter [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Transformations-Editors für die DQS-Bereinigung](#open)  
  
-   [Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"](#connection)  
  
-   [Festlegen der Optionen auf der Registerkarte "Zuordnung"](#mapping)  
  
-   [Festlegen der Optionen auf der Registerkarte "Erweitert"](#advanced)  
  
-   [Festlegen der Optionen im Dialogfeld "Verbindungs-Manager für DQS-Bereinigung"](#manager)  
  
###  <a name="open"></a> Öffnen des Transformations-Editors für die DQS-Bereinigung  
  
1.  Fügen Sie die DQS-Bereinigungstransformation dem [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Paket in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]hinzu.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Komponente, und klicken Sie anschließend auf **Bearbeiten**.  
  
###  <a name="connection"></a> Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"  
 **Data Quality Services-Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen DQS-Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Verbindungs-Manager für DQS-Bereinigung** einen neuen Verbindungs-Manager. Siehe [Festlegen der Optionen im Dialogfeld „Verbindungs-Manager für DQS-Bereinigung“](#manager)  
  
 **Data Quality-Wissensdatenbank**  
 Wählen Sie eine vorhandene DQS-Wissensdatenbank für die verbundene Datenquelle aus. Weitere Informationen zur DQS-Wissensdatenbank finden Sie unter [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Verschlüsseln der Verbindung**  
 Gibt an, ob die Verbindung verschlüsselt wird, um die Datenübertragung zwischen dem DQS-Server und [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]zu verschlüsseln.  
  
 **Verfügbare Domänen**  
 Listet die verfügbaren Domänen für die ausgewählte Wissensdatenbank auf. Es gibt zwei Typen von Domänen: einzelne Domänen und Verbunddomänen, die aus mindestens zwei einzelnen Domänen bestehen.  
  
 Weitere Informationen zum Zuordnen von Spalten zu Verbunddomänen finden Sie unter [Map Columns to Composite Domains](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md).  
  
 Weitere Informationen zu Domänen finden Sie unter [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Fehlerausgabe konfigurieren**  
 Gibt an, wie Fehler auf Zeilenebene verarbeitet werden. Wenn durch die Transformation Daten aus der verbundenen Datenquelle korrigiert werden, können aufgrund unerwarteter Datenwerte oder Überprüfungseinschränkungen Fehler auftreten.  
  
 Folgende Werte sind gültig:  
  
-   **Fehler bei Komponente**gibt an, dass die Transformation fehlgeschlagen ist und dass die Eingabedaten nicht in die Data Quality Services-Datenbank eingefügt werden. Dies ist der Standardwert.  
  
-   **Zeile umleiten**gibt an, dass die Eingabedaten nicht in die Data Quality Services-Datenbank eingefügt und an die Fehlerausgabe umgeleitet werden.  
  
###  <a name="mapping"></a> Festlegen der Optionen auf der Registerkarte "Zuordnung"  
 Weitere Informationen zum Zuordnen von Spalten zu Verbunddomänen finden Sie unter [Map Columns to Composite Domains](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md).  
  
 **Verfügbare Eingabespalten**  
 Listet die Spalten aus der verbundenen Datenquelle auf. Wählen Sie Spalten aus, die zu korrigierende Daten enthalten.  
  
 **Eingabespalte**  
 Zeigt eine im Bereich **Verfügbare Eingabespalten** ausgewählte Eingabespalte an.  
  
 **Domäne**  
 Wählen Sie eine Domäne aus, die der Eingabespalte zugeordnet werden soll.  
  
 **Alias – Quelle**  
 Zeigt die Quellspalte an, die den ursprünglichen Spaltenwert enthält.  
  
 Klicken Sie in das Feld, um den Spaltennamen zu ändern.  
  
 **Ausgabealias**  
 Zeigt die Spalte an, die vom **Transformations-Editor für die DQS-Bereinigung**ausgegeben wird. Die Spalte enthält den ursprünglichen Spaltenwert oder den korrigierten Wert.  
  
 Klicken Sie in das Feld, um den Spaltennamen zu ändern.  
  
 **Alias – Status**  
 Zeigt die Spalte an, die Statusinformationen für die korrigierten Daten enthält. Klicken Sie in das Feld, um den Spaltennamen zu ändern.  
  
###  <a name="advanced"></a> Festlegen der Optionen auf der Registerkarte "Erweitert"  
 **Ausgabe standardisieren**  
 Gibt an, ob die Daten im standardisierten Format auf Grundlage des für Domänen definierten Ausgabeformats ausgegeben werden. Weitere Informationen zum standardisierten Format finden Sie unter [Datenbereinigung](../../../data-quality-services/data-cleansing.md).  
  
 **Vertrauen**  
 Gibt an, ob der Vertrauensgrad für korrigierte Daten eingeschlossen wird. Der Vertrauensgrad gibt die DQS-Sicherheitsstufe der Korrektur oder des Vorschlags an. Weitere Informationen zu Vertrauensgraden finden Sie unter [Datenbereinigung](../../../data-quality-services/data-cleansing.md).  
  
 **Reason**  
 Gibt an, ob der Grund für die Datenkorrektur eingeschlossen wird.  
  
 **Angefügte Daten**  
 Gibt an, ob weitere, von einem vorhandenen Verweisdatenanbieter empfangene Daten ausgegeben werden. Weitere Informationen finden Sie unter [Reference Data Services in DQS](../../../data-quality-services/reference-data-services-in-dqs.md).  
  
 **Angefügtes Datenschema**  
 Gibt an, ob das Datenschema ausgegeben wird. Weitere Informationen finden Sie unter [Anfügen einer Domäne oder Verbunddomäne an Verweisdaten](../../../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
###  <a name="manager"></a> Festlegen der Optionen im Dialogfeld "Verbindungs-Manager für DQS-Bereinigung"  
 **Servername**  
 Wählen Sie den Namen des DQS-Servers aus, mit dem Sie eine Verbindung herstellen möchten, oder geben Sie ihn ein. Weitere Informationen zum Server finden Sie unter [DQS Administration](../../../data-quality-services/dqs-administration.md).  
  
 **Verbindung testen**  
 Klicken Sie auf diese Schaltfläche, um zu überprüfen, ob die angegebene Verbindung gültig ist.  
  
 Sie können das Dialogfeld **Verbindungs-Manager für DQS-Bereinigung** auch wie folgt über den Verbindungsbereich öffnen:  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]ein vorhandenes [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt, oder erstellen Sie ein neues Projekt.  
  
2.  Klicken Sie im Verbindungsbereich mit der rechten Maustaste auf **Neue Verbindung**, und klicken Sie anschließend auf **DQS**.  
  
3.  Klicken Sie auf **Hinzufügen**.  
  

