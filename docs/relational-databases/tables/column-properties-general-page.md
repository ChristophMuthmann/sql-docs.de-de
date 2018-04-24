---
title: Spalteneigenschaften (Registerkarte Allgemein) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.columnproperties.general.f1
ms.assetid: a745890b-994e-4c23-8028-5c83751e60c4
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0bf90973ad2a99e415f23d62fd4ad047f881f2a4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="column-properties-general-page"></a>Spalteneigenschaften (Registerkarte Allgemein)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Zeigen Sie mithilfe dieser Seite die Eigenschaften der ausgewählten Spalte an.  
  
 Die Informationen auf dieser Seite sind schreibgeschützt. Zum Ändern der Spalte schließen Sie das Dialogfeld **Spalteneigenschaften** , erweitern Sie im Objekt-Explorer die Tabelle und die Spalten, klicken Sie mit der rechten Maustaste auf die Spalte, und klicken Sie dann auf **Entwurf**.  
  
## <a name="options"></a>Tastatur  
 **Name**  
 Name der Spalte.  
  
 **Datentyp**  
 Datentyp, den die Spalte enthalten kann. Wenn der Datentyp ein benutzerdefinierter Datentyp ist, wird der benutzerdefinierte Datentyp angezeigt. Wenn der Datentyp kein benutzerdefinierter Datentyp ist, wird der Systemdatentyp angezeigt. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
 **Systemtyp**  
 Datentyp, den die Spalte enthalten kann. Wenn der Datentyp ein Systemdatentyp ist, wird der Systemdatentyp angezeigt. Wenn der Datentyp ein benutzerdefinierter Datentyp ist, wird der Systemdatentyp angezeigt, auf den der benutzerdefinierte Datentyp aufbaut.  
  
 **Primärschlüssel**  
 Gibt an, ob es sich bei der Spalte um einen Primärschlüssel handelt. Mögliche Werte sind **True**und **False**.  
  
 **NULL-Werte zulassen**  
 Gibt an, ob die Spalte NULL-Werte annimmt. Mögliche Werte sind **True** und **False**.  
  
 **Ist berechnet**  
 Gibt an, ob der Spaltenwert das Ergebnis eines berechneten Ausdrucks ist.  
  
 **Berechneter Text**  
 Gibt die Anweisung an, die zur Berechnung des Spaltentexts verwendet wird. Weitere Informationen finden Sie unter [Specify Computed Columns in a Table](../../relational-databases/tables/specify-computed-columns-in-a-table.md).  
  
 **Identität**  
 Gibt an, ob die Spalte die Identitätsspalte der Tabelle ist. Mögliche Werte sind **True** und **False**.  
  
 **ID-Startwert**  
 Gibt den anfänglichen Zeilenwert für eine Identitätsspalte an.  
  
 **ID-Schrittweite**  
 Die Eigenschaft **ID-Inkrement** gibt den Wert an, den [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Generieren eines Identitätswerts für eine eingefügte Zeile zum größten vorhandenen Zeilenidentitätswert hinzufügt.  
  
 **Standardbindungen**  
 Der an die Spalte gebundene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Standard. Ohne gebundenen Standard ist diese Spalte leer.  
  
 **Standardschema**  
 Identifiziert das Datenbankschema, das den an die Spalte, auf die verwiesen wird, gebundenen Standard besitzt. Ohne gebundenen Standard ist diese Spalte leer.  
  
 **Rule**  
 Identifiziert die Datenintegritätseinschränkung, die an die Spalte gebunden ist. Ohne gebundene Regel ist diese Spalte leer.  
  
 **Regelschema**  
 Zeigt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankschema an, das die Regel besitzt, die an diejenige Spalte gebunden ist, auf die verwiesen wird. Ohne gebundene Regel ist diese Spalte leer.  
  
 **Länge**  
 Gibt die maximale für die Spalte zulässige Anzahl von Zeichen oder Bytes an.  
  
 **Sortierung**  
 Zeigt die aktuelle Sortierung für die Spalte an. Wenn leer, wird die Sortierungseigenschaft vom Objekt geerbt.  
  
 **Numerische Genauigkeit**  
 Gibt die maximale Anzahl von Ziffern bei einem numerischen Datentyp mit fester Genauigkeit an.  
  
 **Numerische Dezimalstellen**  
 Gibt die Anzahl von Ziffern rechts vom Dezimaltrennzeichen bei einem numerischen Datentyp mit fester Genauigkeit an.  
  
 **XML-Schemanamespace**  
 Definiert den Typ der XML-Spalte mithilfe einer XSD-Überprüfung (XML Schema Definition Language).  
  
 **XML-Schemanamespace-Schema**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Schema, das den XML-Schemanamespace besitzt.  
  
> [!NOTE]  
>  Es gibt eine Reihe häufig verwendeter, jedoch unterschiedlicher Bedeutungen des Begriffs Schema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein Schema zum Organisieren von Datenbankobjekten verwendet. Ähnliches gilt für den Begriff Besitz. XML verwendet das Schema zum Definieren der Organisation von XML-Informationen in einer Reihe von Namespaces. Es stellt eine Möglichkeit dar, miteinander in Beziehung stehenden XML-Code zu gruppieren.  
  
 **Ist von geringer Dichte**  
 Gibt an, ob die Spalte eine Sparsespalte ist. Mögliche Werte sind **True** und **False**. Weitere Informationen finden Sie unter [Verwenden von Spalten mit geringer Dichte](../../relational-databases/tables/use-sparse-columns.md).  
  
 **Ist ein Spaltensatz**  
 Gibt an, ob es sich bei der Spalte um einen Spaltensatz handelt. Mögliche Werte sind **True** und **False**. Weitere Informationen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
 **ANSI-Auffüllungsstatus**  
 Gibt an, ob die ANSI-Auffüllung aktiviert ist. Weitere Informationen finden Sie unter [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
 **Volltext**  
 Zeigt an, ob die Spalte bei Volltextabfragen berücksichtigt wird.  
  
 **Statistische Semantik**  
 Gibt an, ob die statistische semantische Suche für die Spalte aktiviert ist. Weitere Informationen finden Sie unter [Semantische Suche &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 **Not For Replication**  
 Gibt an, ob die Spalte zur Replizierung zur Verfügung steht. Mögliche Werte sind **True** und **False**.  
  
  
