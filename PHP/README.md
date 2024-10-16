# Página com exemplos simples e práticos

## Índice

  1. [Introdução](#introdução)
  2. [PDO](#pdo)
     * [Conexão com Banco de Dados](#conexao-com-banco-de-dados)


## Introdução

A ideia inicial é manter exemplos simples de codigos para uso com PHP. 

## PDO

### Conexão com Banco de Dados

**MySQL:**

```php
try {
    $pdo = new PDO('mysql:host=localhost;dbname=nome_banco', $usuario, $senha);
} catch(PDOException $e) {
    echo 'Erro na conexão com o banco de dados: <br>- ' . $e->getMessage();
    die();
}
```

**[⬆ retornar](#conexao_mysql)**

