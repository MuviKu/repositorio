# MuviKu
Um modelo de repositório Cydia. Este modelo contém exemplos de como você pode criar facilmente páginas de representação sem replicar suas páginas html. As páginas são estilizadas usando o Bootstrap, que é realmente fácil de usar. Você pode ver como é a aparência 
visitando este repositório de amostra no seu desktop ou telefone celular.A maioria dos dados desse repositório é armazenada em arquivos XML e carregada na página de representação dinamicamente. Veja o guia abaixo sobre como configurá-lo. Observe que este guia não cobre a criação de arquivos .deb, 
mas cobrirá brevemente as descrições de atribuição.

## Como usar este modelo

### 1. Download

Se você não está * hospedando seu repositório no [Github Pages] (https://pages.github.com/), pode fazer o download do arquivo zip [aqui] (https://github.com/supermamon/Reposi3/archive /master.zip) e extraia para uma subpasta no seu site.

Existem 2 opções para quem usa [Páginas do Github] (https://pages.github.com/).

A. Se você deseja usar seu root `nomedeusuario.github.io` como seu repositório, bifurque-o e renomeie-o para` nomedeusuario.github.io`. Portanto, ao adicioná-lo no Cydia, use `https: // nomedeusuário.github.io`.

B. Se você deseja usar uma subpasta para o seu `nome_de_usuário.github.io 'existente como seu repositório (exemplo: nome_de_usuário.github.io / repo`), bifurque esse repositório e renomeie-o para` repo`. Portanto, ao adicioná-lo no Cydia, use `https: // nomedeusuário.github.io / repo`.

Você pode alterar o `repo` para o que quiser, como o` cydia`, por exemplo. Portanto, seu URL de repositório seria `https: // nomedeusuário.github.io / cydia`.


#### 2. Personalize

**Liberar arquivo**

Edite o arquivo `Release`. Modifique os itens apontados por `<--`

    Origin: Reposi3  <--
    Label: Reposi3   <--
    Suite: stable
    Version: 1.0
    Codename: ios
    Architectures: iphoneos-arm
    Components: main
    Description: Reposi3 - a cydia repo template  <--

**Marca**



Edit `index.html`
* Change the page title in the `<title>Reposi3</title>` tag
* See lines 20 and 21.
* Change line 20 into your own **brand** and line 21 to have your own URL.
* Line2 30-51 contains the list of featured packages. You can edit those or remove them totally.
* Replace CydiaIcon.png.


**Page Footers**

Esses dados são os links que aparecem na parte inferior de cada representação. Os dados são armazenados em `repo.xml` na pasta raiz do seu repo.

```xml
<repo>
    <footerlinks>
        <link>
            <name>Follow me on Twitter</name>
            <url>https://twitter.com/reposi3</url>
            <iconclass>glyphicon glyphicon-user</iconclass>
        </link>
        <link>
            <name>I want this depiction template</name>
            <url>https://github.com/supermamon/Reposi3</url>
            <iconclass>glyphicon glyphicon-thumbs-up</iconclass>
        </link>
    </footerlinks>
</repo>
```


#### 3. Seu repo está quase pronto.
Nesse ponto, seu repositório está basicamente pronto para ser adicionado ao Cydia.
Você também pode visitar a página inicial do seu repositório, acessando `https://muviku.github.io/repositorio/`.
Ele virá com 2 pacotes de amostra, Pacote Antigo e Novo Pacote.
Cada um dos pacotes possui um link nesta página apontando para suas representações.
O próximo guia mostrará como atribuir e personalizar suas páginas de representação.

## Adicionando pacotes primeiro pacote ao seu repositório

#### 1. Adding a simple depiction page

Go to the depictions folder and duplicate the folder `com.supermamon.oldpackage`.
Rename the duplicate with the same name as your package name.
There are 2 files inside the folder - `info.xml` and `changelog.xml`.
Update the 2 files with information regading your package.
The tags are pretty much self-explanatory.
Contact [@reposi3](https://twitter.com/reposi3) or [@supermamon](https://twitter.com/supermamon) for questions.

`info.xml`.
```xml
<package>
    <id>com.supermamon.oldpackage</id>
    <name>Old Package</name>
    <version>1.0.0-1</version>
    <compatibility>
        <firmware>
            <miniOS>5.0</miniOS>
            <maxiOS>7.0</maxiOS>
            <otherVersions>unsupported</otherVersions>
            <!--
            for otherVersions, you can put either unsupported or unconfirmed
            -->
        </firmware>
    </compatibility>
    <dependencies></dependencies>
    <descriptionlist>
        <description>This is an old package. Requires iOS 7 and below..</description>
    </descriptionlist>
    <screenshots></screenshots>
    <changelog>
        <change>Initial release</change>
    </changelog>
    <links></links>
</package>
```

`changelog.xml`.
```xml
<changelog>
    <changes>
        <version>1.0.0-1</version>
        <change>Initial release</change>
    </changes>
</changelog>
```


#### 2. Link the depiction page your tweak's `control` file

You can add the depictions url at the end of your package's `control` file before compiling it.
The depiction line should look like this:

```text
Depiction: https://username.github.io/repo/depictions/?p=[idhere]
```

Replace `[idhere]` with your actual package name.

```text
Depiction: https://username.github.io/repo/depictions/?p=com.supermamon.oldpackage
```

#### 3. Rebuilding the `Packages` file

With your updated `control` file, build your tweak.
Store the resulting `.deb.` file into the `/debs/` folder of your repo.
Build your `Packages` file and compress with `bzip2`.

```sh
user:~/ $ cd repo
user:~/repo $ dpkg-scanpackages -m ./debs > Packages
user:~/repo $ bzip2 Packages
```

_Windows users, see [dpkg-scanpackages-py](https://github.com/supermamon/dpkg-scanpackages-py) or [scanpkg](https://github.com/mstg/scanpkg)._

#### 5. Cydia finalmente!

Se você ainda não o fez, vá em frente e adicione seu repositório ao Cydia.Agora você deve conseguir instalar o seu tweak em seu próprio repositório.

### Limpeza

Apenas uma etapa de limpeza, remova as debs que acompanham este modelo e execute novamente os comandos na etapa 3. Você pode manter as representações de amostra para referência, pois elas não são necessárias para o seu repositório.
