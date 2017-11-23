---
title: Verwenden der adaptiven Pufferung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: "53"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4743d48d09625dd4ce1840b61abb58497057789d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="using-adaptive-buffering"></a>Verwenden der adaptiven Pufferung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Mit der adaptiven Pufferung können Daten mit großen Werten ohne den Aufwand von Servercursorn abgerufen werden. Anwendungen können die Funktion die adaptive Pufferung mit allen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , die vom Treiber unterstützt werden.  
  
 Normalerweise, wenn die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] eine Abfrage ausführt, ruft der Treiber alle Ergebnisse vom Server in einen Anwendungsspeicher. Obwohl dieser Ansatz die ressourcenauslastung für reduziert wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], es kann eine OutOfMemoryError auslösen, in der JDBC-Anwendung für die Abfragen, die sehr große Ergebnisse zurückgegeben.  
  
 Damit Anwendungen sehr große Ergebnisse behandeln können die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] stellt die adaptive Pufferung bereit. Mit adaptiver Pufferung ruft der Treiber Ergebnisse aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ab, wenn die Anwendung benötigt, anstatt alle auf einmal abzurufen. Der Treiber verwirft außerdem die Ergebnisse, sobald die Anwendung nicht mehr auf sie zugreifen kann. Im Folgenden werden einige Szenarien beschrieben, in denen die Verwendung der adaptiven Pufferung sinnvoll sein kann:  
  
-   **Die Abfrage erzeugt ein sehr umfangreiches Resultset:** Ausführen der Anwendung kann eine SELECT-Anweisung, die mehr Zeilen zurückgibt als die Anwendung im Arbeitsspeicher gespeichert werden können. In früheren Versionen musste die Anwendung einen Servercursor verwenden, um eine OutOfMemoryError zu vermeiden. Die adaptive Pufferung stellt die Möglichkeit bereit, ein beliebig großes Resultset mit Vorwärtscursor und schreibgeschützt zu übergeben, ohne dass ein Servercursor erforderlich ist.  
  
-   **Die Abfrage erzeugt sehr große**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**Spalten oder**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**OUT-Parameterwerte:**  Abrufen der Anwendung kann einen einzelnen Wert (Spalte oder OUT-Parameter), ist zu groß, um vollständig im Anwendungsspeicher gespeichert. Adaptive Pufferung kann die Clientanwendung solche Werte als einen Stream abrufen, indem Sie mit der GetAsciiStream, die GetBinaryStream oder die GetCharacterStream-Methoden. Die Anwendung ruft den Wert aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wie aus dem Stream gelesen.  
  
> [!NOTE]  
>  Mit adaptiver Pufferung puffert der JDBC-Treiber nur die benötigte Datenmenge. Der Treiber stellt keine öffentliche Methode zum Steuern oder Beschränken der Puffergröße bereit.  
  
## <a name="setting-adaptive-buffering"></a>Festlegen der adaptiven Pufferung  
 Ab JDBC Driver, Version 2.0, das Standardverhalten des Treibers ist "**adaptive**". Dies bedeutet, um das Verhalten der adaptiven Pufferung zu verwenden, muss das Verhalten der adaptiven Pufferung in der Anwendung nicht explizit angefordert werden. In Version 1.2, jedoch der pufferungsmodus lautete "**vollständige**" standardmäßig und die Anwendung hatte Modus für die adaptive Pufferung explizit anfordern.  
  
 Es gibt drei Möglichkeiten, mit denen eine Anwendung die Verwendung der adaptiven Pufferung für die Anweisungsausführung anfordern kann:  
  
