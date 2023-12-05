---
tags:
  - WEB
  - Pentest
---
# Path Transversal
Uma vulnerabilidade de segurança na Web *permite que um invasor leia recursos do sistema operacional*, como **arquivos locais no servidor** que executa um aplicativo.

O gráfico a seguir mostra como um aplicativo da Web armazena arquivos em `/var/www/app`. O caminho feliz seria o usuário solicitando o conteúdo de `userCV.pdf` de um caminho definido `/var/www/app/CVs`.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/45d9c1baacda290c1f95858e27f740c9.png)

 Se o invasor encontrar o ponto de entrada, que, nesse caso, é `get.php?file=`, ele poderá enviar algo como o seguinte, `http://webapp.thm/get.php?file=../../../../etc/passwd`

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/3037513935e3242f74bd0fe97833b5ac.png)

# LFI 1
Os ataques de LFI contra aplicativos da Web geralmente se devem à falta de conscientização de segurança por parte dos desenvolvedores.

1. Suponha que o aplicativo da Web ofereça dois idiomas e que o usuário possa selecionar entre *EN* e *AR*
```php
<?PHP 
	include($_GET["lang"]);
?>
```

2. Em seguida, no código a seguir, o desenvolvedor decidiu especificar o diretório dentro da função

```php
<?PHP 
	include("languages/". $_GET['lang']); 
?>
```

# LFI 2
Nesse caso, os erros são importantes para entender como os dados são transmitidos e processados no aplicativo Web.

```php
Warning: include(languages/THM.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
```

