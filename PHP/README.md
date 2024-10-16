# Página com exemplos simples e práticos

## Índice

  1. [Introdução](#introdução)
  2. [PDO](#pdo)
     * [Conexão com Banco de Dados](#conexao-com-banco-de-dados)
     * [Retornando dados](#retornando-dados)
     * [Manipulando dados](#manipulando-dados)


## Introdução

A ideia inicial é manter exemplos simples de codigos para uso com PHP. 

## PDO

### Conexão com Banco de Dados

**MySQL:**

Conexão com o banco de dados

```php
try {
    $pdo = new PDO('mysql:host=localhost;dbname=nome_banco', $usuario, $senha, array(PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES UTF8"));
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    $pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
} catch(PDOException $e) {
    echo 'Erro na conexão com o banco de dados: <br>- ' . $e->getMessage();
    die();
}
```

**[⬆ retornar](#conexao-com-banco-de-dados)**

### Retornando dados

Podemos retornar os dados linha a linha

```php
$retorno = $pdo->query("SELECT id, texto FROM tabela;");
while ($linha = $retorno->fetch()) 
{
    echo "id: {$linha['id']} - texto: {$linha['texto']}<br />";
}
```

Ou podemos retornar todos os registro para um array depois trabalhar os dados

```php
$stm = $pdo->query("SELECT id, texto FROM tabela;");
$retorno = $stm->fetchAll();
if (!empty($retorno)) {
    $total = count($retorno);
    for ($i=0; $i < $total; $i++) { 
        echo "id: {$retorno[$i]['id']} - texto: {$retorno[$i]['texto']}<br />";
    }
}

```

Filtrando dados 

```php
$id = 1;
$stm = $pdo->prepare('SELECT id, texto FROM tabela WHERE id = :id_registro;');
$stm->bindValue(':id_registro', $id, PDO::PARAM_INT);
$stm->execute();
$retorno = $stm->fetchAll();
```


**[⬆ retornar](#retornando-dados)**

### Manipulando dados

Inserindo dados

```php
$id_novo = 0;
$pdo->beginTransaction();
try {
    $texto = 'MAIS UM TEXTO';
    $stm = $pdo->prepare('INSERT INTO tabela (texto) VALUES(:texto)');
    $stm->bindParam(':texto', $texto, PDO::PARAM_STR);
    $stm->execute();    
    $id_novo = $pdo->lastInsertId();
    $pdo->commit();
} catch (\Throwable $th) {
    $pdo->rollback();
    echo 'Trate a mensagem de seu erro: <br>- ' . $th->getMessage();
    die();
}
```

Alterando dados

```php
$pdo->beginTransaction();
try {
    $id = 2;
    $texto = 'OUTRO TEXTO';
    $stm = $pdo->prepare('UPDATE tabela SET texto = :novo_texto WHERE id = :id;');
    $stm->bindParam(':id', $id, PDO::PARAM_INT);
    $stm->bindParam(':novo_texto', $texto, PDO::PARAM_STR);
    $stm->execute();    
    $pdo->commit();
} catch (\Throwable $th) {
    $pdo->rollback();
    echo 'Trate a mensagem de seu erro: <br>- ' . $th->getMessage();
    die();
}
```

Excluindo dados 

```php
$pdo->beginTransaction();
try {
    $id = 2;
    $stm = $pdo->prepare('DELETE FROM tabela WHERE id = :id;');
    $stm->bindParam(':id', $id, PDO::PARAM_INT);
    $stm->execute();    
    $pdo->commit();
} catch (\Throwable $th) {
    $pdo->rollback();
    echo 'Trate a mensagem de seu erro: <br>- ' . $th->getMessage();
    die();
}
```

**[⬆ retornar](#manipulando-dados)**
