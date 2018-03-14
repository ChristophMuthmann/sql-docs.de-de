---
title: "Datentypzuordnung für Oracle-Verleger | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 241e3a775bc00fbd1d8c9a773a75c9cf25138ae2
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="data-type-mapping-for-oracle-publishers"></a>Data Type Mapping for Oracle Publishers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle-Datentypen und [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentypen stimmen nicht immer exakt überein. Wenn möglich, wird beim Veröffentlichen einer Oracle-Tabelle der übereinstimmende Datentyp automatisch ausgewählt. In Fällen, in denen eine einzelne Datentypzuordnung unklar ist, werden alternative Datentypzuordnungen bereitgestellt. Informationen dazu, wie alternative Zuordnungen ausgewählt werden, finden Sie im Abschnitt "Angeben alternativer Datentypzuordnungen" weiter unten in diesem Thema.  
  
 Die folgende Tabelle zeigt die standardmäßige Zuordnung von Datentypen zwischen Oracle und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die für den Datenfluss von einem Oracle-Verleger zu einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler gültig ist. Die Spalte Alternativen gibt an, ob alternative Zuordnungen verfügbar sind.  
  
|Oracle-Datentyp|SQL Server-Datentyp|Alternativen|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|ja|  
|BLOB|VARBINARY(MAX)|ja|  
|CHAR([1-2000])|CHAR([1-2000])|ja|  
|CLOB|VARCHAR(MAX)|ja|  
|DATE|DATETIME|ja|  
|GLEITKOMMAZAHL|GLEITKOMMAZAHL|nein|  
|FLOAT([1-53])|FLOAT([1-53])|nein|  
|FLOAT([54-126])|GLEITKOMMAZAHL|nein|  
|INT|NUMERIC(38)|ja|  
|INTERVAL|DATETIME|ja|  
|LONG|VARCHAR(MAX)|ja|  
|LONG RAW|IMAGE|ja|  
|NCHAR([1-1000])|NCHAR([1-1000])|nein|  
|NCLOB|NVARCHAR(MAX)|ja|  
|NUMBER|GLEITKOMMAZAHL|ja|  
|NUMBER([1-38])|NUMERIC([1-38])|nein|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|ja|  
|NVARCHAR2([1-2000])|NVARCHAR([1-2000])|nein|  
|RAW([1-2000])|VARBINARY([1-2000])|nein|  
|real|GLEITKOMMAZAHL|nein|  
|ROWID|CHAR(18)|nein|  
|TIMESTAMP|DATETIME|ja|  
|TIMESTAMP(0-7)|DATETIME|ja|  
|TIMESTAMP(8-9)|DATETIME|ja|  
|TIMESTAMP(0-7) WITH TIME ZONE|VARCHAR(37)|ja|  
|TIMESTAMP(8-9) WITH TIME ZONE|VARCHAR(37)|nein|  
|TIMESTAMP(0-7) WITH LOCAL TIME ZONE|VARCHAR(37)|ja|  
|TIMESTAMP(8-9) WITH LOCAL TIME ZONE|VARCHAR(37)|nein|  
|UROWID|CHAR(18)|nein|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|ja|  
  
## <a name="considerations-for-data-type-mapping"></a>Überlegungen zur Datentypzuordnung  
 Beachten Sie beim Replizieren von Daten aus Oracle-Datenbanken in Bezug auf Datentypen Folgendes:  
  
### <a name="unsupported-data-types"></a>Nicht unterstützte Datentypen  
 Die folgenden Datentypen werden nicht unterstützt. Spalten, die diese Datentypen enthalten, können nicht repliziert werden:  
  
-   Objekttypen  
  
-   XML-Typen  
  
-   Varray-Typen  
  
-   Geschachtelte Tabellen  
  
-   Spalten, die den REF-Befehl verwenden  
  
### <a name="the-date-data-type"></a>Der DATE-Datentyp  
 Datumswerte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reichen von 1753 n. Chr. bis 9999 n. Chr., Datumswerte in Oracle hingegen von 4712 v. Chr. bis 4712 n. Chr. Wenn eine Spalte vom Typ DATE Werte enthält, die nicht im für SQL Server zulässigen Bereich liegen, wählen Sie einen alternativen Datentyp für die Spalte, d. h. VARCHAR(19).  
  
### <a name="float-and-number-types"></a>FLOAT- und NUMBER-Typen  
 Die Anzahl der Dezimalstellen und die Genauigkeit (Parameter 'scale' und 'precision'), die während der Zuordnung der Datentypen FLOAT und NUMBER angegeben werden, sind von den Parametern abhängig, die in der Spalte der Oracle-Datenbank angegeben wurde, die diese Datentypen verwendet. Genauigkeit gibt die Anzahl der Ziffern einer Zahl an. Dezimalstellen gibt die Anzahl der Nachkommastellen an. Die Zahl 123,45 hat z. B. eine Genauigkeit von 5 und 2 Dezimalstellen.  
  
 Bei Oracle können Zahlen mit Werten für 'scale' größer als 'precision' definiert werden, z. B. NUMBER(4,5), in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] muss jedoch 'precision' größer oder gleich 'scale' sein. Um sicherzustellen, dass keine Daten abgeschnitten werden, wenn auf dem Oracle-Verleger 'scale' größer ist als 'precision', wird 'precision' bei der Zuordnung auf denselben Wert festgelegt wie 'scale': NUMBER(4,5) wird also beispielsweise NUMERIC(5,5) zugeordnet.  
  
> [!NOTE]  
>  Wenn Sie für NUMBER weder 'scale' noch 'precision' angeben, verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] standardmäßig die maximalen Werte für 'scale' (8) und 'precision' (38). Es wird empfohlen, in Oracle eine bestimmte Anzahl von Dezimalstellen ('scale') und eine bestimmte Genauigkeit ('precision') festzulegen, um die Speicherplatzanforderungen zu reduzieren und die Leistung zu erhöhen, wenn die Daten repliziert werden.  
  
### <a name="large-object-types"></a>LOB-Typen (Large Object)  
 Oracle unterstützt bis zu 4 Gigabyte (GB), SQL Server bis zu 2 GB. Replizierte Daten über 2 GB werden deshalb abgeschnitten.  
  
 Wenn eine Oracle-Tabelle eine BFILE-Spalte enthält, werden die Daten für die Spalte im Dateisystem gespeichert. Dem Administratorkonto für die Replikation muss Zugriff auf das Verzeichnis gewährt werden, in dem die Daten gespeichert sind. Dabei ist die folgende Syntax zu verwenden:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Weitere Informationen zu LOB-Typen finden Sie im Abschnitt „Überlegungen zu großen Objekten“ unter [Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="specifying-alternative-data-type-mappings"></a>Angeben alternativer Datentypzuordnungen  
 In der Regel ist die standardmäßige Datentypzuordnung ausreichend; für bestimmte Oracle-Datentypen können Sie jedoch Datentypzuordnungen aus einem alternativen Zuordnungssatz auswählen. Es gibt zwei Möglichkeiten zum Angeben alternativer Zuordnungen:  
  
-   Überschreiben der Standardwerte auf Artikelbasis mithilfe von gespeicherten Prozeduren oder des Assistenten für neue Veröffentlichung.  
  
-   Globales Ändern der Standardwerte für alle zukünftigen Artikel mithilfe von gespeicherten Prozeduren (für vorhandene Artikel werden die Standardwerte nicht geändert).  
  
 Informationen zum Angeben alternativer Datentypzuordnungen finden Sie unter [Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
