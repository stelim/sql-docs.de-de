---
title: Konfigurieren des Clients für SSL-Verschlüsselung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d80c9d8103e7a0a0eeea766487e1fc013ae5e100
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726628"
---
# <a name="configuring-the-client-for-ssl-encryption"></a>Konfigurieren des Clients für SSL-Verschlüsselung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oder Client muss überprüfen, ob es sich bei dem Server um den richtigen Server handelt und das Serverzertifikat von einer Zertifizierungsstelle herausgegeben wurde, der der Client vertraut. Zum Überprüfen des Serverzertifikats müssen die Informationen zur Vertrauenswürdigkeit zur Verbindungszeit angegeben werden. Außerdem muss der Aussteller des Serverzertifikats eine Zertifizierungsstelle sein, der der Client vertraut.  
  
 In diesem Thema wird zuerst beschrieben, wie die Vertrauenswürdigkeitsinformationen auf dem Clientcomputer angegeben werden. Anschließend wird das Importieren eines Serverzertifikats in den Vertrauensspeicher des Clientcomputers erläutert, wenn die Instanz des Secure Sockets Layer (SSL)-Zertifikats von SQL Server von einer privaten Zertifizierungsstelle veröffentlicht wird.  
  
 Weitere Informationen zum Überprüfen des Serverzertifikats finden Sie im Abschnitt zum Überprüfen des SSL-Serverzertifikats unter [Grundlegendes zur SSL-Unterstützung](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Konfigurieren des Clientvertrauensspeichers  
 Damit das Serverzertifikat überprüft werden kann, müssen die Vertrauensinformationen zur Verbindungszeit explizit mithilfe der **trustStore**- und **trustStorePassword**-Verbindungseigenschaft oder implizit mithilfe des Standardvertrauensspeichers der zugrunde liegenden Java Virtual Machine (JVM) übermittelt werden. Weitere Informationen zum Festlegen der **trustStore**- und **trustStorePassword**-Eigenschaft in einer Verbindungszeichenfolge finden Sie unter [Verbinden mit SSL-Verschlüsselung](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Wenn die **trustStore**-Eigenschaft nicht angegeben oder auf NULL festgelegt ist, verwendet [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] den Sicherheitsanbieter der zugrunde liegenden JVM, d. h. Java Secure Socket Extension (SunJSSE). Der SunJSSE-Anbieter stellt einen Standard-TrustManager bereit. Hiermit werden die von SQL Server zurückgegebenen X.509-Zertifikate anhand der in einem Vertrauensspeicher bereitgestellten Vertrauensinformationen überprüft.  
  
 Der TrustManager versucht, den Standard-trustStore in der folgenden Suchreihenfolge zu suchen:  
  
-   Wenn die Systemeigenschaft „javax.net.ssl.trustStore“ definiert ist, versucht TrustManager, die standardmäßige trustStore-Datei anhand des von der Systemeigenschaft angegebenen Dateinamens zu suchen.  
  
-   Wenn die Systemeigenschaft „javax.net.ssl.trustStore“ nicht angegeben wurde und die Datei „\<java-home>/lib/security/jssecacerts“ vorhanden ist, wird diese Datei verwendet.  
  
-   Wenn die Datei „\<java-home>/lib/security/cacerts“ vorhanden ist, wird diese Datei verwendet.  
  
 Weitere Informationen finden Sie in der Dokumentation zur SUNX509 TrustManager-Schnittstelle auf der Sun Microsystems-Website.  
  
 Durch die Java Runtime-Umgebung können Sie die trustStore-Systemeigenschaft und die trustStorePassword-Systemeigenschaft wie folgt festlegen:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 In diesem Fall verwenden alle Anwendungen, die auf dieser JVM ausgeführt werden, diese Einstellungen als Standard. Zum Überschreiben der Standardeinstellungen in Ihrer Anwendung sollten Sie die **trustStore**- und **trustStorePassword**-Verbindungseigenschaft in der Verbindungszeichenfolge oder in der entsprechenden Festlegungsmethode der [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)-Klasse festlegen.  
  
 Außerdem können Sie die Standardvertrauensspeicherdateien wie „\<java-home>/lib/security/jssecacerts“ und „\<java-home>/lib/security/cacerts“ konfigurieren und verwalten. Verwenden Sie hierzu das JAVA-Hilfsprogramm "keytool", das mit der JRE (Java Runtime Environment) installiert wird. Weitere Informationen zum Hilfsprogramm "keytool" finden Sie in der Dokumentation zu keytool auf der Sun Microsystems-Website.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importieren des Serverzertifikats in den Vertrauensspeicher  
 Während des SSL-Handshakes sendet der Server sein Zertifikat für öffentliche Schlüssel an den Client. Der Aussteller eines Zertifikats für öffentliche Schlüssel wird als Zertifizierungsstelle bezeichnet. Der Client muss sicherstellen, dass der Client der Zertifizierungsstelle vertraut. Dies wird erreicht, indem der öffentliche Schlüssel von vertrauenswürdigen Zertifizierungsstellen im Voraus bekannt ist. Normalerweise wird die JVM mit einem vordefinierten Satz vertrauenswürdiger Zertifizierungsstellen geliefert.  
  
 Wenn die Instanz des Secure Sockets Layer (SSL)-Zertifikats von SQL Server von einer privaten Zertifizierungsstelle veröffentlicht wird, müssen Sie das Zertifikat der Zertifizierungsstelle der Liste der vertrauenswürdigen Zertifikate im Vertrauensspeicher des Clientcomputers hinzufügen.  
  
 Verwenden Sie hierzu das JAVA-Hilfsprogramm „keytool“, das mit der JRE (Java Runtime Environment) installiert wird. Mit der folgenden Eingabeaufforderung wird die Verwendung des Hilfsprogramms "keytool" zum Importieren eines Zertifikats aus einer Datei veranschaulicht:  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 Im Beispiel wird die Datei "caCert.cer" als Zertifikatsdatei verwendet. Sie müssen diese Zertifikatsdatei vom Server abrufen. In den folgenden Schritten wird erläutert, wie das Serverzertifikat in eine Datei exportiert wird:  
  
1.  Klicken Sie auf Start, klicken Sie auf Ausführen, und geben Sie MMC ein. (MMC ist die Abkürzung für Microsoft Management Console.)  
  
2.  Öffnen Sie in MMC die Zertifikate.  
  
3.  Erweitern Sie Eigene Zertifikate und dann Zertifikate.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Serverzertifikat, und wählen Sie dann unter Alle Aufgaben die Option Exportieren aus.  
  
5.  Klicken Sie auf Weiter, um das Dialogfeld Willkommen des Zertifikatexport-Assistenten zu überspringen.  
  
6.  Stellen Sie sicher, dass "Nein, privaten Schlüssel nicht exportieren" ausgewählt ist, und klicken Sie dann auf Weiter.  
  
7.  Stellen Sie sicher, dass DER-codiert-binär X.509 (.CER) oder Base-64-codiert X.509 (.CER) ausgewählt ist, und klicken Sie dann auf Weiter.  
  
8.  Geben Sie einen Namen für die Exportdatei ein.  
  
9. Klicken Sie auf Weiter, und klicken Sie dann auf Fertig stellen, um das Zertifikat zu exportieren.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Using SSL Encryption (Verwenden der SSL-Verschlüsselung)](../../connect/jdbc/using-ssl-encryption.md)   
 [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
