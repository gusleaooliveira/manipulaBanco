# Usando o Manipula Banco

Para usar esse "framework" primeiramente baixe o código clicando [aqui](https://gusleaooliveira.github.io/manipulaBanco/Banco.class.php).

Caso esteja usando o linux e queira usar via terminal execute:
```bash
wget -c https://gusleaooliveira.github.io/manipulaBanco/Banco.class.php
```

Para executar faça a requisição do arquivo:
```php
require_once('Banco.class.php');
```

Instancie o banco da seguinte maneira:

```php
$servidor = "localhost";
$banco = "api_mrconstrucoes";
$usuario = "root";
$senha = "";
$mensagem = true;

$banco =  new Banco($servidor, $banco, $usuario, $senha, $mensagem);
```
Respectivamente, cada variável serve para:
* `$servidor` é o servidor onde o banco está localizado.
* `$banco` é o *banco* em que serão inseridos os *dados*.
* `$usuario` é o *usuário* do *banco*.
* `$senha` é a *senha* do *banco*.
* `$mensagem` é se as *mensagens* de **sucesso** serão ou não **exibidas** (portanto use `true` ou `false`).  

Para demonstrar o que pode ser feito, vou usar o seguinte banco  de exemplo (que chamei de `api_mrconstrucoes`), com a tabela:

![Imagem do banco relacional](img/banco.png)


```php
$sql = "INSERT INTO depoimentos(nome, email, depoimento) VALUES (:nome, :email, :depoimento)";
$dados = array(
  ":nome" => "Gustavo Leão Nogueira de Oliveira",
  ":email" => "gus.leaono@gmail.com",
  ":depoimento" => "Gostei muito da empresa. Me ajudou muito, fizeram a minha casa."
);

$resposta=$banco->executa_query_array($sql,$dados);


```

```php
$sql = "UPDATE depoimentos SET email = :email WHERE id = :id";
$dados = array(
  ":email" => "gustavo.leao.nogueira.2017@gmail.com",
  ":id" => 1
);

$resposta=$banco->executa_query_array($sql, $dados);
```

```php
$sql = "DELETE FROM depoimentos WHERE id = :id";
$id = 1;

$resposta=$banco->executa_query_parametro($sql,$id);
```


```php
$sql ="SELECT * FROM depoimentos";

$resposta=$banco->executa_query($sql);


while ($linha = $resposta->fetch(PDO::FETCH_ASSOC)) {
    echo "<p><strong>".$linha['nome'].":</strong>".$linha['email']."</p>";
    echo "<p><strong>Depoimento:</strong>".$linha['depoimento']."</p>";
    echo "<hr/>";
}
```

**Gustavo Leão Nogueira de Oliveira:** gus.leaono@gmail.com

**Depoimento:** Gostei muito da empresa. Me ajudou muito, fizeram a minha casa.

***

**Sônia Leão Nogueira:** sonia_leao69@gmail.com

**Depoimento:** Minha casa foi reformada pela empresa, fizeram um ótimo trabalho.
