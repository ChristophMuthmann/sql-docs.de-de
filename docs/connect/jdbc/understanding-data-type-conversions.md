---
title: Grundlegendes zu Datentypkonvertierungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e18bd56e110cccab17488de752ba5ab4c8666fa9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-data-type-conversions"></a>Grundlegendes zu Datentypkonvertierungen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zur Erleichterung der Konvertierung von Java-Datentypen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] stellt datentypkonvertierungen gemäß der JDBC-Spezifikation bereit. Alle Typen sind in verschiedene andere und aus Flexibilität **Objekt**, **Zeichenfolge**, und **Byte []** -Datentypen.  
  
## <a name="getter-method-conversions"></a>Konvertierungen für Abrufmethoden  
 Basierend auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentypen, das folgende Diagramm enthält konvertierungsschema des JDBC-Treibers, für die Get\<Typ > ()-Methode, der die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse und die unterstützten Konvertierungen für die Get-\< Typ > Methoden der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse.  
  
 ![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")  
  
 Von den Abrufmethoden des JDBC-Treibers werden drei Konvertierungskategorien unterstützt:  
  
-   **Non-Lossy (X)**: Konvertierungen für Fälle, in denen die Getter-Typ dem entspricht, oder kleiner als die zugrunde liegenden Servertyp. Beispielsweise ist beim Aufruf von GetBigDecimal für eine zugrunde liegende dezimale Serverspalte keine Konvertierung erforderlich.  
  
-   **Konvertierte (y)**: Konvertierungen von numerischen Servertypen zu Java-Typen, in denen die Konvertierung ist regulär und Konvertierungsregeln von Java-Konvertierung. Bei diesen Konvertierungen wird die Genauigkeit gekürzt (niemals gerundet), und der Überlauf wird als Modulo des Zieltyps behandelt, der kleiner ist. Aufrufen z. B. für eine zugrunde liegende GetInt **decimal** Spalte, die von "1,9999" zurück "1", oder, wenn die zugrunde liegende **decimal** Wert ist "3000000000" wird das **Int** Wert führt zu einem Überlauf "-1294967296".  
  
-   **Data Dependent (Z)**: Konvertierungen von zugrunde liegenden Datentypen in numerische Typen müssen die Zeichentypen Werte enthalten, die in den betreffenden Typ konvertiert werden kann. Andere Konvertierungen werden nicht ausgeführt. Werte, die für den Abruftyp zu groß sind, sind ungültig. Z. B. wenn GetInt für eine varchar(50)-Spalte, die "53" enthält aufgerufen wird, der Wert wird als zurückgegeben ein **Int**; aber wenn der zugrunde liegenden Wert "Xyz" oder "3000000000" ist, wird ein Fehler ausgelöst.  
  
 Wenn GetString aufgerufen wird, auf eine **binäre**, **Varbinary**, **varbinary(max)**, oder **Image** Spaltendatentyp, als der Wert zurückgegeben wird ein hexadezimaler Zeichenfolgenwert.  
  
## <a name="updater-method-conversions"></a>Konvertierungen für Updatemethoden  
 Für die Java-, die übergeben werden, um das Update Typdaten\<Typ > ()-Methode, der die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) -Klasse, gelten die folgenden Konvertierungen.  
  
 ![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")  
  
 Von den Updatemethoden des JDBC-Treibers werden drei Konvertierungskategorien unterstützt:  
  
-   **Non-Lossy (X)**: Konvertierungen für Fälle, in denen der Aktualisierungstyp gleich ist, oder kleiner als die zugrunde liegenden Servertyp. Beim Aufruf von updateBigDecimal für eine zugrunde liegende dezimale Serverspalte ist beispielsweise keine Konvertierung erforderlich.  
  
-   **Konvertierte (y)**: Konvertierungen von numerischen Servertypen zu Java-Typen, in denen die Konvertierung ist regulär und Konvertierungsregeln von Java-Konvertierung. Bei diesen Konvertierungen wird die Genauigkeit gekürzt (niemals gerundet), und der Überlauf wird als Modulo des (kleineren) Zieltyps behandelt. Aufrufen z. B. für eine zugrunde liegende UpdateDecimal **Int** Spalte, die von "1,9999" zurück "1", oder, wenn das zugrunde liegende **decimal** Wert ist "3000000000" wird das **Int**Wert führt zu einem Überlauf "-1294967296".  
  
-   **Data Dependent (Z)**: Konvertierungen von zugrunde liegenden Quelldatentypen zu Zieldatentypen müssen die enthaltenen Werte zu den Zieltypen konvertiert werden können. Andere Konvertierungen werden nicht ausgeführt. Werte, die für den Abruftyp zu groß sind, sind ungültig. Beispielsweise wird das Update bei einem Aufruf von updateString für eine int-Spalte, die "53" enthält, erfolgreich ausgeführt. Bei einem zugrunde liegenden String-Wert von "foo" oder "3000000000" wird ein Fehler ausgelöst.  
  
 Wenn UpdateString aufgerufen wird, auf eine **binäre**, **Varbinary**, **varbinary(max)**, oder **Image** den Datentyp, den Zeichenfolgenwert behandelt als hexadezimale Zeichenfolge zurück.  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Spaltendatentyp ist **XML**, das dem Datenwert muss ein gültiger **XML**. Beim UpdateBytes, UpdateBinaryStream oder UpdateBlob-Methoden aufrufen, sollte der Datenwert die hexadezimale Zeichenfolgendarstellung der XML-Zeichen sein. Beispiel:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Beachten Sie, dass eine Bytereihenfolge-Marke (BOM) erforderlich ist, wenn die XML-Zeichen in einer bestimmten Zeichencodierung vorliegen.  
  
## <a name="setter-method-conversions"></a>Konvertierungen für Festlegungsmethoden  
 Für die Java-, die übergeben werden, auf den Satz Typdaten\<Typ > ()-Methode, der die [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse und die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Klasse, gelten die folgenden Konvertierungen.  
  
 ![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")  
  
 Der Server versucht alle Konvertierungen und gibt bei Fehlern eine Fehlermeldung zurück.  
  
 Im Fall von der **Zeichenfolge** -Datentyp, wenn der Wert die Länge von überschreitet **VARCHAR**, ordnet ihn **LONGVARCHAR**. Auf ähnliche Weise **NVARCHAR** ordnet **LONGNVARCHAR** überschreitet der Wert die Länge von **NVARCHAR**. Dasselbe gilt für **Byte []**. Werte, die länger als **VARBINARY** werden **"LONGVARBINARY"**.  
  
 Von den Festlegungsmethoden des JDBC-Treibers werden zwei Konvertierungskategorien unterstützt:  
  
-   **Non-Lossy (X)**: Konvertierungen für numerische Fälle, wobei der Setter gleich ist, oder kleiner als die zugrunde liegenden Servertyp. Beispielsweise wird beim Aufrufen von SetBigDecimal für eine zugrunde liegende **decimal** Spalte ist keine Konvertierung erforderlich. Für die numerischen Typen in Zeichentypen wird der Java **numerischen** -Datentyp in konvertiert eine **Zeichenfolge**. Aufrufen von für eine varchar(50)-Spalte, SetDouble mit dem Wert "53" erzeugt z. B. einen Zeichenwert "53" in dieser Spalte "Ziel".  
  
-   **Konvertierte (y)**: Konvertierungen eines-Java **numerischen** Typ in einen zugrunde liegenden **numerischen** Typ, der kleiner ist. Diese Konvertierung ist regulär und erfolgt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] entsprechend den-konvertierungskonventionen. Die Genauigkeit gekürzt (niemals gerundet) und Überlauf löst einen Fehler für die Konvertierung nicht unterstützt. Verwenden z. B. UpdateDecimal mit einem Wert von "1,9999" für eine zugrunde liegende Integer-Ergebnisse für die Spalte in "1" in Spalte "Ziel"; Wenn "3000000000" übergeben wird, löst der Treiber jedoch einen Fehler.  
  
-   **Data Dependent (Z)**: Konvertierungen eines-Java **Zeichenfolge** zu den zugrunde liegenden Typ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp unterliegen den folgenden Bedingungen: der Treiber sendet die **Zeichenfolge** Wert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] führt Konvertierungen, bei Bedarf. Wenn SendStringParametersAsUnicode auf "true" und dem zugrunde liegenden festgelegt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentyp **Image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] lässt keine Konvertierung von **Nvarchar** auf **Image** und löst eine SQLServerException aus. Wenn SendStringParametersAsUnicode auf "false" und dem zugrunde liegenden festgelegt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentyp **Image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ermöglicht das Konvertieren von **Varchar** auf **Image**und löst keine Ausnahme.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] führt die Konvertierungen aus und übergibt Fehler bei Problemen wieder an den JDBC-Treiber.  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Spaltendatentyp ist **XML**, das dem Datenwert muss ein gültiger **XML**. Beim UpdateBytes, UpdateBinaryStream oder UpdateBlob-Methoden aufrufen, sollte der Datenwert die hexadezimale Zeichenfolgendarstellung der XML-Zeichen sein. Beispiel:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Beachten Sie, dass eine Bytereihenfolge-Marke (BOM) erforderlich ist, wenn die XML-Zeichen in einer bestimmten Zeichencodierung vorliegen.  
  
