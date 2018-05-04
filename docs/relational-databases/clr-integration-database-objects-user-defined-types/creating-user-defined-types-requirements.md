---
title: User-Defined Type-Anforderungen | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6d4bccc8ae83d25f848011421d057ad8cb0a7016
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="creating-user-defined-types---requirements"></a>Erstellen von benutzerdefinierten Typen - Anforderungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie müssen mehrere wichtige entwurfsentscheidungen für die Erstellung einen benutzerdefinierten Typ (UDT), auf installiert werden, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Für die meisten UDTs wird das Erstellen als Struktur empfohlen, obwohl auch das Erstellen als Klasse möglich ist. Die UDT-Definition muss den Spezifikationen für das Erstellen von UDTs entsprechen, um mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert werden zu können.  
  
## <a name="requirements-for-implementing-udts"></a>Anforderungen für das Implementieren von UDTs  
 Um in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt zu werden, muss der UDT die folgenden Anforderungen in der UDT-Definition implementieren:  
  
 Geben Sie der UDT muss die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**. Die Verwendung der **System.SerializableAttribute** ist optional, jedoch empfohlen.  
  
-   Der UDT muss implementieren die **System.Data.SqlTypes.INullable** in der Klasse oder Struktur durch Erstellen einer öffentlichen Schnittstelle **statische** (**Shared** in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) **Null** Methode. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erkennt standardmäßig NULL-Werte. Dies ist notwendig für Code, der im UDT ausgeführt wird, um in der Lage zu sein, einen NULL-Wert zu erkennen.  
  
-   Der UDT muss eine öffentliche enthalten **statische** (oder **Shared**) **analysieren** -Methode, die Analysen unterstützt, sowie eine öffentliche **ToString** Methode für Konvertieren in eine Zeichenfolgendarstellung des Objekts.  
  
-   Ein UDT mit einem benutzerdefinierten Serialisierungsformat muss implementieren die **System.Data.IBinarySerialize** Schnittstelle, und geben Sie eine **lesen** und ein **schreiben** Methode.  
  
-   Der UDT muss implementieren **System.Xml.Serialization.IXmlSerializable**, oder alle öffentlichen Felder und Eigenschaften von Typen, die XML-serialisierbar oder mit ergänzten müssen die **XmlIgnore** Attribut, wenn Überschreiben einer Standardserialisierung ist erforderlich.  
  
-   Es darf nur eine Serialisierung eines UDT-Objekts geben. Die Überprüfung schlägt fehl, wenn die Serialisierungs- oder Deserialisierungsroutinen mehr als eine Darstellung eines bestimmten Objekts erkennen.  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** muss **"true"** , Daten in Bytereihenfolge zu vergleichen. Wenn die IComparable-Schnittstelle nicht implementiert wird und **SqlUserDefinedTypeAttribute.IsByteOrdered** ist **"false"**, Vergleiche in Bytereihenfolge fehl.  
  
-   Ein in einer Klasse definierter UDT muss über einen öffentlichen Konstruktor verfügen, der keine Argumente verwendet. Sie können optional zusätzliche überladene Klassenkonstruktoren erstellen.  
  
-   Der UDT muss Datenelemente als öffentliche Felder oder Eigenschaftenprozeduren verfügbar machen.  
  
