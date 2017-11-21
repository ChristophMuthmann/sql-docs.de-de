---
title: CREATE SPATIAL INDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SPATIAL INDEX
- CREATE SPATIAL INDEX
- CREATE_SPATIAL_INDEX_TSQL
- SPATIAL_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], creating
- index creation [SQL Server], spatial indexes
- CREATE SPATIAL INDEX statement
- CREATE INDEX statement
ms.assetid: ee6b9116-a7ff-463a-a9f0-b360804d8678
caps.latest.revision: 89
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8fc44c4e52900f6aea611575773e3c439f3dec7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-spatial-index-transact-sql"></a>CREATE SPATIAL INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt für eine angegebene Tabelle und Spalte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen räumlichen Index. Ein Index kann erstellt werden, bevor Daten in der Tabelle enthalten sind. Indizes können für Tabellen oder Sichten einer anderen Datenbank durch Angabe eines gekennzeichneten Datenbanknamens erstellt werden. Beim räumlichen Indizes muss die Tabelle einen gruppierten Primärschlüssel aufweisen. Informationen zu räumlichen Indizes finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- SQL Server Syntax  
  
CREATE SPATIAL INDEX index_name   
  ON <object> ( spatial_column_name )  
    {  
       <geometry_tessellation> | <geography_tessellation>  
    }   
  [ ON { filegroup_name | "default" } ]  
[;]   
  
<object> ::=  
    [ database_name. [ schema_name ] . | schema_name. ]  table_name  
  
<geometry_tessellation> ::=  
{   
  <geometry_automatic_grid_tessellation>   
| <geometry_manual_grid_tessellation>   
}  
  
<geometry_automatic_grid_tessellation> ::=  
{  
    [ USING GEOMETRY_AUTO_GRID ]  
          WITH  (  
        <bounding_box>  
            [ [,] <tessellation_cells_per_object> [ ,…n] ]  
            [ [,] <spatial_index_option> [ ,…n] ]  
                 )  
}  
  
<geometry_manual_grid_tessellation> ::=  
{  
       [ USING GEOMETRY_GRID ]  
         WITH (  
                    <bounding_box>  
                        [ [,]<tessellation_grid> [ ,…n] ]  
                        [ [,]<tessellation_cells_per_object> [ ,…n] ]  
                        [ [,]<spatial_index_option> [ ,…n] ]  
   )  
}   
  
<geography_tessellation> ::=  
{  
      <geography_automatic_grid_tessellation> | <geography_manual_grid_tessellation>  
}  
  
<geography_automatic_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_AUTO_GRID ]  
    [ WITH (  
        [ [,] <tessellation_cells_per_object> [ ,…n] ]  
        [ [,] <spatial_index_option> ]  
     ) ]  
}  
  
<geography_manual_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_GRID ]  
    [ WITH (  
                [ <tessellation_grid> [ ,…n] ]  
                [ [,] <tessellation_cells_per_object> [ ,…n] ]  
                [ [,] <spatial_index_option> [ ,…n] ]  
                ) ]  
}  
  
<bounding_box> ::=  
{  
      BOUNDING_BOX = ( {  
       xmin, ymin, xmax, ymax   
       | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>   
  } )  
}  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tesselation_grid> ::=  
{   
    GRIDS = ( { <grid_level> [ ,...n ] | <grid_size>, <grid_size>, <grid_size>, <grid_size>  }   
        )  
}  
<tesseallation_cells_per_object> ::=  
{   
   CELLS_PER_OBJECT = n   
}  
  
<grid_level> ::=  
{  
     LEVEL_1 = <grid_size>   
  |  LEVEL_2 = <grid_size>   
  |  LEVEL_3 = <grid_size>   
  |  LEVEL_4 = <grid_size>   
}  
  
<grid_size> ::= { LOW | MEDIUM | HIGH }  
  
<spatial_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE }  
}  
  
```  
  
```  
-- Windows Azure SQL Database Syntax   
  