## <a name="conversions-on-setobject"></a>Konvertierungen für setObject  
  
> [!NOTE]  
>  Microsoft JDBC Drivers 4.2 (und höher) für SQL Server JDBC 4.1 und 4.2 unterstützt. Weitere Details zu den Versionen 4.1 und 4.2 datentypzuordnungen und-Konvertierungen finden Sie unter [JDBC 4.1-Kompatibilität für JDBC Driver](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) und [JDBC 4.2-Kompatibilität für JDBC Driver](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), zusätzlich zu den folgenden Informationen.  
  
 Für die Java-, die an die SetObject übergeben Typdaten (\<Typ >) Methoden der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -Klasse, gelten die folgenden Konvertierungen.  
  
 ![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")  
  
 Die SetObject-Methode, wenn Sie keine Angabe eines Zieltyps verwendet die standardzuordnung. Im Fall von der **Zeichenfolge** -Datentyp, wenn der Wert die Länge von überschreitet **VARCHAR**, ordnet ihn **LONGVARCHAR**. Auf ähnliche Weise **NVARCHAR** ordnet **LONGNVARCHAR** überschreitet der Wert die Länge von **NVARCHAR**. Dasselbe gilt für **Byte []**. Werte, die länger als **VARBINARY** werden **"LONGVARBINARY"**.  
  
 Von den setObject-Methoden des JDBC-Treibers werden drei Konvertierungskategorien unterstützt:  
  
-   **Non-Lossy (X)**: Konvertierungen für numerische Fälle, wobei der Setter gleich ist, oder kleiner als die zugrunde liegenden Servertyp. Beispielsweise wird beim Aufrufen von SetBigDecimal für eine zugrunde liegende **decimal** Spalte ist keine Konvertierung erforderlich. Für die numerischen Typen in Zeichentypen wird der Java **numerischen** -Datentyp in konvertiert eine **Zeichenfolge**. Aufrufen von für eine varchar(50)-Spalte, SetDouble mit dem Wert "53" erzeugt z. B. einen Zeichenwert "53" in dieser Spalte "Ziel".  
  
-   **Konvertierte (y)**: Konvertierungen eines-Java **numerischen** Typ in einen zugrunde liegenden **numerischen** Typ, der kleiner ist. Diese Konvertierung ist regulär und erfolgt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] entsprechend den-konvertierungskonventionen. Die Genauigkeit wird immer gekürzt (niemals gerundet). Bei einem Überlauf wird der Fehler ausgegeben, dass die Konvertierung nicht unterstützt wird. Verwenden z. B. UpdateDecimal mit einem Wert von "1,9999" für eine zugrunde liegende Integer-Ergebnisse für die Spalte in "1" in Spalte "Ziel"; Wenn "3000000000" übergeben wird, löst der Treiber jedoch einen Fehler.  
  