-   Die Anwendung kann die Verbindungseigenschaft festlegen **ResponseBuffering** auf "adaptive". Weitere Informationen zum Festlegen der Verbindungseigenschaften finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
-   Können Sie die Anwendung die [SetResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) Methode der [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt, das den antwortpuffermodus für alle Verbindungen mit diesem erstellt festgelegt [ SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.  
  
-   Können Sie die Anwendung die [SetResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse, um den antwortpuffermodus für ein bestimmtes Anweisungsobjekt festzulegen.  
  
 Bei Verwendung von JDBC Driver, Version 1.2, mussten die umwandeln, um Anwendungen eine [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Klasse die [SetResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode. Die Codebeispiele in der [lesen großer Datenbeispiel](../../connect/jdbc/reading-large-data-sample.md) und [Lesen umfangreicher Daten mit gespeicherten Prozeduren Beispiel](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) veranschaulichen diese frühere Verwendungsweise.  
  
 Mit JDBC Driver, Version 2.0, Anwendungen können jedoch die [IsWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) Methode und die [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) Methode, um die herstellerspezifischen Funktionen ohne vermutungen über die Klassenhierarchie der Implementierung. Beispielcode hierzu finden Sie unter der [große Datenbeispiel aktualisieren](../../connect/jdbc/updating-large-data-sample.md) Thema.  
  
## <a name="retrieving-large-data-with-adaptive-buffering"></a>Abrufen umfangreicher Daten mit adaptiver Pufferung  
 Wenn große Werte einmal mithilfe der Get gelesen werden\<Typ > Stream-Methoden und die ResultSet-Spalten und die CallableStatement-OUT-Parameter erfolgt in der Reihenfolge zurückgegeben werden, indem Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], minimiert die adaptive Pufferung die Anwendung speicherauslastung beim Verarbeiten der Ergebnisse. Beim Verwenden der adaptiven Pufferung:  
  
-   Die Get\<Typ > Stream in definierte Methoden den [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) und [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Methoden geben schreibgeschützte Datenströme standardmäßig zurück, wenn zurückgesetzt werden können von der Anwendung gekennzeichnet. Wenn die Anwendung möchte `reset` zum Aufrufen der Stream verfügt über die `mark` -Methode für diesen Datenstrom zuerst.  
  
-   Die Get\<Typ > Stream in definierte Methoden den [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) und [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) -Methoden geben Datenströme, die immer neu angeordnet werden können an der Anfangsposition des Datenstroms ohne zurück. Aufrufen der `mark` Methode.  
  
 Wenn die Anwendung adaptive Pufferung verwendet werden, die Werte abgerufen, indem die Get\<Typ > Stream-Methoden können nur einmal abgerufen werden. Wenn Sie versuchen, rufen Sie alle Get\<Typ > Methode für die gleiche Spalte oder Parameter nach dem Aufrufen der Get\<Typ > Stream-Methode des gleichen Objekts, eine Ausnahme mit der folgenden Meldung ausgelöst wird, "die Daten zugegriffen wurde und ist nicht verfügbar für diesen Spalte oder Parameter".  
  
> [!NOTE]
> Ein Aufruf von ResultSet.close() während der Verarbeitung ein ResultSet, müsste die Microsoft JDBC Driver für SQL Server zu lesen und alle übrigen Pakete verwerfen. Dies kann längere Zeit dauern, wenn die Abfrage ein großes Dataset zurückgegeben, und insbesondere dann, wenn die Netzwerkverbindung langsam ist.     
  
## <a name="guidelines-for-using-adaptive-buffering"></a>Richtlinien für die Verwendung der adaptiven Pufferung  
 Entwickler sollten sich an diese wichtigen Richtlinien halten, um die Speicherauslastung durch die Anwendung zu minimieren:  
  
-   Vermeiden Sie die Verwendung der Verbindungszeichenfolgeneigenschaft **SelectMethod = Cursor** festzulegen, der die Anwendung ein sehr großes Resultset verarbeiten kann. Die adaptive Pufferung ermöglicht Anwendungen, sehr große, schreibgeschützte Vorwärtsresultsets ohne die Verwendung eines Servercursors zu verarbeiten. Beachten Sie, dass beim Festlegen der **SelectMethod = Cursor**, alle Vorwärtscursor, schreibgeschützte Resultsets, die über diese Verbindung generiert betroffen sind. Das heißt, wenn die Anwendung regelmäßig kleine Resultsets mit wenigen Zeilen verarbeitet, erstellen, lesen und Schließen eines Servercursors für jedes Resultset mehr Ressourcen für die clientseitige und serverseitige als wird die Groß-/Kleinschreibung verwendet, in denen die  **SelectMethod** nicht festgelegt ist, um **Cursor**.  
  
-   Lesen Sie große Text- oder Binärwerte als Datenströme mithilfe der GetAsciiStream, die GetBinaryStream oder die GetCharacterStream-Methoden anstelle der GetBlob oder die GetClob-Methoden. Beginnend mit der Version 1.2 der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse bietet neue Get\<Typ > Stream-Methoden für diesen Zweck.  
  
-   Stellen Sie sicher, dass Spalten mit potenziell großen Werten in der Liste der Spalten in einer SELECT-Anweisung und die letzten platziert werden Get\<Typ > Methoden der Stream den [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) werden verwendet, um den Zugriff auf die Spalten in der die Reihenfolge, die sie ausgewählt werden.  
  
-   Stellen Sie sicher, dass die OUT-Parameter mit potenziell großen Werten in der Liste der Parameter im SQL zum Erstellen verwendet zuletzt deklariert werden die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Darüber hinaus sicher, dass die Get\<Typ > Stream-Methoden von der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) werden verwendet, um die OUT-Parameter in der Reihenfolge zuzugreifen, sie deklariert werden.  
  
-   Vermeiden Sie, gleichzeitig mehrere Anweisungen über die gleiche Verbindung auszuführen. Das Ausführen einer weiteren Anweisung vor dem Verarbeiten der Ergebnisse der vorhergehenden Anweisung kann dazu führen, dass nicht verarbeitete Ergebnisse im Anwendungsspeicher gepuffert werden.  
  
-   Es gibt einige Fälle, die Verwendung **SelectMethod = Cursor** anstelle von **ResponseBuffering = adaptive** gegenüber, z. B. wäre:  
  
    -   Wenn Ihre Anwendung nur vorwärts verarbeiten, nur-Lese Resultset langsam, z. B. beim Lesen jeder Zeile nach einer Benutzereingabe, mit **SelectMethod = Cursor** anstelle von **ResponseBuffering = adaptive** möglicherweise Verringern der Ressourcenverwendung durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Wenn Ihre Anwendung zwei oder mehr Vorwärtscursor, schreibgeschützte Resultsets verarbeitet gleichzeitig über dieselbe Verbindung, **SelectMethod = Cursor** anstelle von **ResponseBuffering = adaptive** hilfreich sein Reduzieren Sie die vom Treiber bei der Verarbeitung dieser Resultsets benötigte Speicher.  
  
     In beiden Fällen müssen Sie den zusätzlichen Aufwand des Erstellens, Lesens und Schließens der Servercursor berücksichtigen.  
  
 Darüber hinaus enthält die folgende Liste einige Empfehlungen für scrollfähige Resultsets und aktualisierbare Resultsets mit Vorwärtscursor:  
  
-   Bei scrollfähigen Resultsets liest beim Abrufen eines Blocks von Zeilen des Treibers immer in den Arbeitsspeicher die angegebene Anzahl von Zeilen durch die [GetFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt, selbst wenn die Adaptive Pufferung ist aktiviert. Wenn ein OutOfMemoryError Durchführen eines Bildlaufs verursacht werden, können Sie die Anzahl der Zeilen, die durch den Aufruf abgerufen reduzieren die [SetFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt, das die Abrufgröße auf eine kleinere Zeilenanzahl festzulegen sogar auf 1 Zeile, falls erforderlich. Wenn dies ein OutOfMemoryError nicht verhindert wird, vermeiden Sie einschließen sehr großer Spalten in scrollfähigen Resultsets.  
  
-   Für nur vorwärts aktualisierbare Resultset mit Vorwärtscursor, liest beim Abrufen eines Blocks von Zeilen des Treibers normalerweise in den Arbeitsspeicher die angegebene Anzahl von Zeilen durch die [GetFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt selbst wenn die adaptive Pufferung für die Verbindung aktiviert ist. Beim Aufrufen der [Weiter](../../connect/jdbc/reference/next-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt ergibt ein OutOfMemoryError, reduzieren Sie die Anzahl der Zeilen, die durch den Aufruf abgerufen der [SetFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt, das die Abrufgröße auf eine kleinere Anzahl von Zeilen, sogar auf 1 Zeile bei Bedarf festgelegt. Sie können auch erzwingen, dass den Treiber keine Zeilen puffert, durch Aufrufen der [SetResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt mit "**adaptive**"-Parameter vor dem Ausführen der Anweisung an. Da das Resultset nicht scrollfähig ist, die Anwendung einen großen Spaltenwert zugreift, mit einem der Get ist\<Typ > Stream-Methoden, sobald die Anwendung einfach wie bei der Vorwärtscursor liest, verwirft der Treiber den Wert ohne Schreibzugriff Resultsets.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