CREATE SPATIAL INDEX index_name   
    ON <object> ( spatial_column_name )   
    {   
      [ USING <geometry_grid_tessellation> ]   
          WITH ( <bounding_box>   
                [ [,] <tesselation_parameters> [,... n ] ]   
                [ [,] <spatial_index_option> [,... n ] ] )   
     | [ USING <geography_grid_tessellation> ]   
          [ WITH ( [ <tesselation_parameters> [,... n ] ]   
                   [ [,] <spatial_index_option> [,... n ] ] ) ]   
    }  
  
[ ; ]  
  
<object> ::=  
{  
    [database_name. [schema_name ] . | schema_name. ]   
                table_name   
}  
  
<geometry_grid_tessellation> ::=   
{ GEOMETRY_GRID }  
  
<bounding_box> ::=   
BOUNDING_BOX = ( {  
        xmin, ymin, xmax, ymax   
   | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>   
  } )  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tesselation_parameters> ::=   
{   
    GRIDS = ( { <grid_density> [ ,... n ] | <density>, <density>, <density>, <density>  } )   
  | CELLS_PER_OBJECT = n   
}  
  
<grid_density> ::=   
{  
     LEVEL_1 = <density>   
  |  LEVEL_2 = <density>   
  |  LEVEL_3 = <density>   
  |  LEVEL_4 = <density>   
}  
  
<density> ::= { LOW | MEDIUM | HIGH }  
  
<geography_grid_tessellation> ::=   
{ GEOGRAPHY_GRID }  
  