-   **Data Dependent (Z)**: Konvertierungen eines-Java **Zeichenfolge** zu den zugrunde liegenden Typ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp unterliegen den folgenden Bedingungen: der Treiber sendet die **Zeichenfolge** Wert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] führt Konvertierungen, bei Bedarf. Wenn die SendStringParametersAsUnicode-Verbindungseigenschaft auf "true" und dem zugrunde liegenden festgelegt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentyp **Image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] lässt keine Konvertierung von in **Nvarchar** auf **Image** und löst eine SQLServerException aus. Wenn SendStringParametersAsUnicode auf "false" und dem zugrunde liegenden festgelegt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentyp **Image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ermöglicht das Konvertieren von **Varchar** auf **Image**und löst keine Ausnahme.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Führt den Großteil der festlegungskonvertierungen aus und übergibt Fehler bei Problemen wieder an den JDBC-Treiber. Clientseitige Konvertierungen sind die Ausnahme und werden nur im Fall von ausgeführt **Datum**, **Zeit**, **Zeitstempel**, **booleschen**, und  **Zeichenfolge** Werte.  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Spaltendatentyp ist **XML**, das dem Datenwert muss ein gültiger **XML**. Beim Aufrufen der Methoden setObject(byte[], SQLXML), setObject(inputStream, SQLXML) oder setObject(Blob, SQLXML) sollte der Datenwert die hexadezimale Zeichenfolgendarstellung der XML-Zeichen sein. Beispiel:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Beachten Sie, dass eine Bytereihenfolge-Marke (BOM) erforderlich ist, wenn die XML-Zeichen in einer bestimmten Zeichencodierung vorliegen.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
