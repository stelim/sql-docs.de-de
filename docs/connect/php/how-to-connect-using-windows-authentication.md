---
title: 'Vorgehensweise: Herstellen einer Verbindung mit der Windows-Authentifizierung | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c78506897432cdbfa4f4dd926e3f6035fb1881f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759944"
---
# <a name="how-to-connect-using-windows-authentication"></a>Vorgehensweise: Herstellen einer Verbindung mithilfe der Windows-Authentifizierung
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Standardmäßig verwenden die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] für die Verbindung zu SQL Server die Windows-Authentifizierung. Es ist wichtig zu beachten, dass dies in den meisten Szenarien bedeutet, dass die Prozess- oder Threadidentität des Servers (falls der Webserver Identitätswechsel verwendet) dazu verwendet wird, sich mit dem Server und nicht mit der Identität des Endbenutzers zu verbinden.  
  
Bitte beachten Sie die folgenden Punkte, wenn Sie die Windows-Authentifizierung verwenden, um eine Verbindung mit einem SQL Server herzustellen:  
  
-   Die Anmeldeinformationen, unter denen der Webserverprozess (oder Thread) läuft, müssen einer gültigen SQL Server-Anmeldung zugeordnet sein, um eine Verbindung herstellen zu können.  
  
-   Wenn sich SQL Server und der Webserver auf unterschiedlichen Computern befinden, müssen für SQL Server Remoteverbindungen aktiviert sein.  
  
> [!NOTE]  
> Sie können Verbindungsattribute wie z. B. *Database* und *ConnectionPooling* festlegen, wenn Sie eine Verbindung herstellen. Eine vollständige Liste der unterstützten Verbindungsattribute finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
  
Aus folgenden Gründen sollte, wann immer möglich, die Windows-Authentifizierung für die Verbindung zu SQL Server verwendet werden:  
  
-   Während der Authentifizierung werden keine Anmeldeinformationen über das Netzwerk übergeben. Benutzernamen und Kennwörter werden nicht in die Verbindungszeichenfolge der Datenbank eingebettet. Dies bedeutet, dass böswillige Benutzer oder Angreifer die Anmeldeinformationen nicht durch Überwachen des Netzwerks oder durch Einsehen der Verbindungszeichenfolgen in Konfigurationsdateien erhalten können.  
  
-   Die Benutzer werden über ein zentrales Kontenmanagement verwaltet. Sicherheitsrichtlinien wie z. B. Gültigkeitszeiträume für Passwörter, Vorgaben zur Mindestlänge von Passwörtern und die Sperrung von Konten nach mehreren ungültigen Anmeldeanfragen werden umgesetzt.  
  
Wenn die Windows-Authentifizierung für Sie nicht praktikabel ist, lesen Sie [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird bei Verwendung des SQLSRV-Treibers von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]die Windows-Authentifizierung verwendet, um eine Verbindung mit einer lokalen SQL Server-Instanz herzustellen. Nach dem Aufbau der Verbindung wird eine Anfrage an den Benutzer gestellt, den Benutzer anzumelden, der auf die Datenbank zugreifen möchte.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über den Browser ausgeführt wird, werden alle Ausgaben im Browser geschrieben.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel verwendet den PDO_SQLSRV-Treiber, um dasselbe Ergebnis zu erreichen wie das vorherige Beispiel.  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Gewusst wie: Herstellen einer Verbindung mithilfe der SQL Server-Authentifizierung](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)

[Vorgehensweise: Erstellen einer SQL Server-Anmeldung](../../relational-databases/security/authentication-access/create-a-login.md)

[Vorgehensweise: Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Verwalten von Benutzern, Rollen und Anmeldungen](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Trennung von Benutzer und Schema](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Objektberechtigungen vergeben (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