<spatial_index_option> ::=   
{  
    IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF   
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 *index_name*  
 Der Name des Indexes. Indexnamen müssen für eine Tabelle eindeutig sein, können aber innerhalb einer Datenbank mehrfach vorkommen. Indexnamen müssen den Regeln der [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 ON \<Objekt > ( *Spatial_column_name* )  
 Gibt das Objekt (Datenbank, Schema oder Tabelle), für das der Index erstellt werden soll, sowie den Namen der räumlichen Spalte an.  
  
 *Spatial_column_name* gibt an, die räumliche Spalte, auf denen der Index basiert. Nur eine räumliche Spalte kann in der Definition eines einzelnen räumlichen Indexes angegeben werden; Allerdings können mehrere räumliche Indizes erstellt werden, auf eine **Geometrie** oder **Geography** Spalte.  
  
 USING  
 Gibt das Mosaikschema für den räumlichen Index an. Dieser Parameter verwendet den typspezifischen, in der folgenden Tabelle angezeigten Wert:  
  
|Datentyp der Spalte|Mosaikschema|  
|-------------------------|-------------------------|  
|**Geometrie**|GEOMETRY_GRID|  
|**Geometrie**|GEOMETRY_AUTO_GRID|  
|**geography**|GEOGRAPY_GRID|  
|**geography**|GEOGRAPHY_AUTO_GRID|  
  
 Ein räumlicher Index kann nur für eine Spalte des Typs **Geometrie** oder **Geografie**erstellt werden. Andernfalls wird ein Fehler ausgelöst. Ein Fehler wird auch dann ausgelöst, wenn für einen bestimmten Typ ein ungültiger Parameter übergeben wird.  
  
 Informationen zur Verwendung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Mosaik, implementiert finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 ON *Filegroup_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Erstellt den angegebenen Index für die angegebene Dateigruppe. Wenn kein Speicherort angegeben und die Tabelle nicht partitioniert ist, verwendet der Index die gleiche Dateigruppe wie die zugrunde liegende Tabelle. Die Dateigruppe muss bereits vorhanden sein.  
  
 ON "default"  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Erstellt den angegebenen Index für die Standarddateigruppe.  
  
 Die Benennung default ist in diesem Kontext kein Schlüsselwort. Es handelt sich dabei um einen Bezeichner für die Standarddateigruppe, der begrenzt sein muss, wie in ON "default" oder ON [default]. Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 **\<Objekt >:: =**  
  
 Gibt das vollqualifizierte oder nicht vollqualifizierte Objekt an, das indiziert werden soll.  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle gehört.  
  
 *table_name*  
 Der Name der Tabelle, die indiziert werden soll.  
  
 Die Windows Azure SQL-Datenbank unterstützt das aus drei Teilen bestehende Format database_name.[schema_name].object_name, wenn database_name die aktuelle Datenbank bzw. database_name tempdb ist und object_name mit # beginnt.  
  
### <a name="using-options"></a>USING-Optionen  
 GEOMETRY_GRID  
 Gibt an, die **Geometrie** rastermosaikschema, die Sie verwenden. GEOMETRY_GRID kann nur für eine Spalte angegeben werden die **Geometrie** -Datentyp.  GEOMETRY_GRID ermöglicht manuelle Anpassungen des Mosaikschemas.  
  
 GEOMETRY_AUTO_GRID  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Kann nur für eine Spalte des geometry-Datentyps angegeben werden. Dies ist der Standardwert für diesen Datentyp; eine Angabe ist nicht erforderlich.  
  
 GEOGRAPHY_GRID  
 Gibt das Mosaikschema für das Geografieraster an. GEOGRAPHY_GRID kann nur für eine Spalte angegeben werden die **Geography** -Datentyp.  
  
 GEOGRAPHY_AUTO_GRID  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Kann nur für eine Spalte mit dem Datentyp geography angegeben werden.  Dies ist der Standardwert für diesen Datentyp; eine Angabe ist nicht erforderlich.  
  
### <a name="with-options"></a>WITH-Optionen  
 BOUNDING_BOX  
 Gibt einen aus vier Werten bestehenden numerischen Tupel zurück, der die vier Koordinaten des Begrenzungsrahmens definiert: die minimale X- und die minimale Y-Koordinate der unteren linken Ecke und die maximale X- und die maximale Y-Koordinate der oberen rechten Ecke.  
  
 *xmin*  
 Gibt die X-Koordinate der unteren linken Ecke des umgebenden Felds an.  
  
 *"ymin"*  
 Gibt die Y-Koordinate der unteren linken Ecke des umgebenden Felds an.  
  
 *"xmax"*  
 Gibt die X-Koordinate der oberen rechten Ecke des Begrenzungsrahmens an.  
  
 *ymax*  
 Gibt die Y-Koordinate der oberen rechten Ecke des Begrenzungsrahmens an.  
  
 XMIN = *Xmin*  
 Gibt den Eigenschaftsnamen und -wert für die X-Koordinate der unteren linken Ecke des Begrenzungsrahmens an.  
  
 "Ymin" =*"ymin"*  
 Gibt den Eigenschaftsnamen und -wert für die Y-Koordinate der unteren linken Ecke des umgebenden Felds an.  
  
 "Xmax" =*"xmax"*  
 Gibt den Eigenschaftsnamen und -wert für die X-Koordinate der oberen rechten Ecke des umgebenden Felds an.  
  
 YMAX =*Ymax*  
 Gibt den Eigenschaftsnamen und -wert für die Y-Koordinate der oberen rechten Ecke des umgebenden Felds an.  
  
 Die Koordinaten des umgebenden Felds gelten nur in einer USING GEOMETRY_GRID-Klausel.  
  
 *"xmax"* muss größer sein als *Xmin* und *Ymax* muss größer sein als *"ymin"*. Sie können eine beliebige gültige angeben ["float"](../../t-sql/data-types/float-and-real-transact-sql.md) Darstellung, vorausgesetzt, dass value: *"xmax"* > *Xmin* und *Ymax*  >  *"ymin"*. Andernfalls werden die entsprechenden Fehler ausgelöst.  
  
 Es gibt keine Standardwerte.  
  
 Bei den Eigenschaftsnamen für umgebende Felder wird, unabhängig von der Datenbanksortierung, die Groß- und Kleinschreibung nicht beachtet.  
  
 Eigenschaftsnamen müssen jeweils nur einmal angegeben werden. Sie können in einer beliebigen Reihenfolge angegeben werden. Beispielsweise sind die folgenden Klauseln gleichwertig:  
  
-   BOUNDING_BOX = (XMIN =*Xmin*, "ymin" =*"ymin"*, "xmax" =*"xmax"*, YMAX =*Ymax* )  
  
-   BOUNDING_BOX = (XMIN =*Xmin*, "xmax" =*"xmax"*, "ymin" =*"ymin"*, YMAX =*Ymax*)  
  
 GRIDS  
 Definiert die Dichte des Rasters auf jeder Ebene eines Mosaikschemas. Wenn GEOMETRY_AUTO_GRID und GEOGRAPHY_AUTO_GRID ausgewählt werden, wird diese Option deaktiviert.  
  
 Informationen zu Mosaiken finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 Die GRIDS-Parameter lauten wie folgt:  
  
 LEVEL_1  
 Gibt das Raster der obersten (höchsten) Ebene an.  
  
 LEVEL_2  
 Gibt das Raster der zweiten Ebene an.  
  
 LEVEL_3  
 Gibt das Raster der dritten Ebene an.  
  
 LEVEL_4  
 Gibt das Raster der vierten Ebene an.  
  
 LOW  
 Gibt die niedrigste mögliche Dichte für das Raster auf einer bestimmten Ebene an. LOW entspricht 16 Zellen (4 x 4-Raster).  
  
 **MITTEL**  
 Gibt die mittlere Dichte für das Raster auf einer bestimmten Ebene an. MEDIUM entspricht 64 Zellen (8 x 8-Raster).  
  
 HIGH  
 Gibt die höchste mögliche Dichte für das Raster auf einer bestimmten Ebene an. HIGH entspricht 256 Zellen (16 x 16-Raster).  
  
 Mithilfe von Ebenennamen können Sie die Ebenen in einer beliebigen Reihenfolge angeben oder Ebenen auslassen. Wenn Sie den Namen einer Ebene verwenden, müssen Sie auch die Namen aller anderen angegebenen Ebenen verwenden. Wenn Sie eine Ebene auslassen, wird die Dichte standardmäßig auf MEDIUM festgelegt.  
  
 Bei Angabe einer ungültigen Dichte wird ein Fehler ausgelöst.  
  
 CELLS_PER_OBJECT =*n*  
 Gibt die Anzahl von Zellen pro Objekt für das Mosaik an, die vom Mosaikprozess für ein einzelnes räumliches Objekt im Index verwendet werden können. *n*eine beliebige ganze Zahl zwischen 1 und 8192 (einschließlich) kann sein. Wenn bei einem bestimmten Mosaik eine ungültige Anzahl übergeben wird oder die Anzahl die maximal zulässige Anzahl von Zellen überschreitet, wird ein Fehler ausgelöst.  
  
 CELLS_PER_OBJECT hat die folgenden Standardwerte:  
  
|USING-Option|Standardzellen pro Objekt|  
|------------------|------------------------------|  
|GEOMETRY_GRID|**16**|  
|GEOMETRY_AUTO_GRID|**8**|  
|GEOGRAPHY_GRID|**16**|  
|GEOGRAPHY_AUTO_GRID|**12**|  
  
 Auf höchster Ebene verwendet die Indizierung die Anzahl von Zellen, die zum Bereitstellen eines vollständigen Mosaiks der höchsten Ebene erforderlich sind, wenn ein Objekt mehr Zellen abdeckt, als durch *n*angegeben sind. In solchen Fällen ist es möglich, dass ein Objekt mehr als die angegebene Anzahl von Zellen erhält. Die maximale Anzahl ist dann die Anzahl von Zellen, die von dem Raster der höchsten Ebene generiert wird, welche von der Dichte abhängt.  
  
 Der CELLS_PER_OBJECT-Wert wird von der Zellen-pro-Objekt-Mosaikregel verwendet. Informationen zu den mosaikregeln finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 PAD_INDEX = {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 ON  
 Gibt an, dass der Prozentsatz des freien, der Speicherplatz angegebenen *Fillfactor* auf die zwischenebenenseiten des Indexes angewendet wird.  
  
 Deaktivieren oder *Fillfactor* ist nicht angegeben.  
 Gibt an, dass die Zwischenebenenseiten nahezu vollständig aufgefüllt sind. Allerdings ist ausreichend Speicherplatz vorhanden, um mindestens eine Zeile in der maximal für den Index möglichen Größe aufzunehmen, wenn der Schlüsselsatz auf den Zwischenseiten berücksichtigt wird.  
  
 Die Option PAD_INDEX ist nur dann hilfreich, wenn FILLFACTOR angegeben ist, da PAD_INDEX den durch FILLFACTOR angegebenen Prozentsatz verwendet. Wenn der für FILLFACTOR angegebene Prozentsatz nicht groß genug ist, um eine Zeile aufzunehmen, überschreibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] diesen Prozentsatz intern, um das Minimum zuzulassen. Die Anzahl der Zeilen auf jeder Zwischenindexseite ist nie kleiner als zwei, unabhängig davon, wie Niedrig der Wert der *Fillfactor*.  
  
 FILLFACTOR =*Fillfactor*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt einen Prozentsatz an, der angibt, wie weit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -neuerstellung füllen soll. *FILLFACTOR* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0. Wenn *Fillfactor* 100 oder 0 (null) ist die [!INCLUDE[ssDE](../../includes/ssde-md.md)] Indizes mit vollständig aufgefüllten Blattseiten erstellt.  
  
> [!NOTE]  
>  Die Füllfaktorwerte 0 und 100 sind in jeder Hinsicht identisch.  
  
 Die FILLFACTOR-Einstellung gilt nur, wenn der Index erstellt oder neu erstellt wird. [!INCLUDE[ssDE](../../includes/ssde-md.md)] hält den angegebenen Prozentsatz des Speicherplatzes nicht dynamisch auf den Seiten frei. Verwenden Sie zum Anzeigen der füllfaktoreinstellung der [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
> [!IMPORTANT]  
>  Das Erstellen eines gruppierten Indexes mit einem FILLFACTOR-Wert unter 100 wirkt sich auf den Speicherplatz aus, den die Daten belegen, da [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Daten beim Erstellen des gruppierten Indexes neu verteilt.  
  
 Weitere Informationen finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt an, ob temporäre Ergebnisse des Sortierens in tempdb gespeichert werden sollen. Der Standardwert ist OFF.  
  
 ON  
 Die Zwischenergebnisse von Sortierungen, mit denen der Index erstellt wird, werden in tempdb gespeichert. Diese Option verringert u. U. den Zeitaufwand, der mit der Erstellung eines Indexes verbunden ist, wenn sich tempdb auf einem anderen Datenträgersatz befindet als die Benutzerdatenbank. Sie erhöht jedoch den Betrag an Speicherplatz, der während der Indexerstellung verwendet wird.  
  
 OFF  
 Die Zwischenergebnisse der Sortierung werden in derselben Datenbank gespeichert wie der Index.  
  
 Zusätzlich zu dem Speicherplatz, der in der Benutzerdatenbank zum Erstellen des Indexes erforderlich ist, muss tempdb ungefähr die gleiche Menge an zusätzlichem Speicherplatz aufweisen, um die Zwischenergebnisse des Sortierens zu speichern. Weitere Informationen finden Sie unter [SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY =**OFF**  
 Hat keine Auswirkungen für räumliche Indizes, da der Indextyp nie eindeutig ist. Legen Sie diese Option nicht auf ON fest, oder es wird ein Fehler ausgelöst.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF**}  
 Gibt an, ob Verteilungsstatistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ON  
 Veraltete Indexstatistiken werden nicht automatisch neu berechnet.  
  
 OFF  
 Die automatischen Updates der Statistiken sind aktiviert.  
  
 Um das automatische Aktualisieren von Statistiken wiederherzustellen, müssen Sie STATISTICS_NORECOMPUTE auf OFF festlegen oder die UPDATE STATISTICS-Anweisung ohne die NORECOMPUTE-Klausel ausführen.  
  
> [!IMPORTANT]  
>  Wenn Sie die automatische Neuberechnung von Verteilungsstatistiken deaktivieren, wählt der Abfrageoptimierer möglicherweise nicht die optimalen Ausführungspläne für Abfragen, an denen die Tabelle beteiligt ist.  
  
 DROP_EXISTING = {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt an, dass der benannte, bereits vorhandene räumliche Index gelöscht und neu erstellt wird. Der Standardwert ist OFF.  
  
 ON  
 Der vorhandene Index wird gelöscht und neu erstellt. Der angegebene Indexname muss mit dem Namen eines derzeit vorhandenen Index übereinstimmen. Die Indexdefinition kann jedoch geändert werden. Sie können beispielsweise andere Spalten, eine andere Sortierreihenfolge, ein anderes Partitionsschema oder andere Indexoptionen angeben.  
  
 OFF  
 Es wird ein Fehler angezeigt, wenn der angegebene Indexname bereits vorhanden ist.  
  
 Der Indextyp kann nicht mithilfe von DROP_EXISTING geändert werden.  
  
 ONLINE =**OFF**  
 Gibt an, dass zugrunde liegende Tabellen oder zugehörige Indizes für Abfragen und Datenänderungen während des Indexvorgangs nicht zur Verfügung stehen. In dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Onlineindexerstellungen für räumliche Indizes nicht unterstützt. Wenn diese Option für einen räumlichen Index auf ON festgelegt ist, wird ein Fehler ausgelöst. Lassen Sie die ONLINE-Option weg, oder legen Sie ONLINE auf OFF fest.  
  
 Ein Offlineindexvorgang, der einen räumlichen Index erstellt, neu erstellt oder löscht, aktiviert eine Schemaänderungssperre (Sch-M) für die Tabelle. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können.  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ALLOW_ROW_LOCKS = { **ON** | {OFF}  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Zeilensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden.  
  
 OFF  
 Zeilensperren werden nicht verwendet.  
  
 ALLOW_PAGE_LOCKS = { **ON** | {OFF}  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Seitensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden.  
  
 OFF  
 Seitensperren werden nicht verwendet.  
  
 MAXDOP =*Max_degree_of_parallelism*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Überschreibt die Konfigurationsoption `max degree of parallelism` für die Dauer des Indexvorgangs. Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
> [!IMPORTANT]  
>  Obwohl die MAXDOP-Option syntaktisch unterstützt wird, verwendet CREATE SPATIAL INDEX derzeit immer nur einen einzelnen Prozessor.  
  
 *Max_degree_of_parallelism* sind möglich:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Beschränkt die maximale Anzahl der Prozessoren, die bei einem parallelen Indexvorgang verwendet werden, je nach aktueller Systemauslastung auf die angegebene Zahl oder einen niedrigeren Wert.  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Parallele Indexvorgänge sind nicht verfügbar in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 DATA_COMPRESSION = {NONE | ROW | PAGE}  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Bestimmt die Ebene der vom Index verwendeten Datenkomprimierung.  
  
 Keine  
 Die Daten werden im Index nicht komprimiert.  
  
 ROW  
 Die Daten werden im Index zeilenweise komprimiert.  
  
 PAGE  
 Die Daten werden im Index seitenweise komprimiert.  
  
## <a name="remarks"></a>Hinweise  
 Jede Option kann pro CREATE SPATIAL INDEX-Anweisung nur einmal angegeben werden. Beim Angeben einer Option, die es schon einmal gibt, wird ein Fehler ausgelöst.  
  
 Sie können bis zu 249 räumliche Indizes für jede räumliche Spalte in einer Tabelle erstellen. Es kann sich als nützlich erweisen, mehrere räumliche Indizes für bestimmte räumliche Spalten zu erstellen, z. B. zum Indizieren verschiedener Mosaikparameter in einer Spalte.  
  
> [!IMPORTANT]  
>  Die Erstellung von räumlichen Indizes unterliegt einigen weiteren Einschränkungen. Weitere Informationen finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 Bei der Indexerstellung kann eine verfügbare Prozessparallelität nicht genutzt werden.  
  
## <a name="methods-supported-on-spatial-indexes"></a>Von räumlichen Indizes unterstützte Methoden  
 Unter bestimmten Bedingungen unterstützen räumliche Indizes eine Reihe von mengenorientierten Geometriemethoden. Weitere Informationen finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="spatial-indexes-and-partitioning"></a>Räumliche Indizes und Partitionierung  
 Standardmäßig wird beim Erstellen eines räumlichen Indexes für eine partitionierte Tabelle der Index in Übereinstimmung mit dem Partitionsschema der Tabelle partitioniert. So kann sichergestellt werden, dass Indexdaten und die zugehörige Zeile in der gleichen Partition gespeichert werden.  
  
 In diesem Fall müssen Sie, um das Partitionsschema der Basistabelle zu ändern, den räumlichen Index löschen, bevor Sie die Basistabelle neu partitionieren können. Diese Einschränkung kann umgangen werden, indem Sie beim Erstellen eines räumlichen Indexes die "ON filegroup"-Option angeben. Weitere Informationen finden Sie nachfolgend unter "Räumliche Indizes und Dateigruppen".  
  
## <a name="spatial-indexes-and-filegroups"></a>Räumliche Indizes und Dateigruppen  
 Standardmäßig werden räumliche Indizes in die gleichen Dateigruppen wie die Tabelle partitioniert, für die der Index angegeben wird. Dies kann durch Angabe der Dateigruppe überschrieben werden:  
  
 [ON { *Filegroup_name* | "Default"}]  
  
 Wenn Sie eine Dateigruppe für einen räumlichen Index angeben, wird der Index unabhängig vom Partitionierungsschema der Tabelle in dieser Dateigruppe platziert.  
  
## <a name="catalog-views-for-spatial-indexes"></a>Katalogsichten für räumliche Indizes  
 Die folgenden Katalogsichten sind für räumliche Indizes spezifisch:  
  
 [Sys. spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)  
 Stellt die wichtigsten Indexinformationen der räumlichen Indizes dar.  
  
 [Sys. spatial_index_tessellations](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)  
 Stellt die Informationen zum Mosaikschema und zu den Parametern jedes räumlichen Indexes dar.  
  
## <a name="additional-remarks-about-creating-indexes"></a>Zusätzliche Hinweise zum Erstellen von Indizes  
 Weitere Informationen zum Erstellen von Indizes finden Sie unter dem Abschnitt "Hinweise" in [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss über die ALTER-Berechtigung für die Tabelle oder Sicht verfügen oder Mitglied der festen Serverrolle "Sysadmin" oder der Db_ddladmin und der festen Datenbankrolle "Db_owner" sein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-spatial-index-on-a-geometry-column"></a>A. Erstellen eines räumlichen Indexes für eine geometry-Spalte  
 Das folgende Beispiel erstellt eine Tabelle namens `SpatialTable` , enthält eine **Geometrie** Spalte des Typs `geometry_col`. Dann wird ein räumlicher Index, `SIndx_SpatialTable_geometry_col1`, für `geometry_col` erstellt. Im Beispiel wird das Standardmosaikschema verwendet und das umgebende Feld angegeben.  
  
```  
CREATE TABLE SpatialTable(id int primary key, geometry_col geometry);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col1   
   ON SpatialTable(geometry_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ) );  
```  
  
### <a name="b-creating-a-spatial-index-on-a-geometry-column"></a>B. Erstellen eines räumlichen Indexes für eine geometry-Spalte  
 Im folgenden Beispiel wird ein zweiter räumlicher Index, `SIndx_SpatialTable_geometry_col2`, für `geometry_col` in der Tabelle `SpatialTable` erstellt. Im Beispiel wird `GEOMETRY_GRID` als Mosaikschema angegeben. Im Beispiel werden auch das umgebende Feld, unterschiedliche Dichten auf verschiedenen Ebenen und 64 Zellen pro Objekt angegeben. Zudem wird die Auffüllung von Indizes auf `ON` festgelegt.  
  
```  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col2  
   ON SpatialTable(geometry_col)  
   USING GEOMETRY_GRID  
   WITH (  
    BOUNDING_BOX = ( xmin=0, ymin=0, xmax=500, ymax=200 ),  
    GRIDS = (LOW, LOW, MEDIUM, HIGH),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="c-creating-a-spatial-index-on-a-geometry-column"></a>C. Erstellen eines räumlichen Indexes für eine geometry-Spalte  
 Im folgenden Beispiel wird ein dritter räumlicher Index, `SIndx_SpatialTable_geometry_col3`, für `geometry_col` in der Tabelle `SpatialTable` erstellt. Im Beispiel wird das Standardmosaikschema verwendet. Im Beispiel wird das umgebende Feld angegeben, und es werden unterschiedliche Zelldichten auf der dritten und vierten Ebene, aber die vorgegebene Anzahl von Zellen pro Objekt verwendet.  
  
```  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col3  
   ON SpatialTable(geometry_col)  
   WITH (  
    BOUNDING_BOX = ( 0, 0, 500, 200 ),  
    GRIDS = ( LEVEL_4 = HIGH, LEVEL_3 = MEDIUM ) );  
```  
  
### <a name="d-changing-an-option-that-is-specific-to-spatial-indexes"></a>D. Ändern einer für räumliche Indizes spezifischen Option  
 Im folgenden Beispiel wird der räumliche Index neu erstellt, der im vorherigen Beispiel erstellt wurde, nämlich `SIndx_SpatialTable_geography_col3`. Zu diesem Zweck wird eine neue Dichte für `LEVEL_3` mit DROP_EXISTING = ON angegeben.  
  
```  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable(geography_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ),  
        GRIDS = ( LEVEL_3 = LOW ),  
        DROP_EXISTING = ON );  
```  
  
### <a name="e-creating-a-spatial-index-on-a-geography-column"></a>E. Erstellen eines räumlichen Indexes für eine geography-Spalte  
 Das folgende Beispiel erstellt eine Tabelle namens `SpatialTable2` , enthält eine **Geography** Spalte des Typs `geography_col`. Dann wird ein räumlicher Index, `SIndx_SpatialTable_geography_col1`, für `geography_col` erstellt. Im Beispiel werden die Standardparameterwerte des Mosaikschemas GEOGRAPHY_AUTO_GRID verwendet.  
  
```  
CREATE TABLE SpatialTable2(id int primary key, object GEOGRAPHY);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col1   
   ON SpatialTable2(object);  
```  
  
> [!NOTE]  
>  Für Geografierasterindizes kann kein Begrenzungsrahmen angegeben werden.  
  
### <a name="f-creating-a-spatial-index-on-a-geography-column"></a>F. Erstellen eines räumlichen Indexes für eine geography-Spalte  
 Im folgenden Beispiel wird ein zweiter räumlicher Index, `SIndx_SpatialTable_geography_col2`, für `geography_col` in der Tabelle `SpatialTable2` erstellt. Im Beispiel wird `GEOGRAPHY_GRID` als Mosaikschema angegeben. Im Beispiel werden auch unterschiedliche Rasterdichten auf verschiedenen Ebenen und 64 Zellen pro Objekt angegeben. Zudem wird die Auffüllung von Indizes auf `ON` festgelegt.  
  
```  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col2  
   ON SpatialTable2(object)  
   USING GEOGRAPHY_GRID  
   WITH (  
    GRIDS = (MEDIUM, LOW, MEDIUM, HIGH ),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="g-creating-a-spatial-index-on-a-geography-column"></a>G. Erstellen eines räumlichen Indexes für eine geography-Spalte  
 Im folgenden Beispiel wird dann ein dritter räumlicher Index, `SIndx_SpatialTable_geography_col3`, für `geography_col` in der Tabelle `SpatialTable2` erstellt. Im Beispiel werden das Standardmosaikschema GEOGRAPHY_GRID und der Standardwert für CELLS_PER_OBJECT (16) verwendet.  
  
```  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable2(object)  
   WITH ( GRIDS = ( LEVEL_3 = HIGH, LEVEL_2 = HIGH ) );  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [Sys. spatial_index_tessellations &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [Sys. spatial_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  

