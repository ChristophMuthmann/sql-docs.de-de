---
title: Wrapper und Schnittstellen | Microsoft Docs
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
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b0dc608dc62db0f8f06092843c0c2a0e7b747ca
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="wrappers-and-interfaces"></a>Wrapper und Schnittstellen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt Schnittstellen, mit denen Sie einen Proxy einer Klasse erstellen können, sowie Wrapper, mit denen Sie den Zugriff auf Erweiterungen der JDBC-API, die spezifisch für die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] über eine Proxyschnittstelle.  
  
## <a name="wrappers"></a>Wrapper  
 Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die java.sql.Wrapper-Schnittstelle. Diese Schnittstelle bietet einen Mechanismus für den Zugriff auf Erweiterungen, die für spezifischen JDBC-API die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] über eine Proxyschnittstelle.  
  
 Die java.sql.Wrapper-Schnittstelle sind zwei Methoden definiert: **IsWrapperFor** und **unwrap**. Die **IsWrapperFor** Methode überprüft, ob das angegebene Eingabeobjekt diese Schnittstelle implementiert. Die **unwrap** Methode gibt ein Objekt, das implementiert diese Schnittstelle, um Zugriff auf die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] spezifischen Methoden.  
  
 **IsWrapperFor** und **unwrap** -Methoden werden folgendermaßen verfügbar gemacht:  
  
-   [IsWrapperFor-Methode &#40; SQLServerCallableStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [Unwrap-Methode &#40; SQLServerCallableStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [IsWrapperFor-Methode &#40; SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [Unwrap-Methode &#40; SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [IsWrapperFor-Methode &#40; SQLServerDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [Unwrap-Methode &#40; SQLServerDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [IsWrapperFor-Methode &#40; SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [Unwrap-Methode &#40; SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [IsWrapperFor-Methode &#40; SQLServerStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [Unwrap-Methode &#40; SQLServerStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [IsWrapperFor-Methode &#40; SQLServerXADataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [Unwrap-Methode &#40; SQLServerXADataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>Schnittstellen  
 Ab [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0, stehen die Schnittstelle für einen Anwendungsserver, auf eine treiberspezifische Methode über die zugehörige Klasse zuzugreifen. Der Anwendungsserver kann die Klasse durch Erstellen eines Proxy, Verfügbarmachen von umschließen die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]--spezifische Funktionen über eine Schnittstelle. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt Schnittstellen, haben die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] -spezifischen Methoden und Konstanten, sodass ein Anwendungsserver einen Proxy der Klasse erstellen kann.  
  
 Die Schnittstellen sind von Java-Standardschnittstellen, damit Sie das gleiche Objekt verwenden können, sobald er Zugriff auf entwrappt treiberspezifischen Funktionen oder generisch ist abgeleitet [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Funktionalität.  
  
 Die folgenden Schnittstellen wurden hinzugefügt:  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>Beispiel  
  
### <a name="description"></a>Description  
 In diesem Beispiel wird veranschaulicht, wie der Zugriff auf eine [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]--spezifische Funktion über ein DataSource-Objekt. Diese Klasse DataSource möglicherweise von einem Anwendungsserver umschlossen sein. Sie können Zugriff auf die JDBC-Treiber-spezifische Funktion oder Konstante Entpacken die Datenquelle in eine ISQLServerDataSource-Schnittstelle und verwenden Sie die Funktionen, die in dieser Schnittstelle deklariert.  
  
### <a name="code"></a>Code  
  
```  
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver   
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  
  
   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  
  
         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  
  
      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
