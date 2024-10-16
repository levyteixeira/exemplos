# Página com exemplos simples e práticos

## Índice

  1. [Introdução](#introducao)
  2. [Banco de Dados com PDO](#BDPDO)
     * [Conexão com o Banco de Dados](#use-conexao_mysql)


## Introdução

A ideia inicial é manter exemplos simples de codigos para uso com PHP. 

## Banco de Dados com PDO

### Conexão com o Banco de Dados

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
