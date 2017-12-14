---
title: "Abrufen und Verstehen der Änderungsdaten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d6a3dfdc39808dd1b39ca93fd4dedc0531ed668e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="retrieve-and-understand-the-change-data"></a>Abrufen und Verstehen der Änderungsdaten
  Im Datenfluss eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt, besteht der erste Task darin, die Abfrage auszuführen, bei der die Änderungsdaten abgerufen werden. Sie führen diese Abfrage innerhalb einer Quellkomponente in einem Datenflusstask aus. Sie können dann Downstream-Transformationen und -Ziele verwenden, um die Änderungsdaten auf Ihr Ziel anzuwenden.  
  
> [!NOTE]  
>  Das Erstellen einer Abfrage, die eine Tabellenwertfunktion enthält, ist der dritte Schritt beim Erstellen eines Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt. Weitere Informationen zu dieser Abfrage finden Sie unter [Erstellen der Funktion zum Abrufen der Änderungsdaten](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md). Eine Beschreibung des Gesamtprozesses zur Erstellung eines Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt, finden Sie unter [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="adding-the-data-flow-task"></a>Hinzufügen des Datenflusstasks  
 Trennen Sie im Datenfluss des Pakets, in dem Sie die Änderungsdaten abrufen, die Zeilen basierend auf dem aufgetretenen Typ der Änderung, und wenden Sie dann die Änderungen auf das Ziel an.  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>So fügen Sie dem Paket einen Datenflusstask hinzu  
  
1.  Fügen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf der Registerkarte **Ablaufsteuerung** einen Datenflusstask hinzu.  
  
2.  Verbinden Sie den vorhergehenden Task, in dem die Abfragezeichenfolge vorbereitet wurde, mit dem Datenflusstask.  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>Konfigurieren der Quellkomponente zur Abfrage von Änderungen  
 Die Quellkomponente verwendet die Abfragezeichenfolge, die in einer Variablen vorbereitet und gespeichert wurde, um die Tabellenwertfunktion aufzurufen, mit der die geänderten Daten abgerufen werden.  
  
> [!NOTE]  
>  Weitere Informationen zur Abfragezeichenfolge, die in einer Variablen vorbereitet und gespeichert wurde, finden Sie unter [Vorbereiten zur Abfrage der Änderungsdaten](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md). Weitere Informationen zur Tabellenwertfunktion, mit der die Änderungsdaten abgerufen werden, finden Sie unter [Erstellen der Funktion zum Abrufen der Änderungsdaten](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md).  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>So konfigurieren Sie eine OLE DB-Quelle zum Abrufen der Änderungsdaten  
  
1.  Fügen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf der Registerkarte **Datenfluss** eine OLE DB-Quelle hinzu.  
  
2.  Aktivieren Sie im **Quellen-Editor für OLE DB**auf der Seite **Verbindungs-Manager** die folgenden Optionen:  
  
    1.  Konfigurieren Sie zur Quelldatenbank eine gültige Verbindung.  
  
    2.  Wählen Sie für **Datenzugriffsmodus**die Option **SQL-Befehl aus Variable**aus.  
  
    3.  Wählen Sie für **Variablenname**die Option **User::SqlDataQuery**aus.  
  
3.  Vergewissern Sie sich im **Quellen-Editor für OLE DB**auf der Seite **Spalten** , dass alle gewünschten Spalten Ausgabespalten zugeordnet sind.  
  
## <a name="next-step"></a>Nächster Schritt  
 Nachdem Sie eine OLE DB-Quelle konfiguriert haben, um die Änderungsdaten abzurufen, ist der nächste Schritt der Entwurf des Datenflusses im Paket.  
  
 **Nächstes Thema** [Verarbeiten von Einfügungen, Updates und Löschungen](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)  
  
  
