---
title: "Hinzufügen von Wissen zur Wissensdatenbank | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/04/2013
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28cc61fbee4f967b4f5b25124b34f183c57521d4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>Hinzufügen von Wissen zur Wissensdatenbank
  In diesem Thema werden die Methoden beschrieben, mit denen Sie einer Wissensdatenbank in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) Wissen hinzufügen können. Bevor Sie Data Quality-Vorgänge ausführen können, müssen Sie Wissen zu den Daten haben. Sie erlangen dieses Wissen, indem Sie eine Data Quality-Wissensdatenbank erstellen und verwalten und ihr Wissen zu einem bestimmten Typ von Datenquelle hinzufügen. Die Wissensdatenbank ist ein Repository des Wissens zu den Daten. Sie ermöglicht es Ihnen, die Daten zu verstehen und ihre Integrität aufrechtzuerhalten.  
  
 Die Wissensdatenbank enthält Datendomänen, die sich auf die Datenquelle beziehen. Für jede Datendomäne speichert die DQKB alle identifizierten Begriffe, Rechtschreibfehler, Überprüfungs- und Geschäftsregeln sowie Verweisdaten, die verwendet werden können, um Data Quality-Aktionen für die Datenquelle auszuführen. DQS verwendet dieses Wissen, um falsche oder ungültige Daten zu identifizieren und Abgleiche auszuführen.  
  
 Sie können einer Wissensdatenbank Wissen auf die folgenden computerunterstützten oder interaktiven Weisen hinzufügen.  
  
-   [Durchführen der Wissensermittlung](#Discovery)  
  
-   [Verwalten von Datenwerten in einer Domäne](#ManageDomain)  
  
-   [Importieren von Wissen aus einer DQS-Datei](#DQSFile)  
  
-   [Importieren von Wissen aus einer Excel-Datei](#Excel)  
  
-   [Importieren von Wissen aus einem Projekt zurück in die Wissensdatenbank](#Project)  
  
-   [Verwenden der Standard-DQS-Wissensdatenbank](#Default)  
  
##  <a name="Discovery"></a> Durchführen der Wissensermittlung  
 Die Wissensermittlung analysiert Beispieldaten im Hinblick auf Data Quality-Kriterien und fügt dann der Wissensdatenbank das erlangte Wissen hinzu. Dies ist ein computerunterstützter Prozess, der Dateninkonsistenzen und Syntaxfehler identifiziert und Änderungen an den Daten vorschlägt. Die Wissensermittlungsaktivität ist ein Assistent, der eine Seite einschließt, auf der Sie Domänenwerte interaktiv verwalten können.  
  
-   Weitere Informationen finden Sie in der Dokumentation unter [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
-   Klicken Sie [hier](http://msdn.microsoft.com/sqlserver/hh323825.aspx), um ein Video anzuzeigen, in dem das Durchführen der Wissensermittlung demonstriert wird.  
  
##  <a name="ManageDomain"></a> Verwalten von Datenwerten in einer Domäne  
 DQS ermöglicht es Ihnen, die Metadaten, die von der computerunterstützten Wissensermittlungsaktivität generiert werden, interaktiv zu ändern und zu erweitern. Dazu verwenden Sie die Domänenverwaltungsaktivität, in der Sie eine Änderung auf einen bestimmten Datenwert anwenden können.  
  
-   Weitere Informationen finden Sie in der Dokumentation unter [Change Domain Values](../data-quality-services/change-domain-values.md).  
  
-   Klicken Sie [hier](http://msdn.microsoft.com/sqlserver/hh323825.aspx), um ein Video anzuzeigen, in dem das Durchführen der Domänenverwaltung demonstriert wird. Beachten Sie, dass Sie in diesem Video Domänenwerte auf der Seite zum Verwalten von Domänenwerten des Wissensermittlungs-Assistenten ändern. Sie können diese Schritte auch auf der Domänenwerteseite der Domänenverwaltungsaktivität ausführen.  
  
##  <a name="DQSFile"></a> Importieren von Wissen aus einer DQS-Datei  
 Sie können eine Domäne aus einer DQS-Datendatei in eine vorhandene Wissensdatenbank importieren, oder Sie können eine ganze Wissensdatenbank aus einem einer DQS-Datei in eine neue Wissensdatenbank importieren. Hierzu müssen Sie zuerst eine vorhandene Domäne oder Wissensdatenbank in eine DQS-Datei exportieren. Eine DQS-Datei, die eine Domäne enthält, enthält alle Domänendaten; eine DQS-Datei, die eine Wissensdatenbank enthält, enthält alle Wissensdatenbankinformationen, einschließlich Domänen und der Abgleichsrichtlinie.  
  
-   Weitere Informationen finden Sie in der Dokumentation unter [Importieren einer Domäne aus einer DQS-Datei](../data-quality-services/import-a-domain-from-a-dqs-file.md) oder [Importieren einer Wissensdatenbank aus einer DQS-Datei](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md).  
  
##  <a name="Excel"></a> Importieren von Wissen aus einer Excel-Datei  
 Sie können Domänenwerte aus einer Excel-Arbeitsblattdatei in eine vorhandene Domäne oder Wissensdatenbank importieren. Hierzu müssen Sie zuerst ein Excel-Arbeitsblatt mit den Domänenwerten erstellen, die Sie importieren möchten, und sicherstellen, dass Excel auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert ist, damit Sie in der Lage sind, Werte mithilfe von [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]zu importieren. Sie können keine Domänenwerte aus einer Domäne oder Wissensdatenbank in eine Excel-Datei importieren.  
  
-   Weitere Informationen finden Sie in der Dokumentation unter [Importieren von Werten aus einer Excel-Datei in eine Domäne](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md) oder [Importieren von Domänen aus einer Excel-Datei in eine Wissensermittlung](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md).  
  
##  <a name="Project"></a> Importieren von Wissen aus einem Projekt zurück in die Wissensdatenbank  
 Nachdem Sie ein Data Quality-Bereinigungs- oder Abgleichsprojekt mithilfe einer Wissensdatenbank ausgeführt haben, können Sie während der Bereinigung oder des Abgleichs erstelltes Wissen zurück in diese Wissensdatenbank importieren. Dies ermöglicht es Ihnen, während des Projekts generiertes Wissen beizubehalten und das Wissen in der Wissensdatenbank kontinuierlich zu vergrößern.  
  
-   Weitere Informationen finden Sie unter [Importieren von Bereinigungsprojektwerten in eine Domäne](../data-quality-services/import-cleansing-project-values-into-a-domain.md).  
  
##  <a name="Default"></a> Verwenden der Standard-DQS-Wissensdatenbank  
 Im Lieferumfang von DQS ist eine bereits erstellte Wissensdatenbank namens „DQS-Daten“ enthalten, die Domänen für US-amerikanische Firmen- und Adressdaten enthält. Diese Wissensdatenbank kann verwendet werden, um schnell ein Projekt zu starten, ohne eine neue Wissensdatenbank erstellen zu müssen. Die DQS-Daten-Wissensdatenbank ist schreibgeschützt, aber der Data Steward kann darauf basierend eine neue Wissensdatenbank erstellen.  
  
-   Weitere Informationen finden Sie in der Dokumentation unter [Using the DQS Default Knowledge Base](../data-quality-services/using-the-dqs-default-knowledge-base.md).  
  
  
