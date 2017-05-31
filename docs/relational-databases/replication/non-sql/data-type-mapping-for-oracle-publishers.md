---
title: "Datentypzuordnung für Oracle-Verleger | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6eb74ce4647046c91fa199c260abeb1ae1845f66
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="data-type-mapping-for-oracle-publishers"></a>Datentypzuordnung für Oracle-Verleger
  Oracle-Datentypen und [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentypen stimmen nicht immer exakt überein. Wenn möglich, wird beim Veröffentlichen einer Oracle-Tabelle der übereinstimmende Datentyp automatisch ausgewählt. In Fällen, in denen eine einzelne Datentypzuordnung unklar ist, werden alternative Datentypzuordnungen bereitgestellt. Informationen dazu, wie alternative Zuordnungen ausgewählt werden, finden Sie im Abschnitt "Angeben alternativer Datentypzuordnungen" weiter unten in diesem Thema.  
  
 Die folgende Tabelle zeigt die standardmäßige Zuordnung von Datentypen zwischen Oracle und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die für den Datenfluss von einem Oracle-Verleger zu einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler gültig ist. Die Spalte Alternativen gibt an, ob alternative Zuordnungen verfügbar sind.  
  
|Oracle-Datentyp|SQL Server-Datentyp|Alternativen|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|Ja|  
|BLOB|VARBINARY(MAX)|Ja|  
|CHAR([1-2000])|CHAR([1-2000])|Ja|  
|CLOB|VARCHAR(MAX)|Ja|  
|DATE|DATETIME|Ja|  
|GLEITKOMMAZAHL|GLEITKOMMAZAHL|Nein|  
|FLOAT([1-53])|FLOAT([1-53])|Nein|  
|FLOAT([54-126])|GLEITKOMMAZAHL|Nein|  
|INT|NUMERIC(38)|Ja|  
|INTERVAL|DATETIME|Ja|  
|LONG|VARCHAR(MAX)|Ja|  
|LONG RAW|IMAGE|Ja|  
|NCHAR([1-1000])|NCHAR([1-1000])|Nein|  
|NCLOB|NVARCHAR(MAX)|Ja|  
|NUMBER|GLEITKOMMAZAHL|Ja|  
|NUMBER([1-38])|NUMERIC([1-38])|Nein|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|Ja|  
|NVARCHAR2([1-2000])|NVARCHAR([1-2000])|Nein|  
|RAW([1-2000])|VARBINARY([1-2000])|Nein|  
|REAL|GLEITKOMMAZAHL|Nein|  
|ROWID|CHAR(18)|Nein|  
|TIMESTAMP|DATETIME|Ja|  
|TIMESTAMP(0-7)|DATETIME|Ja|  
|TIMESTAMP(8-9)|DATETIME|Ja|  
|TIMESTAMP(0-7) WITH TIME ZONE|VARCHAR(37)|Ja|  
|TIMESTAMP(8-9) WITH TIME ZONE|VARCHAR(37)|Nein|  
|TIMESTAMP(0-7) WITH LOCAL TIME ZONE|VARCHAR(37)|Ja|  
|TIMESTAMP(8-9) WITH LOCAL TIME ZONE|VARCHAR(37)|Nein|  
|UROWID|CHAR(18)|Nein|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|Ja|  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
