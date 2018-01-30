---
title: "Erstellen, Ändern und Löschen von räumlichen Indizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11d8454a5862b02e162e22ead3ca46e68b4f1354
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="create-modify-and-drop-spatial-indexes"></a>Erstellen, Ändern und Löschen von räumlichen Indizes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Mit einem räumlichen Index lassen sich bestimmte Operationen mit Spalten des Datentyps **geometry** oder **geography** (*räumliche Spalten*) effizienter ausführen. Für eine räumliche Spalte können mehrere räumliche Indizes angegeben werden. Dies ist beispielsweise hilfreich, wenn verschiedene Mosaikparameter in einer Spalte indiziert werden sollen.  
  
 Die Erstellung von räumlichen Indizes unterliegt einigen Einschränkungen. Weitere Informationen zu den Beschränkungen von räumlichen Indizes finden Sie unter [Erstellen, Ändern und Löschen von räumlichen Indizes](#restrictions) in diesem Thema.  
  
> [!NOTE]  
>  Weitere Informationen zur Beziehung zwischen räumlichen Indizes und Partitionen und Dateigruppen finden Sie im Abschnitt mit Hinweisen unter [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
##  <a name="creating"></a> Erstellen, Ändern und Löschen von räumlichen Indizes  
  
###  <a name="create"></a> So erstellen Sie einen räumlichen Index  
 **So erstellen Sie einen räumlichen Index mit Transact-SQL**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **So erstellen Sie mit dem Dialogfeld "Neuer Index" in Management Studio einen räumlichen Index**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>So erstellen Sie einen räumlichen Index in Management Studio  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**und anschließend die Datenbank, die die Tabelle mit dem angegebenen Index enthält, und erweitern Sie anschließend **Tabellen**.  
  
3.  Erweitern Sie die Tabelle, für die Sie den Index erstellen möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Indizes** , und wählen Sie **Neuer Index**aus.  
  
5.  Geben Sie im Feld **Indexname** einen Namen für den Index ein.  
  
6.  Wählen Sie in der Dropdownliste **Indextyp** den Eintrag **räumlich**aus.  
  
7.  Klicken Sie auf **Hinzufügen**, um die räumliche Spalte anzugeben, die indiziert werden soll.  
  
8.  Wählen Sie im Dialogfeld **Spalten auswählen aus**  *\<Tabellenname>* eine Spalte des Typs **Geometrie** oder **Geografie** aus, indem Sie das betreffende Kontrollkästchen aktivieren. Alle anderen räumlichen Spalten werden daraufhin nicht editierbar. Wenn Sie eine andere räumliche Spalte auswählen möchten, müssen Sie zuerst die Auswahl der aktuell ausgewählten Spalte aufheben. Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
9. Überprüfen Sie die Spaltenauswahl im Raster **Indexschlüsselspalten** .  
  
10. Klicken Sie im Bereich **Seite auswählen** des Dialogfelds **Indexeigenschaften** auf **räumlich**.  
  
11. Geben Sie auf der Seite **räumlich** die Werte ein, die Sie für die räumlichen Eigenschaften des Index verwenden möchten.  
  
     Beim Erstellen eines Index für eine Spalte des Typs **Geometrie** müssen Sie die Koordinaten **(***X-min***, ***Y-min***)** und **(***X-max***, ***Y-max***)** des umgebenden Felds angeben. Bei einem Index für eine Spalte des Typs **Geografie** werden die umgebenden Felder schreibgeschützt, nachdem Sie das Mosaikschema **Geografieraster** angegeben haben, weil im Geografierastermosaik kein umgebendes Feld verwendet wird.  
  
     Optional können Sie benutzerdefinierte Werte für das Feld **Zellen pro Objekt** und für die Rasterdichte auf jeder Ebene des Mosaikschemas angeben. Die Standardanzahl von Zellen pro Objekt ist 16 für [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder 8 für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder höher, und die Standardrasterdichte ist **Mittel** für [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
     In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]können Sie GEOMETRY_AUTO_GRID oder GEOGRAPHY_AUTO_GRID für das Mosaikschema auswählen. Wenn GEOMETRY_AUTO_GRID oder GEOGRAPHY_AUTO_GRID ausgewählt wird, sind die Rasterdichteoptionen für Ebene 1, Ebene 2, Ebene 3 und Ebene 4 deaktiviert.  
  
     Weitere Informationen zu diesen Eigenschaften finden Sie unter [Indexeigenschaften (F1-Hilfe)](../../relational-databases/indexes/index-properties-f1-help.md).  
  
12. Klicken Sie auf **OK**.  
  
> [!NOTE]  
>  Um einen weiteren räumlichen Index für die gleiche oder eine andere räumliche Spalte zu erstellen, wiederholen Sie die gerade beschriebenen Schritte.  
  
  
 **So erstellen Sie mit dem Tabellen-Designer in Management Studio einen räumlichen Index**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>So erstellen Sie einen räumlichen Index im Tabellen-Designer  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Tabelle, für die Sie einen räumlichen Index erstellen möchten, und klicken Sie anschließend auf **Entwerfen**.  
  
     Die Tabelle wird im Tabellen-Designer geöffnet.  
  
2.  Wählen Sie eine **Geometrie-** oder **Geografie** spalte für den Index aus.  
  
3.  Klicken Sie im Menü **Tabellen-Designer** auf **räumlicher Index**.  
  
4.  Klicken Sie im Dialogfeld **räumliche Indizes** auf **Hinzufügen**.  
  
5.  Wählen Sie den neuen Index aus der Liste **Ausgewählter räumlicher Index** aus, und legen Sie im Raster rechts die Eigenschaften für den räumlichen Index fest. Informationen zu den Eigenschaften finden Sie unter [Dialogfeld 'Räumliche Indizes' &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/4d84239a-68c7-4aa2-8602-2b51dd07260f).  
  
  
###  <a name="alter"></a> So ändern Sie einen räumlichen Index  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  Zum Ändern von Optionen, die einem bestimmten räumlichen Index eigen sind, beispielsweise BOUNDING_BOX oder GRID, können Sie entweder eine CREATE SPATIAL INDEX-Anweisung mit der Angabe DROP_EXISTING = ON verwenden, oder Sie löschen den räumlichen Index und erstellen einen neuen räumlichen Index. Für ein Beispiel gehen Sie unter [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
-   [Ändern eines Indexes](../../relational-databases/indexes/modify-an-index.md)  
  
-   [Verschieben eines vorhandenen Indexes in eine andere Dateigruppe](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="drop"></a> So löschen Sie einen räumlichen Index  
 **So löschen Sie einen räumlichen Index mit Transact-SQL**  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **So löschen Sie einen Index mit Management Studio**  
 [Löschen eines Indexes](../../relational-databases/indexes/delete-an-index.md)  
  
 **So löschen Sie mit dem Tabellen-Designer in Management Studio einen räumlichen Index**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>So löschen Sie einen räumlichen Index im Tabellen-Designer  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Tabelle mit dem räumlichen Index, den Sie löschen möchten, und klicken Sie anschließend auf **Entwerfen**.  
  
     Die Tabelle wird im Tabellen-Designer geöffnet.  
  
2.  Klicken Sie im Menü **Tabellen-Designer** auf **räumlicher Index**.  
  
     Das Dialogfeld **räumlicher Index** wird geöffnet.  
  
3.  Klicken Sie in der Spalte **Ausgewählter räumlicher Index** auf den Index, den Sie löschen möchten.  
  
4.  Klicken Sie auf **Löschen**.  
  
  
##  <a name="restrictions"></a> Erstellen, Ändern und Löschen von räumlichen Indizes  
 Ein räumlicher Index kann nur für eine Spalte des Typs **Geometrie** oder **Geografie**erstellt werden.  
  
### <a name="table-and-view-restrictions"></a>Einschränkungen für Tabellen und Sichten  
 Räumliche Indizes können nur für eine Tabelle definiert werden, die über einen Primärschlüssel verfügt. Die maximale Anzahl von Primärschlüsselspalten in einer Tabelle beträgt 15.  
  
 Die maximal zulässige Größe der Indexschlüsseldatensätze beträgt 895 Byte. Eine Überschreitung dieser Größe verursacht ein Fehler.  
  
> [!NOTE]  
>  Primärschlüsselmetadaten können nicht geändert werden, während ein räumlicher Index für eine Tabelle definiert wird.  
  
 Räumliche Indizes können nicht für indizierte Sichten angegeben werden.  
  
### <a name="multiple-spatial-index-restrictions"></a>Einschränkungen für mehrere räumliche Indizes  
 Sie können bis zu 249 räumliche Indizes für beliebige räumliche Spalten in einer unterstützten Tabelle erstellen. Die Erstellung mehrerer räumlicher Indizes für dieselben räumlichen Spalten kann sinnvoll sein, beispielsweise um verschiedene Mosaikparameter in einer einzelnen Spalte zu indizieren.  
  
 Sie können jeweils nur einen räumlichen Index erstellen.  
  
### <a name="spatial-indexes-and-process-parallelism"></a>Räumliche Indizes und Prozessparallelität  
 Bei der Indexerstellung kann die verfügbare Prozessparallelität genutzt werden.  
  
### <a name="version-restrictions"></a>Versionseinschränkungen  
 Räumliche Mosaike, die mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt wurden, können nicht in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] oder [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]repliziert werden. Sie müssen räumliche Mosaike von [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] oder [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] für räumliche Indizes für die Abwärtskompatibilität mit [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] - oder [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] -Datenbanken verwenden.  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
