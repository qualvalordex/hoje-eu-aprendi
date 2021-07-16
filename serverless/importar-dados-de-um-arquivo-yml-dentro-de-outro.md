Supondo que eu tenha o seguinte arquivo `.yml`:

```yml
service: meu-servico

provider:
    name: aws
    region: sa-east-1
    runtime: node14.x
```

Eu posso separá-lo em dois arquivos, usando a notação `${file(caminho_para_o_arquivo)}` para importar um no outro:

`file0.yml`

```yml
service: meu-servico

provider: ${file(./file1.yml)}
```

`file1.yml`

```yml
name: aws
region: sa-east-1
runtime: node14.x
```