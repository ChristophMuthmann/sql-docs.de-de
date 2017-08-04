---
title: Cacheverbindungs-Manager-Editor | Microsoft Docs
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
- sql13.dts.designer.cacheconnection.f1
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c8fd51cc4abae8c4756a896809b75d6c449862d
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="cache-connection-manager-editor"></a>Editor für den Cacheverbindungs-Manager
  Der Cacheverbindungs-Manager liest ein Verweisdataset aus der Cachetransformation oder einer Cachedatei (.caw) und kann die Daten in einer Cachedatei speichern. Die Daten werden immer im Arbeitsspeicher abgelegt.  
  
> [!NOTE]  
>  Der Cacheverbindungs-Manager unterstützt die BLOB-Datentypen (Binary Large Object) DT_TEXT, DT_NTEXT und DT_IMAGE nicht. Wenn das Verweisdataset einen BLOB-Datentyp enthält, schlägt die Komponente fehl, wenn Sie das Paket ausführen. Sie können den **Cacheverbindungs-Manager-Editor** verwenden, um Spaltendatentypen zu ändern.  
  
 Die Transformation für Suche führt Suchvorgänge im Verweisdataset aus.  
  
 Das Dialogfeld **Editor für den Cacheverbindungs-Manager** schließt die folgenden Registerkarten ein:  
  
-   [Registerkarte "Allgemein"](../../integration-services/connection-manager/cache-connection-manager-editor.md#generaltab)  
  
-   [Registerkarte "Spalten"](../../integration-services/connection-manager/cache-connection-manager-editor.md#columnstab)  
  
 Weitere Informationen zum Cacheverbindungs-Manager finden Sie unter [Cache Connection Manager](../../integration-services/connection-manager/cache-connection-manager.md).  
  
##  <a name="generaltab"></a> Registerkarte Allgemein  
 Geben Sie auf der Registerkarte **Allgemein** des Dialogfelds **Editor für den Cacheverbindungs-Manager** an, ob der Cache aus einer Datei gelesen werden soll oder ob der Cache in einer Datei gespeichert werden soll.  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Cacheverbindung im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Die bewährte Methode ist hierbei, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Dateicache verwenden**  
 Geben Sie an, ob eine Cachedatei verwendet werden soll.  
  
> [!NOTE]  
>  Die Schutzebene des Pakets gilt nicht für die Cachedatei. Wenn die Cachedatei vertrauliche Informationen enthält, schränken Sie den Zugriff auf den Speicherort oder Ordner, in dem Sie die Datei speichern, mithilfe einer Zugriffssteuerungsliste ein. Sie sollten nur bestimmten Konten den Zugriff ermöglichen. Weitere Informationen finden Sie unter [Zugriff auf Dateien, die von Paketen verwendet werden](../../integration-services/security/security-overview-integration-services.md#files).  
  
 Wenn Sie den Cacheverbindungs-Manager für die Verwendung einer Cachedatei konfigurieren, führt der Verbindungs-Manager eine der folgenden Aktionen aus:  
  
-   Speichern der Daten in einer Datei, wenn eine Cachetransformation so konfiguriert ist, dass Daten aus einer Datenquelle im Datenfluss in den Cacheverbindungs-Manager geschrieben werden. Weitere Informationen finden Sie unter [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Lesen von Daten aus der Cachedatei  
  
 **Dateiname**  
 Geben Sie den Pfad und Dateinamen der Cachedatei ein.  
  
 **Durchsuchen**  
 Suchen Sie die Cachedatei.  
  
 **Metadaten aktualisieren**  
 Löschen Sie die Spaltenmetadaten im Cacheverbindungsmanager, und füllen Sie den Cacheverbindungs-Manager erneut mit Spaltenmetadaten aus einer bestimmten Cachedatei auf.  
  
##  <a name="columnstab"></a> Registerkarte 'Spalten'  
 Auf der Registerkarte **Spalten** des Dialogfelds **Editor für den Cacheverbindungs-Manager** können Sie die Eigenschaften jeder Spalte im Cache konfigurieren.  
  
### <a name="options"></a>enthalten  
 **Column**  
 Geben Sie den Spaltennamen an.  
  
 **Indexposition**  
 Geben Sie an, welche Spalten Indexspalten sind, indem Sie die Indexposition jeder Spalte angeben. Der Index ist eine Auflistung einer oder mehrerer Spalten.  
  
 Für Nicht-Index-Spalten ist die Indexposition 0.  
  
 Für Indexspalten ist die Indexposition eine fortlaufende positive Zahl. Diese Zahl gibt die Reihenfolge an, in der die Suchtransformation Zeilen im Verweisdataset mit Zeilen der Eingabedatenquelle vergleicht. Die Spalte mit den meisten eindeutigen Werten sollte die niedrigste Indexposition aufweisen.  
  
> [!NOTE]  
>  Wenn die Transformation für Suche so konfiguriert ist, dass sie einen Cacheverbindungs-Manager verwendet, können nur Indexspalten im Verweisdataset Eingabespalten zugeordnet werden. Auch müssen alle Indexspalten zugeordnet werden.  
  
 **Typ**  
 Geben Sie den Datentyp der Spalte an.  
  
 **Länge**  
 Gibt den Datentyp der Spalte an. Wenn für den Datentyp zutreffend, können Sie den Wert von **Length**aktualisieren.  
  
 **Genauigkeit**  
 Gibt die Genauigkeit für bestimmte Spaltendatentypen an. Genauigkeit gibt die Anzahl der Ziffern einer Zahl an. Wenn für den Datentyp zutreffend, können Sie den Wert von **Precision**aktualisieren.  
  
 **Dezimalstellen**  
 Gibt die Dezimalstellen für bestimmte Spaltendatentypen an. Dezimalstellen gibt die Anzahl der Nachkommastellen an. Wenn für den Datentyp zutreffend, können Sie den Wert von **Scale**aktualisieren.  
  
 **Codepage**  
 Gibt die Codepage für den Spaltentyp an. Wenn für den Datentyp zutreffend, können Sie den Wert von **Code Page**aktualisieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für Suche](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