-   Öffentliche Namen dürfen nicht länger als 128 Zeichen enthalten und entsprechen dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benennungsregeln für Bezeichner gemäß [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
-   **Sql_variant** Spalten können keine Instanzen eines UDTS enthalten.  
  
-   Auf vererbte Member kann nicht von [!INCLUDE[tsql](../../includes/tsql-md.md)] aus zugegriffen werden, da das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Typsystem die Vererbungshierarchie zwischen UDTs nicht kennt. Sie können Vererbung allerdings verwenden, wenn Sie Klassen strukturieren, und Sie können diese Methoden in der verwalteten Codeimplementierung des Typs aufrufen.  
  
-   Mit Ausnahme des Klassenkonstruktors können Member nicht überladen werden. Wenn Sie eine überladene Methode erstellen, wird kein Fehler ausgelöst, wenn Sie die Assembly registrieren oder den Typ in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellen Erkennung der überladenen Methode tritt zur Laufzeit auf, nicht beim Erstellen des Typs. Überladene Methoden können in der Klasse vorhanden sein, solange sie nie aufgerufen werden. Sobald Sie eine überladene Methode aufrufen, wird ein Fehler ausgelöst.  
  
-   Alle **statische** (oder **Shared**) Member müssen als Konstanten deklariert oder als schreibgeschützt sein. Statische Member können nicht änderbar sein.  
  
-   Wenn die **SqlUserDefinedTypeAttribute.MaxByteSize** -Feld auf-1 festgelegt ist, kann der serialisierten UDTS so groß wie die größenbeschränkung für große Objekte (LOB) (zurzeit 2 GB). Die Größe des UDTS kann nicht angegebenen Wert überschreitet die **MaxByteSized** Feld.  
  
> [!NOTE]  
>  Obwohl sie vom Server zum Durchführen von Vergleichen nicht verwendet wird, können Sie optional implementieren die **System.IComparable** -Schnittstelle, die eine einzelne Methode verfügbar macht, **CompareTo**. Diese Methode wird auf Clientseite in Situationen verwendet, in denen UDT-Werte präzise verglichen oder geordnet werden sollen.  
  
## <a name="native-serialization"></a>Systemeigene Serialisierung  
 Die Auswahl der richtigen Serialisierungsattribute für den UDT hängt vom Typ des UDTs ab, den Sie erstellen möchten. Die **Native** Serialisierungsformat wird eine sehr einfache Struktur, die es ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um eine effiziente systemeigene Darstellung des UDTS auf dem Datenträger zu speichern. Die **Native** Format wird empfohlen, wenn der UDT einfach ist und nur Felder der folgenden Typen enthält:  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Werttypen, die aus Feldern der oben genannten Typen bestehen, die gute für Kandidaten **Native** format, z. B. **Strukturen** in Visual c# (oder **Strukturen** wie in der sie bekannt sind Visual Basic). Ein UDT beispielsweise angegeben, mit der **Native** Serialisierungsformat möglicherweise auf ein Feld eines anderen UDTS, die auch mit angegeben wurde die **Native** Format. Wenn die UDT-Definition komplexer ist und Datentypen, die nicht in der obigen Liste enthält, geben Sie die **UserDefined** Serialisierungsformat stattdessen.  
  
 Die **Native** Format gelten die folgenden Anforderungen:  
  
-   Der Typ muss keinen Wert für **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**.  
  
-   Alle Felder müssen serialisierbar sein.  
  
-   Die **System.Runtime.InteropServices.StructLayoutAttribute** muss angegeben werden, als **StructLayout.LayoutKindSequential** ist der UDT in einer Klasse und nicht in einer Struktur definiert wird. Dieses Attribut steuert das physische Layout der Datenfelder und wird verwendet, um zu erzwingen, dass die Elemente in der Reihenfolge angeordnet werden, in der sie erscheinen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bestimmt anhand dieses Attributs die Feldreihenfolge für UDTs mit mehreren Werten.  
  
 Ein Beispiel für einen UDT mit definierten **Native** Serialisierung finden Sie unter der Point-UDT in [Codieren benutzerdefinierter Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>UserDefined-Serialisierung  
 Die **UserDefined** -formateinstellung für die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** -Attribut gibt dem Entwickler volle Kontrolle über das Binärformat. Beim Angeben der **Format** -Attributeigenschaft als **UserDefined**, müssen Sie folgende in Ihrem Code:  
  
-   Geben Sie den optionalen **IsByteOrdered** -Attributeigenschaft. Der Standardwert ist **false**.  
  
-   Geben Sie die **MaxByteSize** Eigenschaft von der **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
-   Schreiben Sie Code zum Implementieren von **lesen** und **schreiben** Methoden für den UDT durch Implementieren der **System.Data.Sql.IBinarySerialize** Schnittstelle.  
  
 Ein Beispiel für einen UDT mit definierten **UserDefined** Serialisierung finden Sie im Currency-UDT in [Codieren benutzerdefinierter Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Für UDT-Felder muss die systemeigene Serialisierung verwendet werden, oder die Felder müssen erhalten bleiben, um indiziert zu werden.  
  
## <a name="serialization-attributes"></a>Serialisierungsattribute  
 Attribute bestimmen, wie die Serialisierung verwendet wird, um die Speicherdarstellung von UDTs zu erstellen und um UDTs durch Werte an den Client zu übertragen. Sie werden aufgefordert, anzugeben der **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** beim Erstellen des UDT. Die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** Attribut gibt an, dass die Klasse ein UDT ist, und den Speicher für den UDT gibt. Sie können optional angeben, die **Serializable** Attribut, obwohl [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dieses nicht erfordert.  
  
 Die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** hat die folgenden Eigenschaften.  
  
 **Format**  
 Gibt das Serialisierungsformat möglich **Native** oder **UserDefined**, abhängig von den Datentypen des UDTS.  
  
 **IsByteOrdered**  
 Ein **booleschen** Wert, der bestimmt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] binäre Vergleiche auf dem UDT ausführt.  
  
 **"IsFixedLength"**  
 Gibt an, ob alle Instanzen dieses UDTs dieselbe Länge haben.  
  
 **MaxByteSize**  
 Die maximale Größe der Instanz in Byte. Sie müssen angeben, **MaxByteSize** mit der **UserDefined** Serialisierungsformat. Bei einem UDT, der eine benutzerdefinierte Serialisierung festgelegt ist **MaxByteSize** bezieht sich auf die Gesamtgröße des UDTS in ihrem serialisierten Format als vom Benutzer definiert. Der Wert der **MaxByteSize** muss im Bereich von 1 und 8000 liegen, oder auf-1 festgelegt werden, um anzugeben, dass der UDT größer als 8000 Bytes ist (die Gesamtgröße darf nicht die maximale LOB-Größe überschreiten). Betrachten Sie einen UDT mit einer Eigenschaft eine Zeichenfolge von 10 Zeichen (**System.Char**). Wenn der UDT anhand eines BinaryWriter serialisiert wird, beträgt die Gesamtgröße der serialisierten Zeichenfolge 22 Byte: 2 Byte pro Unicode-UTF-16-Zeichen, multipliziert mit der maximalen Anzahl von Zeichen, plus 2 Kontrollzeichen, die beim Serialisieren eines binären Datenstroms zusätzlich anfallen. Deshalb beim Bestimmen des Wert der **MaxByteSize**, muss die Gesamtgröße des serialisierten UDT berücksichtigt werden: die Größe der ins Binärformat serialisierten Daten plus der bei der Serialisierung anfallenden.  
  
 **ValidationMethodName**  
 Der Name der Methode, mit der Instanzen des UDTs überprüft werden.  
  
### <a name="setting-isbyteordered"></a>Einstellung 'IsByteOrdered'  
 Wenn die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** -Eigenschaftensatz auf **"true"**, Sie sind sicher, dass die serialisierten Binärdaten für verwendet werden können semantische Sortierung der Informationen. So kann jede Instanz eines UDT-Objekts mit Bytereihenfolge nur eine einzige serialisierte Darstellung haben. Die Ausführung eines Vergleichsvorgangs für die serialisierten Bytes in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollte zu denselben Resultaten führen wie der entsprechende Vergleichsvorgang für verwalteten Code. Die folgenden Funktionen werden ebenfalls unterstützt, wenn **IsByteOrdered** festgelegt ist, um **"true"**:  
  
-   Die Fähigkeit zum Erstellen von Indizes für Spalten dieses Typs  
  
-   Die Fähigkeit, für Spalten dieses Typs Primär- und Fremdschlüssel sowie die Einschränkungen CHECK und UNIQUE zu erstellen  
  
-   Die Fähigkeit, [!INCLUDE[tsql](../../includes/tsql-md.md)]-ORDER BY-, GROUP BY- und PARTITION BY-Klauseln zu verwenden. In diesen Fällen wird die binäre Darstellung des Typs verwendet, um die Reihenfolge zu bestimmen  
  
-   Die Fähigkeit, Vergleichsoperatoren in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zu verwenden  
  
-   Die Fähigkeit, berechnete Spalten dieses Typs persistent zu speichern  
  
 Beachten Sie, dass sowohl die **Native** und **UserDefined** Serialisierungsformate unterstützen die folgenden Vergleichsoperatoren beim **IsByteOrdered** festgelegt ist, um **"true"** :  
  
-   Gleich (=)  
  
-   Ungleich (!=)  
  
-   Größer als (>)  
  
-   Kleiner als (\<)  
  
-   Größer als oder gleich (> =)  
  
-   Kleiner als oder gleich (<=)  
  
### <a name="implementing-nullability"></a>Implementieren von NULL-Zulässigkeit  
 Zusätzlich zum ordnungsgemäßen Angeben der Attribute für die Assemblys muss die Klasse auch NULL-Zulässigkeit unterstützen. UDTs geladenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Null-fähig ist, sind aber in der Reihenfolge der UDT einen Nullwert erkennt, muss die Klasse implementiert die **INullable** Schnittstelle. Weitere Informationen und ein Beispiel für das NULL-Zulässigkeit in einem UDT zu implementieren, finden Sie unter [Codieren benutzerdefinierter Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Zeichenfolgenkonvertierungen  
 Zur Unterstützung der zeichenfolgenkonvertierung in und aus UDTS müssen Sie angeben einer **analysieren** Methode und eine **ToString** Methode in Ihrer Klasse. Die **analysieren** -Methode ermöglicht es, eine Zeichenfolge in einen UDT konvertiert werden. Es muss deklariert werden, als **statische** (oder **Shared** in Visual Basic), und nehmen einen Versionsparameter vom Typ **System.Data.SqlTypes.SqlString**. Weitere Informationen und ein Beispiel zum Implementieren der **analysieren** und **ToString** Methoden, finden Sie unter [Codieren benutzerdefinierter Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>XML-Serialisierung  
 UDTs müssen unterstützen Konvertierung in und aus der **Xml** Datentyp durch, die den Vertrag für die XML-Serialisierung entsprechen. Die **System.Xml.Serialization** -Namespace enthält Klassen, die zur Serialisierung von Objekten in XML-Format Dokumente oder Streams im verwendet werden. Sie können wahlweise implementieren **Xml** Serialisierung mithilfe der **IXmlSerializable** -Schnittstelle, die benutzerdefinierte Formatierung für die XML-Serialisierung und Deserialisierung bereitstellt.  
  
 Zusätzlich zum Durchführen expliziter Konvertierungen von UDT in **Xml**, XML-Serialisierung können Sie:  
  
-   Verwendung **Xquery** für Werte von UDT-Instanzen nach der Konvertierung in den **Xml** -Datentyp.  
  
-   Verwenden von UDTs in parametrisierten Abfragen und Webmethoden mit systemeigenen XML-Webdiensten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Verwenden von UDTs, um ein Massenladen von XML-Daten durchzuführen.  
  
-   Serialisieren von DataSets, die Tabellen mit UDT-Spalten enthalten.  
  
 UDTs werden nicht in FOR XML-Abfragen serialisiert. Zum Ausführen einer FOR XML-Abfrage, die die XML-Serialisierung von UDTs anzeigt, konvertieren Sie explizit jede UDT-Spalte, die die **Xml** -Datentyp in der SELECT-Anweisung. Sie können die Spalten auch explizit konvertieren **Varbinary**, **Varchar**, oder **Nvarchar**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines benutzerdefinierten Typs](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
