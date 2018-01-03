---
title: ADO-Verlauf | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords: ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8be523be459914814d7e92541dd5cca21da006eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="ado-features-for-each-release"></a>ADO-Funktionen für jedes Release
In diesem Thema werden die neuen Funktionen von jeder Version von ADO, ADO MD und ADOX aufgelistet.

## <a name="ado-60"></a>ADO 6.0
 ADO 6.0 ist in Windows Vista, als Teil von Windows Data Access Components (Windows DAC) 6.0 enthalten. ADO 6.0 ist funktionell gleichwertig mit ADO 2.8.

## <a name="ado-28"></a>ADO 2.8
 ADO 2.8 wurde in Windows XP und Windows Server 2003, im Rahmen von Microsoft Data Access Components (MDAC) 2.8 enthalten. Eine verteilbare Version von MDAC 2.8 ist auch verfügbar. Beachten Sie, dass diese redistributable-Version nur auf Windows 2000 installiert werden soll. ADO 2.8 behebt mehrere sicherheitsrelevante Probleme:

 *Festplatte Zugriff ist nicht außerhalb einer Zone vertrauenswürdiger Sites zulässig.*
Die folgenden Vorgänge sind in domänenübergreifende Skripterstellung im Zusammenhang mit nicht vertrauenswürdige Standorten, deaktiviert: **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset.Save**, und **Recordset.Open**, zusammen mit den **AdCmdFile** Flag oder mit der Microsoft OLE DB-Persistenz-Provider (MSPersist).

 **Recordset.Open** *,***Recordset.Save** *,***Stream.SaveToFile** *, und* **Stream.LoadFromFile***für nur physische Dateien verwendet werden.* 
Diese Methoden nun überprüfen Sie, ob Dateihandles auf nur physische Dateien zeigen.

 **Recordset.ActiveCommand***gibt einen Fehler beim Aufrufen aus einem HTML/ASP-Seite zurück.* 
Dies verhindert, dass die **Befehl** -Sitzungsobjekts missbraucht wird.

 *Die Anzahl der***Recordsets***zurückgegebenes eine geschachtelte***Form***Befehl hat eine Obergrenze.* 
Ein geschachtelte Shape-Befehl gibt jetzt maximal 512 **Recordsets**. Dies bedeutet, dass eine **Form** Befehl kann nicht mehr in jeder beliebigen Tiefe geschachtelt werden. Stattdessen ist die maximale Tiefe der Ebene 512, wenn jeder Befehl in einem einzelnen (untergeordneten) ergibt **Recordset**. If-auf jeder Ebene, ein **Form** Befehl gibt mehrere **Recordsets**, die maximale Ebene werden weniger als 512.

## <a name="ado-27"></a>ADO 2.7
 *Unterstützung für 64-Bit-Plattform* ADO 2.7 bietet Unterstützung für 64-Bit-Prozessoren.

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***Methode* beginnen mit ADO 2.6, ADO MD-Objekte können mit abgerufen werden, eindeutige Namen entsprechend den Angaben von der [UniqueName-Eigenschaft (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md). Die Namen der übergeordneten Objekte müssen nicht bekannt sein, und übergeordneten Auflistungen müssen nicht aufgefüllt werden, um ein Objekt abzurufen. Finden Sie unter [GetSchemaObject-Methode (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md).

 *Befehl Streams* der **Befehl** Objekt unterstützt die Befehle im Stream-Format als Alternative zur Verwendung der **CommandText** Eigenschaft. Die [CommandStream-Eigenschaft (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) können verwendet werden, um die XML-Vorlagen oder Updategrams als angeben der **Befehl** Eingabe mit der Microsoft OLE DB-Anbieter für SQL Server.

 **Dialekt***Eigenschaft* [Dialekt](../../ado/reference/ado-api/dialect-property.md) ist eine neue Eigenschaft, die der Syntax definiert und die allgemeinen Regeln, dass der Anbieter verwendet, um die Zeichenfolge oder den Stream zu analysieren.

 **Recordset.Open***Methode* der [Execute-Methode](../../ado/reference/ado-api/execute-method-ado-command.md) von der ADO **Befehl** Objekt wurde verbessert, um Datenströme für ein- und Ausgaben zu verwenden.

 *Statusvalues Feld* , wenn der Benutzer eine DB_E_ERRORSOCCURRED beim Ändern fehlerbehaftete einer **Feld** des eine **Recordset**, ADO wird jetzt Füllen der **Field.Status**Eigenschaft mit dem entsprechenden Statusinformationen, damit der Benutzer hat weitere Informationen zu den Einzelheiten. Finden Sie unter [Status-Eigenschaft (ADO-Feld)](../../ado/reference/ado-api/status-property-ado-field.md).

 **NamedParameters***Eigenschaft* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) ist eine neue Eigenschaft von der **Befehl** -Objekt, das zeigt an, dass der Anbieter sollte mit dem Namen Parameter.

 *Resultsets in Datenströmen* ADO kann Resultsets zurückgeben, aus einer Datenquelle in einem **Stream**, anstelle eines **Recordset** Objekt. Verwenden die neueste Version des Microsoft OLE DB-Anbieter für SQL Server, erhalten XML-Ergebnisse vom Anbieter Sie durch Ausführen einer Abfrage "Für XML". Ein **Stream** , empfängt das Resultset kann mit einem Befehl "Für XML" als Quelle geöffnet werden. Finden Sie unter [Abrufen von Resultsets in Streams](../../ado/guide/data/retrieving-resultsets-into-streams.md).

 *Einzeilige Resultset* der ADO **Datensatz** Objekt kann nun geöffnet werden, auf eine Befehlszeichenfolge oder **Befehl** eine Zeile mit Daten vom Anbieter zurückgegebene Objekt. Dies führt zu einer verbesserten Leistung mit MDAC 2.6-Anbietern. Finden Sie unter [Open-Methode (ADO-Datensatz)](../../ado/reference/ado-api/open-method-ado-record.md).

## <a name="ado-25"></a>ADO 2.5
 **Datensatz** *Objekt* ADO 2.5 führt die **Datensatz** Objekt zum darstellen und verwalten eine Zeile aus einer **Recordset** oder einen Datenanbieter oder ein Objekt Kapseln einer semistrukturierten Daten, z. B. eine Datei oder ein Verzeichnis an.

 **Stream** *Objekt* ADO 2.5 führt auch die **Stream** Objekt zur Darstellung eines Datenstroms Binär oder Text.

 *URL-Bindung* ADO 2.5 führt die Verwendung einer URL als Alternative eine Verbindung und der Befehlstext in Text um Namen Daten um Objekte zu speichern. Eine URL verwendet werden kann, mit dem vorhandenen **Verbindung** und **Recordset** auch Objekte wie mit dem neuen **Datensatz** und **Stream** Objekte.

 *Datenanbieter, die Unterstützung von URL-Bindung* ADO 2.5 unterstützt OLE DB-Anbieter, die die URL-Schemas zu erkennen. Dies schließt OLE DB-Anbieter für Internet Publishing, die greift auf das Dateisystem von Windows 2000 und erkennt die vorhandene HTTP-Schema.
