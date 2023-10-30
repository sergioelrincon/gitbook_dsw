# Manejo de bases de datos

## Recursos

* [Tipos de datos MySQL](https://www.w3schools.com/mysql/mysql\_datatypes.asp)
* [Manejo de excepciones en PHP](https://www.w3schools.com/php/php\_exceptions.asp)
* [setattribute()](https://www.php.net/manual/es/pdo.setattribute.php)

## Contenidos

* [Manejo de BBDD MySQL en PHP](https://www.w3schools.com/php/php\_mysql\_intro.asp)
* MySQLi - PDO
  * [Conexión](https://www.w3schools.com/php/php\_mysql\_connect.asp)
  * [Inserción](https://www.w3schools.com/php/php\_mysql\_insert.asp)
  *   Consulta

      ```php
      $stmt = $pdo->query("SELECT * FROM users");
      while ($row = $stmt->fetch()) {
          echo $row['name']."<br />\n";
      }
      ```

      * [PDO::query()](https://www.php.net/manual/es/pdo.query.php)
      * [PDO::fetch()](https://www.php.net/manual/es/pdostatement.fetch.php)
      *   [PDO::fetchAll()](https://www.php.net/manual/es/pdostatement.fetchall.php)

          ```php
          $data = $pdo->query("SELECT * FROM users")->fetchAll();
          // and somewhere later:
          foreach ($data as $row) {
              echo $row['name']."<br />\n";
          }
          ```
  * [Eliminación](https://www.w3schools.com/php/php\_mysql\_delete.asp)
  * [Modificación](https://www.w3schools.com/php/php\_mysql\_update.asp)
