---
title: Implementierung von Unicode-Komprimierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2637e6c503a5272ff7f4e1f6bc224ecb4449bbd6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633068"
---
# <a name="unicode-compression-implementation"></a>Implementierung von Unicode-Komprimierung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet eine Implementierung des Algorithmus „Standardkomprimierungsschema für Unicode (SCSU)“, um Unicode-Werte zu komprimieren, die in zeilen- oder seitenkomprimierten Objekten gespeichert werden. Für diese komprimierten Objekte erfolgt die Unicode-Komprimierung für **nchar(n)** - und **nvarchar(n)** -Spalten automatisch. [!INCLUDE[ssDE](../../includes/ssde-md.md)] speichert Unicode-Daten als 2 Bytes, unabhängig vom Gebietsschema. Dies wird UCS-2-Codierung genannt. Bei einigen Gebietsschemas kann durch die Implementierung der SCSU-Komprimierung in SQL Server bis zu 50 Prozent des Speicherplatzes eingespart werden.  
  
## <a name="supported-data-types"></a>Unterstützte Datentypen  
 Unicode-Komprimierung unterstützt den **nchar(n)** -Datentyp mit fester Länge und den **nvarchar(n)** -Datentyp. Datenwerte, die außerhalb von Zeilen oder in **nvarchar(max)** -Spalten gespeichert werden, werden nicht komprimiert.  
  
> [!NOTE]  
>  Unicode-Komprimierung wird nicht für **nvarchar(max)** -Daten unterstützt, auch wenn sie in Zeile gespeichert wird. Dieser Datentyp kann immer noch jedoch von der Seitenkomprimierung profitieren.  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>Aktualisieren von früheren Versionen von SQL Server  
 Wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aktualisiert wird, werden keine Änderungen im Zusammenhang mit Unicode-Komprimierung für die Datenbankobjekte durchgeführt – unabhängig davon, ob diese komprimiert oder unkomprimiert sind. Das Datenbankupgrade wirkt sich wie folgt auf Objekte aus:  
  
-   Wenn das Objekt nicht komprimiert ist, werden keine Änderungen durchgeführt, und das Objekt funktioniert wie bisher.  
  
-   Zeilen- oder seitenkomprimierte Objekte funktionieren wie bisher. Unkomprimierte Daten liegen in unkomprimierter Form vor, bis ihr Wert aktualisiert wird.  
  
-   Neue Zeilen, die in eine zeilen- oder seitenkomprimierte Tabelle eingefügt werden, werden mittels Unicode-Komprimierung komprimiert.  
  
    > [!NOTE]  
    >  Um die Vorteile der Unicode-Komprimierung in vollem Umfang zu nutzen, muss das Objekt mit Seiten- oder Zeilenkomprimierung neu erstellt werden.  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Auswirkungen der Unicode-Komprimierung auf Datenspeicher  
 Wenn ein Index erstellt wird oder neu erstellt wird oder wenn ein Wert in einer Tabelle geändert wird, die mit Zeilen- oder Seitenkomprimierung komprimiert wurde, wird der betroffene Index oder Wert nur dann komprimiert gespeichert, wenn die komprimierte Größe kleiner als die aktuelle Größe ist. Dies verhindert, dass Zeilen in einer Tabelle oder in einem Index aufgrund der Unicode-Komprimierung an Größe zunehmen.  
  
 Der Speicherplatz, der durch die Komprimierung eingespart wird, ist von den Eigenschaften der Daten abhängig, die komprimiert werden, und vom Gebietsschema der Daten. In der folgenden Tabelle werden die Speicherplatzeinsparungen aufgelistet, die für verschiedene Gebietsschemas erreicht werden können.  
  
|Gebietsschema|Komprimierung in Prozent|  
|------------|-------------------------|  
|Englisch|50%|  
|Deutsch|50%|  
|Hindi|50%|  
|Türkisch|48%|  
|Vietnamesisch|39%|  
|Japanisch|15%|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)   
 [Implementierung von Seitenkomprimierung](../../relational-databases/data-compression/page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql.md)  
  
  
