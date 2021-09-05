Supondo que queremos criar o diretório `cache` no caminho `/var/lib/nginx` mas não possuímos ainda os diretórios `lib` e `nginx` criados, podemos utilizar a flag `-p` junto com o comando `mkdir` para criar todos os diretórios "pais":

```
$ mkdir -p /var/lib/nginx/cache
```